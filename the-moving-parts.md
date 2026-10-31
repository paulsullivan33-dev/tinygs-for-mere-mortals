# The Moving Parts

A TinyGS station looks like one small
board with a stubby antenna. Inside the
idea there are five parts, and most
confusion about TinyGS is really confusion
about which part does what. This chapter
names them. Later chapters keep coming
back to this map.

## 1. The board

The hardware is an **ESP32** development
board with three things attached: a
**LoRa radio module**, a small **OLED
screen**, and an antenna socket. The ESP32
is a Wi-Fi microcontroller — a whole small
computer on a chip, with Wi-Fi built in.
It runs the show: it drives the radio,
draws the screen, keeps the Wi-Fi link,
and speaks to the internet.

The radio module is a separate chip from
Semtech's SX127x or SX126x families (the
newer SX1280, a 2.4 GHz part, also
appears). The radio chip is what actually
hears the satellite: it can be tuned to a
frequency and a set of LoRa parameters,
and it reports *a packet arrived* along
with the bytes. Everything else — knowing
*which* satellite that was, and what the
bytes mean — happens further up the chain.

Chapter 3 lists the boards the firmware
knows by name.

## 2. The firmware

The firmware is the program the ESP32
runs, and it is one program doing several
jobs:

- **Radio driver.** It configures the
  LoRa chip — frequency, bandwidth,
  spreading factor and the rest — using a
  library called RadioLib, and applies
  **Doppler compensation**, nudging the
  frequency as a satellite's motion shifts
  its signal. (A satellite approaching at
  orbital speed drags its own radio pitch
  with it, like a siren passing.)
- **A web panel.** The board runs its own
  little website: a configuration form, a
  dashboard with a live console and a
  world map, and a restart button. You
  talk to your station through a browser,
  not through the screen.
- **A network client.** It keeps a
  connection to the project's MQTT server
  and publishes what it hears.
- **An updater.** It can replace its own
  firmware over the air when the project
  publishes a new version.

The firmware is one build for many
boards: which board it is running on is a
*setting*, chosen in the web panel, not a
different download. The lab verified this
directly — the project's build file
defines a handful of chip-level variants,
while the firmware's own source carries a
table of 29 named board variants with
their pin layouts.

## 3. The modem configuration

A LoRa receiver can only listen one way at
a time: one frequency, one spreading
factor, one sync word. Satellites differ
in all of those, so "what am I listening
for right now?" is a real question, and
TinyGS answers it with a **modem
configuration** — a single line of JSON
text that completely describes the
listening setup. The project's tuning
guide gives this worked example, for the
satellite Norbi:

```json
{"mode":"LoRa","freq":436.703,"bw":250.0,"sf":10,"cr":5,"sw":18,"pwr":5,"cl":120,"pl":8,"gain":0,"crc":true,"fldro":1,"sat":"Norbi","NORAD":46494}
```

Frequency in megahertz, bandwidth,
spreading factor, coding rate, sync word,
the satellite's name and its NORAD
catalogue number — everything the radio
needs, in one string that can be stored,
sent and swapped. Chapter 8 is about who
writes this string: you, a template, or
the server itself.

## 4. The server

The project's server side (at
`tinygs.com`) is the network's brain:

- It **collects** every packet from every
  station over MQTT — a lightweight
  publish-and-subscribe messaging system,
  the same family of plumbing that home
  automation uses. (This series has a
  guide to MQTT if the word is new.)
- It **predicts**: knowing where each
  satellite is and where your station is,
  it can tell your board what to listen
  for next — the *automatic tuning* of
  chapter 8.
- It **decodes and publishes**: packets
  become readable telemetry on the
  website, points on the live map, and
  messages in the project's Telegram
  channels.
- It **manages**: firmware updates and
  remote configuration flow back down the
  same connection.

Your station's credentials for this server
are individual: the board generates a
one-time code and exchanges it for its
own MQTT username and password (the
firmware calls `api.tinygs.com` for this;
the human route is a Telegram bot, as
chapter 7 explains).

## 5. The community

The fifth part is people. Satellite teams
ask the network to listen for new
satellites. Station owners fill coverage
gaps — a satellite pass over the Pacific
is heard only if someone there is
listening. The project's coordination
happens in the open, mostly on Telegram.
A ground station network is a geometry
problem solved by volunteers: the more
stations, spread wider, the fewer packets
fall on empty ocean. Chapter 10 covers
what your station's packets become once
they join that whole.
