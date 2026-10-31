# Building the Firmware Yourself

Most station owners never build the
firmware — the web installer of chapter 6
exists precisely so they do not have to.
But building it is the deepest way to
understand what a station is, and it is
this guide's laboratory: everything the
earlier chapters claim about the firmware
was checked against the same source that
this chapter compiles. Here is what the
lab actually did, failures included. The
full transcripts are in `tinygs-lab/`.

## The setup

The lab cloned the project
(`github.com/G4lile0/tinyGS`) and checked
out its latest release tag, **2603242**
(commit `a311cedb…`, dated 2026-04-07 —
the project's tags are date-like numbers,
not version numbers in the usual sense).
PlatformIO Core 6.2.0 ran from a Python
virtual environment, with all of its
downloads — an entire ESP32 toolchain,
several hundred megabytes — kept on a
roomy disk, and the build target was the
base environment, **`ESP32`** (board
definition `heltec_wifi_lora_32`,
platform espressif32 6.10.0): the generic
ESP32 build that the web installer also
starts from, since the specific board is
a configuration choice, not a build
choice (chapter 3).

## What happened, in order

**Attempt 1 — the build that never
started** (930 s, FAILED). PlatformIO
downloaded the platform and toolchain,
then died parsing the build flags:
`OSError: 'python git_rev_macro.py'
exited 127`. The first build flag in the
project shells out to a small script that
stamps the firmware with the git revision
(`git describe --tags --always`). The
lab machine has `python3` but no plain
`python` on its path — exit 127, command
not found. An environment gap, not a
project defect: the fix was a `python`
symlink on the path. *Lesson: a build
that fails in the first tooling minutes
is usually about your machine, not the
project.*

**Attempt 2 — the guard** (102 s,
FAILED). Compilation began, and the main
sketch itself refused to continue:

```text
tinyGS.ino:86:2: error: #error "You are not using the correct version of RadioLib please copy TinyGS/lib/RadioLib on Arduino/libraries"
```

The firmware pins its radio library
exactly: an `#error` guard in the source
demands **RadioLib 7.6.0**, no other. But
the project's build file takes RadioLib
from a *moving* git address — the
maintainer's fork, at whatever its
current head is — with the fixed registry
pin (`jgromes/RadioLib @ 7.6.0`) sitting
commented out directly above. By the time
of this lab, the fork's head had drifted
to **7.8.1**. The release, as committed,
no longer builds unmodified: a pinned
expectation fed by an unpinned supply.
*Lesson: "latest" is not a version, and
any project that depends on a moving
target is a time capsule with a slow
leak.*

**Attempt 3 — the override that
wasn't** (37 s, FAILED). The lab tried to
pin the fork to its own 7.6.0-era commit
— `c778d876…`, the fork's state on
2026-04-06, the day before the TinyGS tag
was cut, whose version files read exactly
7.6.0 — via PlatformIO's sanctioned
`platformio_override.ini`. The build
still installed 7.8.1: PlatformIO *merges*
`lib_deps` across configuration files
rather than replacing them, so both
specs were present and the unpinned one
won. Recorded, because the next person
will try it too.

**Attempt 4 — success** (619 s,
SUCCESS). In the lab's throwaway clone —
and disclosed in the transcript, because
a lab that hides its edits teaches
nothing — exactly **one line** of
`platformio.ini` changed: the RadioLib
URL gained the commit fragment
`#c778d876…`. No source code was touched.
The build compiled the firmware and its
library dependencies and linked cleanly:

```text
RAM:   [==        ]  20.1% (used 65872 bytes from 327680 bytes)
Flash: [========  ]  75.6% (used 1337497 bytes from 1769472 bytes)
======================== [SUCCESS] Took 619.24 seconds ========================
```

The product, `.pio/build/ESP32/firmware.bin`,
is **1,344,208 bytes** (SHA-256
`f2fc6abd…e7e8ca`). The flash ceiling it
was measured against — 1,769,472 bytes —
is not an abstraction: it is the
`0x1B0000`-byte OTA app slot in the
project's own partition table
(`tinygs_4M_partition_table.csv`), which
reserves two such slots so a station can
update itself into the spare and fall
back if the new firmware fails. And the
git stamp from attempt 1's troublesome
script is verifiably inside the binary:
the string `2603242` — the release tag —
is embedded in the firmware image.

## What the build proves, and what it does not

It proves the release is real, buildable
software of a known size, with a known
dependency set (the graph lists RadioLib
7.6.0+sha.c778d876, ArduinoJson,
PubSubClient, IotWebConf, the SSD1306
display driver, and friends) — and that
today it needs one informed nudge to
build at all, which the project may well
fix in a later tag. It does not prove the
firmware *works*: nothing was flashed,
no radio transmitted or received, no
satellite was heard. Those claims in
this guide rest on the project's
documentation and on the source reading
of `tinygs-lab/` — labelled, as promised
on the home page, so you always know
which kind of knowing you are reading.
