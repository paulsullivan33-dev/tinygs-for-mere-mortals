# What TinyGS Is

Somewhere above your house, right now, a
satellite the size of a loaf of bread is
falling around the Earth at about seven
and a half kilometres per second. Every
minute or so it calls out — a short radio
packet saying, in effect, *I am alive, my
battery reads this, my panels read that*.
The call is not aimed at anyone. It is a
shout into the dark, made on the chance
that somebody below is listening.

**TinyGS is the organised attempt to be
that somebody.** It is an open network of
small ground stations, run by volunteers
in their homes and gardens all over the
world. Each station is a cheap radio
board — an **ESP32** microcontroller with
a **LoRa** radio chip and a small screen —
running free firmware that listens for
those shouts. When a station hears one,
it passes the packet over home Wi-Fi to
the project's servers, which decode it
and publish it for everyone: on a live
world map, in station statistics, and in
Telegram channels that announce packets
as they arrive. The satellite operators —
often university teams and small space
start-ups — get telemetry from parts of
the Earth where they have no station of
their own. You get to take part in a
space programme for the price of a pizza.

The project's own one-sentence definition,
from its README, is worth quoting exactly:
TinyGS is "an open network of Ground
Stations distributed around the world to
receive and operate LoRa satellites,
weather probes and other flying objects,
using cheap and versatile modules." Note
the last part: the same radios that hear
satellites can hear other LoRa fliers —
high-altitude balloons and weather probes
— and the firmware also handles several
other radio modulations (FSK, GFSK, MSK,
GMSK, OOK) alongside LoRa. Satellites are
the heart of it, but the ears are general.

## Born for one satellite

TinyGS began in late 2019 as a weekend
project with a narrower name — ESP32
Fossa Groundstation — built to hear one
specific satellite, **FossaSAT-1**, a
pocket-sized Spanish satellite that was
the first to use LoRa as its main radio
link. FossaSAT-1 launched on 6 December
2019; four days later a community station
(run by YL3CT) caught its first packet.
The network then did what networks do: it
grew past its original purpose. Norway's
**Norby** satellite followed in 2020, the
**V-R3x** trio in 2021, and the project
renamed itself TinyGS — *Tiny Ground
Station* — and opened its doors to any
LoRa satellite that wants listeners.
Chapter 4 tells the satellite side of the
story.

## Listening is not transmitting

One fact shapes everything else in this
guide, and it is good news: **a TinyGS
station is, in normal use, a receiver.**
Hearing a satellite needs no amateur
radio licence in most places, because
receiving is not broadcasting. The boards
*can* transmit — the network's full name
for what stations do includes "operate",
and some satellites accept commands — and
the firmware has an **Enable TX** switch
for exactly that. The project's own
guidance is plain: on frequencies where
only licensed operators may transmit,
leave TX off unless you hold a licence,
because a station should never transmit
by accident. This guide treats stations
as listeners throughout.

There is a second honest fact to state up
front, because it decides whether TinyGS
is for you: **the network runs on the
project's servers.** Your board talks to
`mqtt.tinygs.com`; the map, the satellite
predictions and the automatic tuning all
live there too. That is what makes the
system simple — and it means the network
is a community service, not a piece of
infrastructure you own. Chapter 14
returns to this.

## What this guide's lab could and could not do

This guide was written from the firmware
itself. The lab cloned the project's
source code at its current release (tag
`2603242`), read it closely, and
**compiled the real firmware** for the
ESP32 with the project's own build setup
— chapter 12 shows that build and its
numbers. Everything the guide says about
what the firmware contains — the boards
it knows, the pages it serves, the server
it talks to — was read out of that code
or the project's own wiki.

What the lab did not have is a board.
There was no ESP32 on the desk, no LoRa
antenna, and no sky. So flashing a real
board, hearing a real satellite, and
watching a real packet arrive are taught
from the project's documentation and
labelled as such wherever they appear.
`criteria.md` keeps the full ledger: what
was built and read, and what was only
read. Nothing in this guide pretends a
packet was received.
