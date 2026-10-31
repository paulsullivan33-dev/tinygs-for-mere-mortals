# TinyGS for Mere Mortals

**Space is overhead right now, whispering to
whoever bothers to listen.** All over the world,
small satellites — student CubeSats, experimental
PocketQubes, research craft — pass over your town
broadcasting their vital signs in a radio whisper
called LoRa. They are too quiet for the antennas
of big agencies to bother with and too far away
for anyone to hear by accident. They can be heard
on purpose, though: by a circuit board about the
size of a pack of cards, costing roughly thirty
dollars, sitting on a windowsill with a small
antenna — a **ground station**. TinyGS is the
open project that turns thousands of those boards
into one cooperative ear: your station hears a
satellite for the few minutes it is over you,
forwards what it caught to the project's servers,
and the satellite's team gets telemetry they
would otherwise never have seen. Your name goes
on the world map, next to your pin.

This guide explains the whole arrangement in
plain language: what the satellites are, what the
boards are, how a station is set up and tuned,
what happens to a packet after your station hears
it — and, just as honestly, the limits: the
passes are short, the sky is non-negotiable, and
the network lives on a small project's servers.

It is honest about what its lab did. The lab
**built the real firmware from source** with
PlatformIO — the project's current release,
compiled for its base ESP32 environment — and
read the firmware's own code for everything it
teaches about boards, console pages and the
data path. What the lab could not do is equally
plain: there is no board in the lab, no LoRa
antenna, and no sky a satellite can be heard
through from inside a computer — so flashing,
first setup and receiving a real pass are
written from the project's own documentation
and labelled documented-only wherever they
appear. Every source the lab used is listed in
`tinygs-lab/`, build transcripts included — one
failed build included, with the diagnosis.

## Chapters

1. **What TinyGS Is** — a citizen network of
   thirty-dollar ground stations, where it came
   from, and why hearing only is both legal and
   the whole point.
2. **The Moving Parts** — the five-piece mental
   model: board, firmware, modem configuration,
   server, community.
3. **The Boards** — ESP32 + LoRa boards, the
   radio chips and frequency bands, and the 29
   board variants the firmware itself knows by
   name.
4. **The Satellites** — why small satellites
   whisper in LoRa, the fleet the network hears
   (FossaSat, Norby and friends), and the anatomy
   of a pass.
5. **Antennas and Placement** — the antenna
   ladder, and the one rule that outweighs all
   hardware: a station needs sky.
6. **Installing TinyGS** — the three documented
   ways to flash the firmware, from the one-click
   web installer to PlatformIO.
7. **Your First Setup** — the board's own access
   point and panel, why coordinates matter, and
   the MQTT credential errand.
8. **Tuning** — who decides what your radio
   hears: the server's scheduler, web templates,
   or you, by hand.
9. **The Web Console and the World Map** — the
   pages the firmware serves (read from the
   source) and the public website where the
   network becomes visible.
10. **What a Received Packet Becomes** — the
    journey from radio frame to MQTT message to
    map pin, decoder and Telegram post.
11. **Building the Firmware Yourself** — the
    lab chapter: the real source build, what it
    produced, and the failure along the way.
12. **Recipes** — five complete jobs: first
    evening, better sky, one satellite, an empty
    place, a spare board.
13. **The Neighbours** — SatNOGS the big
    sibling, LoRaWAN the different thing with the
    same radio, Meshtastic the same hardware
    aiming sideways.
14. **Limits** — geometry, sky, central servers,
    transmission law, and the narrowness that is
    the design.
15. **Troubleshooting** — the silent station,
    the missing map pin, the wrong board type,
    and the rest of the usual failures.

Plus a **Glossary** of every term the radio
world insists on, and the **Writing Criteria**
this guide was held to — including what was
actually verified, and how.

## What it doesn't cover

- **Transmitting.** TinyGS stations here are
  listeners. Nothing in this guide teaches
  sending to satellites; the firmware's TX
  switch stays off, and chapter 14 explains the
  licensing reason.
- **Ham exams and licensing.** If TinyGS gives
  you the taste for the wider amateur satellite
  world, the Ham Radio guide in this series is
  the on-ramp.
- **Building radios from scratch.** The boards
  here are bought whole. The RTL-SDR and GNU
  Radio guides cover the software-defined path
  for everything TinyGS cannot hear.
- **Contributing code.** The project's firmware
  and decoder repositories welcome help; this
  guide teaches operating a station, not
  developing for the platform.

## How to use this guide

Read chapters 1–4 for the idea, in order —
they are short, and everything later leans on
the model in chapter 2. If you have a board in
hand, chapters 5–7 take you to a running
station, and 8–10 explain what it is doing
while it runs. Chapter 12 is the fast path for
the impatient; chapters 13–15 are for when
curiosity or trouble arrives. Values quoted
from the firmware — the board table, the
console routes, the MQTT topics, the release
the lab built — were read out of the release
source itself, and `tinygs-lab/` says exactly
which and how.

---

## Related guides in this series

- **[ESP32 for Mere Mortals](https://paulsullivan33-dev.github.io/esp32-for-mere-mortals/)** — the microcontroller every TinyGS station is built on, from blinking lights to real projects.
- **[PlatformIO for Mere Mortals](https://paulsullivan33-dev.github.io/platformio-for-mere-mortals/)** — the build tool the firmware's source route uses; chapters 6 and 11 assume nothing about it.
- **[MQTT for Mere Mortals](https://paulsullivan33-dev.github.io/mqtt-for-mere-mortals/)** — the publish-and-subscribe plumbing that carries every packet from station to server.
- **[Meshtastic for Mere Mortals](https://paulsullivan33-dev.github.io/meshtastic-for-mere-mortals/)** — the same boards, aimed sideways: an off-grid messaging mesh instead of the sky.
- **[ESPHome for Mere Mortals](https://paulsullivan33-dev.github.io/esphome-for-mere-mortals/)** — another life for spare ESP32 boards: sensors and switches around the house.
- **[RTL-SDR for Mere Mortals](https://paulsullivan33-dev.github.io/rtl-sdr-for-mere-mortals/)** — the wide-open receiver: everything TinyGS cannot hear, and the on-ramp to SatNOGS.
- **[Ham Radio for Mere Mortals](https://paulsullivan33-dev.github.io/ham-radio-for-mere-mortals/)** — the licence, the bands the fleet uses, and the amateur satellite world TinyGS descends from.

Part of the *For Mere Mortals* series — plain-language guides to tools, systems, and subjects that reward a closer look.

## License

Text: CC BY 4.0 (see `LICENSE`). Code examples: MIT (see `LICENSE-CODE`).
