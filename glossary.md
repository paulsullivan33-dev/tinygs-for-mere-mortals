# Glossary

**Access point (AP)** — a Wi-Fi network a
device creates for others to join. A new
TinyGS board starts one called
*My TinyGS* so you can configure it.

**Automatic tuning** — the mode in which
the TinyGS server predicts satellite
passes for your station and retunes its
radio by remote control, pass by pass.

**Bandwidth (BW)** — the width of a LoRa
channel in kilohertz. One of the modem
settings a receiver and a satellite must
share to hear each other.

**Board template** — a text description
of a board's pin connections, entered in
the configuration panel, teaching the
firmware a board it does not know by
name. Templates survive firmware updates.

**Coding rate (CR)** — how much extra
error-correction data a LoRa transmission
carries. More correction survives worse
conditions and costs time.

**CubeSat** — the standard small
satellite form: one or more cubes 10 cm
to a side (1U, 3U, 6U). Most of the TinyGS
fleet are CubeSats or smaller.

**Dashboard** — in TinyGS, two things
with one name: the station's own web page
(`/dashboard`) showing its console and
map, and your personal area on
tinygs.com.

**Decoder** — code, kept by the project,
that turns a satellite's raw packet bytes
into readable values such as battery
voltage and temperature.

**Doppler shift / compensation** — the
change in a satellite's apparent radio
frequency caused by its orbital motion,
and the receiver's trick of sliding its
tuning during a pass to follow it.

**ESP32** — a low-cost microcontroller
with built-in Wi-Fi, the computer at the
heart of every TinyGS station. Variants
include the ESP32-S3 and ESP32-C3.

**Flashing** — writing firmware into a
board's flash memory, over USB. The first
thing done to a new station, and the
recovery for most software trouble.

**Ground station** — the Earth end of a
satellite link: a receiver (and sometimes
transmitter) that hears a satellite while
it is overhead. TinyGS stations are
ground stations that cost about a pizza.

**ISM band** — licence-exempt spectrum
set aside for industrial, scientific and
medical uses — here, 433 MHz, 868 MHz
(Europe) and 915 MHz (Americas) — where
LoRa devices are allowed to operate.

**LoRa** — a radio modulation designed
for very long range at very low power and
very low data rates, by spreading a
signal thinly over a wide channel.
Invented for ground sensors; adopted by
small satellites for the same reasons.

**Modem configuration** — the single
JSON string that fully describes how a
station listens at a given moment:
mode, frequency, bandwidth, spreading
factor, and the satellite it names.

**MQTT** — a lightweight messaging
protocol of publishers and subscribers,
used here between stations and the
TinyGS server over an encrypted
connection (port 8883).

**NORAD number** — the catalogue number
of an orbiting object in the public
satellite catalogue. Orbits, predictions
and modem configurations all key on it.

**OTA (over the air)** — updating a
device's firmware through its network
connection rather than a cable. TinyGS
stations can update themselves this way.

**Packet / frame** — one short burst of
data from a satellite: the unit a station
receives, forwards and gets credited
with.

**Pass** — the few minutes a satellite is
above a station's horizon and can, in
principle, be heard there.

**PocketQube** — a satellite form smaller
than a CubeSat, built in 5 cm cubes.
FossaSAT-1 was one.

**RadioLib** — the open-source radio
library the TinyGS firmware uses to
drive its LoRa chips.

**Spreading factor (SF)** — LoRa's
main speed-versus-sensitivity dial.
Higher numbers are slower and can be
heard much fainter and farther away.

**SX127x / SX126x / SX1280** — Semtech's
LoRa radio chip families: the ears of
the station. The first two work in the
sub-gigahertz bands; the SX1280 is a
2.4 GHz part.

**Sync word** — a short marker at the
start of a LoRa transmission that tells
a receiver "this packet is for your
kind of network". A receiver ignoring
other sync words ignores other fleets.

**Telemetry** — a machine's report on
itself: voltages, temperatures,
counters. What the fleet's packets
mostly contain.

**Test mode** — a station setting that
marks its packets as tests, so practice
traffic never pollutes the real record.
