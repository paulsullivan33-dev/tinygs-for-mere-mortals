# Installing TinyGS

"Installing" TinyGS means putting the
firmware onto the board — an act called
**flashing**, writing the program into
the board's flash memory over USB. There
are three routes, from least to most
involved. This chapter describes them as
the project documents them; this guide's
lab built the firmware from source
(chapter 12) but had no board to flash,
so the flashing steps here are
documented-only, from the project's own
quick start and wiki.

## Route 1 — the web installer

The project's recommended first install
needs no tools at all:

1. Connect the board to your computer by
   USB.
2. Open **installer.tinygs.com** in
   Google Chrome or Microsoft Edge (the
   installer works through the browser's
   serial-port access, which is why those
   two browsers are named).
3. Follow the page: it detects the ESP
   chip in your board and selects the
   matching firmware variant itself, then
   writes it in one click.

The project calls the web installer
experimental and points anyone it fails
to route 2 — but for most first stations
it simply works, and it removes the
classic question of *which file do I
need* (answer, from chapter 3: the
firmware is the same for every board; the
variant that matters is the chip family).

## Route 2 — release files with PlatformIO

The traditional route: download the
latest release from the project's GitHub
releases page and flash it with
**PlatformIO**, the embedded build tool —
this series has a PlatformIO guide if the
tool is new to you. You pick the build
environment that matches your chip
(the current source defines ESP32,
ESP32-S3, ESP32-S3-USB, ESP32-C3 and an
ESP32-LILYGO_SX1280 variant) and
PlatformIO builds and uploads over the
same USB cable. This is also the route
that continues naturally into chapter 11,
where the lab builds from source.

## Route 3 — Arduino IDE

The project documents an Arduino IDE
route and is honest about it: it is "a
longer and hard path", because every
library dependency (RadioLib, ArduinoJson,
the display and configuration libraries)
must be installed by hand. It exists for
people who already live in that tool.
Nothing about the result differs.

## After the first flash

Whichever route you took, the board now
boots as a TinyGS station that knows
nothing about you: it starts its own
Wi-Fi access point named **My TinyGS**
and waits to be configured. That is the
start of chapter 7.

Two later-life facts belong in this
chapter, because they change how you
should feel about installing:

- **Updates do not need the cable.**
  Once configured, the station can update
  itself over the air — from its local web
  panel, or automatically from the
  project's update server when automatic
  updates are enabled (the default the
  project recommends). Configuration
  survives updates.
- **The first flash is the only delicate
  one.** A failed first flash is recovered
  by simply flashing again — the board's
  bootloader survives almost anything a
  USB cable can do to it. Nothing in the
  install can "brick" a board in normal
  use; the patient retry is the fix.
