# Troubleshooting

The failure states of a TinyGS station,
roughly in the order people meet them.
Everything here comes from the project's
wiki and configuration documentation,
and from causes this guide's lab could
verify in the firmware itself; where a
check needs a live board, it says so.

## The station never appears on the map

Work outward from the board:

1. **Is it on your Wi-Fi?** The dashboard
   is reachable at the board's address on
   your network. If the board is still
   broadcasting its **My TinyGS** access
   point, its setup was never saved —
   start chapter 7 again.
2. **Are the MQTT credentials real?**
   Empty or mistyped user/password
   fields are the most common cause of a
   station that is locally healthy and
   publicly invisible. Re-ask the
   Telegram bot (`/mqtt`) and retype
   them; leave the server and port at
   `mqtt.tinygs.com` / 8883.
3. **Are the coordinates set?** A station
   without a location cannot be placed
   on a map, and cannot be tuned for its
   own sky.

## The station is online but hears nothing

First, patience: check chapter 4's
arithmetic — a quiet afternoon is
normal. If days pass with zero packets:

1. **Board type.** The wiki's standing
   warning: the Heltec V2 and TTGO
   LoRa32 V2 are often auto-detected
   wrong, and with the wrong board
   selected the LoRa communication does
   not work at all while everything else
   looks fine. Set the board by hand in
   `/config`.
2. **The band triple.** Board variant,
   antenna, and the satellites you expect
   must share a band. A 433 MHz antenna
   on an 868–915 MHz board (or the wrong
   board variant entirely — they look
   identical) is the classic silent
   station.
3. **The antenna connection.** These
   boards use tiny I-PEX/U.FL connectors
   that can sit half-seated from the
   factory, and the small print on some
   boards warns against powering the
   radio without an antenna connected.
   Reseat the connector; look for the
   antenna lead actually attached.
4. **The sky.** Move the station to a
   window, then outside for a day's
   test. Deaf indoors is a location
   verdict, not a board verdict
   (chapter 5).
5. **Is the satellite alive?** Check
   `tinygs.com/satellites` and the
   network's packet stream: if the whole
   network has heard nothing from that
   satellite either, the fault is in
   orbit, and no ladder will fix it.

## Packets appear, but rarely, and weak

That is propagation and placement, not
malfunction: low-elevation passes at the
edge of the footprint, an antenna behind
a roofline for part of the sky. The
dashboard's console shows signal
strength per packet; a station whose
best packets all arrive from one
direction is telling you where its
blind side is. Height and clearance
(chapter 5) are the remedies.

## The web installer cannot see the board

- Use Chrome or Edge — the installer
  needs the browser serial API.
- Try another USB cable: charge-only
  cables are the most common cause of a
  board that lights up but never appears
  as a serial device.
- Some boards need their boot button
  held while connecting to enter flash
  mode; the project's PlatformIO route
  (chapter 6) is the fallback the
  project itself recommends when the
  installer misbehaves.

## The panel asks for a password you do not know

The panel's user is always **admin**.
The password is the one set at first
setup; there is no published default to
try. The recovery is a reflash
(chapter 6) and a fresh setup — the
board keeps nothing you cannot rebuild
in ten minutes, which is the quiet
virtue of a one-purpose device.

## The station stopped after a router change

New router, new Wi-Fi name or password —
the board is still looking for the old
network. It falls back to its **My
TinyGS** access point; join it and redo
the Wi-Fi fields (chapter 7). Stations
survive firmware updates with
configuration intact, but they cannot
follow a network that changed its name
on them.

## This guide's own lab, honestly

The lab's problems were of a different
kind, and the guide keeps them in
`tinygs-lab/`: a plugin-style build
system that downloads an entire ESP32
toolchain before it compiles a line,
builds measured in minutes on a shared
machine, and a project whose tag names
are dates (`2603242` is a release, not a
typo). Chapter 11 tells that story,
including where the build struggled —
because a reader following the source
route will meet the same weather.
