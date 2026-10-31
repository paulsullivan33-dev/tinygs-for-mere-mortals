# The Satellites

A ground station is only as interesting
as what it can hear. This chapter is
about the other end of the link: the
small satellites that speak LoRa, why
they exist, and what a pass actually
looks like from the ground.

## Why a satellite would use LoRa

LoRa was designed for sensors: tiny
radios that must stretch a small battery
across years by sending short packets
very slowly and very efficiently. Those
are exactly a small satellite's problems.
A CubeSat — the standard small satellite,
built in 10-centimetre cubes — has a
battery the size of a paperback and solar
panels the size of a placemat. It cannot
shout. LoRa lets it whisper: a slow,
narrow, error-corrected signal that a
sensitive receiver can pick out of noise
far below what an ordinary radio would
notice. Receivers on the ground have been
heard copying LoRa satellites more than
2,000 kilometres away, line of sight.

The trade is speed. These are not
broadband links. A packet is a few dozen
or a few hundred bytes: battery voltage,
temperatures, solar panel readings, a
beacon counter — the satellite's vital
signs, called **telemetry**. For a student
team whose satellite is otherwise silent
except over its own university, a global
network of volunteer listeners is the
difference between a few minutes of data
a day and a nearly complete picture.

## The fleet, honestly described

The supported list **changes**: satellites
are added as they launch, and removed as
they fail or re-enter. The live list is
the project's own page,
`tinygs.com/satellites`, and this guide
will not pretend to freeze it. But names
recur, and the project's own history and
real station logs (see `tinygs-lab/`)
name the cast:

- **FossaSAT-1** (2019) — the satellite
  TinyGS was born for; a 1P PocketQube
  from Spain's Fossa Systems, the first
  satellite to use LoRa as its main link.
- **The FossaSat-2E series** — Fossa's
  later constellation satellites; station
  logs show listeners tuning to individual
  members (2E1, 2E11, 2E13 among them).
- **Norby** (2020) — a 6U CubeSat from
  Novosibirsk State University, one of the
  network's first big additions.
- **Norbi and Norby-2** — later Russian
  LoRa satellites that appear constantly
  in station logs; the tuning guide's own
  worked example is Norbi, on 436.703 MHz.
- **V-R3x** (2021) — a trio of small
  satellites whose first packet was caught
  by a community station a day after
  deployment.
- **FEES** — a European educational
  satellite, another regular in the logs.
- **SATLLA-2B**, **GaoFen-7**, **RS52SD**,
  and more — the long tail of small
  missions the network has agreed to hear.

Beyond satellites, the firmware's other
modulations (FSK, GFSK, MSK, GMSK, OOK)
let stations follow **high-altitude
balloons and weather probes** — "other
flying objects", in the README's words.

Two properties of this fleet matter for
expectations. First, these are almost all
**low Earth orbit** satellites, a few
hundred kilometres up, circling the Earth
in about 90 minutes. Second, they are
amateur and experimental craft: they go
silent, they tumble, they die early.
Hearing nothing from a listed satellite
for a week can be the satellite, not you.

## Anatomy of a pass

From your station's point of view, a
satellite is not "up there" in general —
it is available in short appointments:

1. The satellite rises above your
   horizon. For a typical orbit that gives
   you a window of roughly **five to ten
   minutes**.
2. As it approaches, its signal arrives
   shifted **up** in frequency by its
   motion (Doppler shift); as it recedes,
   shifted **down**. At 437 MHz the total
   swing is on the order of ±10 kHz —
   small, but wider than a narrow LoRa
   channel, which is why the firmware
   compensates for it as the pass unfolds.
3. The satellite transmits its packets at
   intervals — every few seconds to every
   minute or so, depending on the mission.
   Your station needs one good packet in
   the window to have contributed.
4. The satellite sets. The next pass over
   your station may be hours away, though
   a busy fleet means *some* satellite is
   usually within reach every hour or two.

The server knows all of this in advance:
it tracks every satellite's orbit
(propagated from published orbital
elements, keyed by NORAD catalogue
number) and every station's coordinates,
so it can tell your board *what rises
next, and how to listen for it*. That
prediction loop — not the radio — is the
network's real trick, and chapter 8
explains the tuning machinery it drives.
