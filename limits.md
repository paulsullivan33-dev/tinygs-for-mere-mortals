# Limits

What TinyGS cannot do, and what it does
not promise. Read this chapter before
buying anything; most disappointment
with the project is a limit discovered
late that could have been known early.

## Geometry rules everything

A station can only hear a satellite that
is above its horizon, and a low-orbit
satellite is above any one horizon for
minutes at a time. No antenna, amplifier
or enthusiasm changes this. Consequences:

- Reception is **appointments, not a
  stream**: passes of five to ten
  minutes, gaps of tens of minutes to
  hours, and whole stretches — especially
  at night, in sparse fleet hours — with
  nothing to hear.
- Two stations a continent apart hear
  **different skies**. Your statistics
  are partly your address.
- A satellite that stops transmitting —
  a failure, a tumble, end of life — is
  indistinguishable, from your station,
  from a satellite that simply is not
  over you. Check the fleet's pulse on
  `tinygs.com/satellites` before blaming
  your hardware.

## You will receive nothing without sky

The project's entry price is a board;
its real price is a **view of the sky**.
A station indoors behind modern glass,
metal roofing or dense city stone can be
correctly built, correctly configured
and permanently deaf. Chapter 5's ladder
— window, then outdoors, then height —
is not an optimisation path; for some
buildings it is the difference between
the hobby and a blinking ornament. Judge
your location before your equipment.

## The network depends on the project's servers

TinyGS is decentralised in hardware and
centralised in coordination. The map,
the packet record, pass prediction,
automatic tuning, credential issuing and
firmware updates all run on
`tinygs.com` infrastructure. Plainly:

- If the project's servers are down,
  stations keep their last settings and
  keep listening — but the network as a
  public whole pauses.
- If the project ever ended, the
  firmware is open (GPL-3.0) and the
  MQTT address is a setting, so the
  boards would not become e-waste — but
  the living network described in this
  guide is a service a small team runs,
  and it lasts exactly as long as they
  run it. That is the standard bargain of
  community infrastructure, stated
  where you can see it.

## Reception is easy; transmission is a regulated act

This guide's stations are listeners, and
listening needs no licence in most
jurisdictions. The moment you enable TX,
different rules apply: several bands the
fleet uses sit inside amateur radio
allocations, where transmitting without
a licence is unlawful, and a misconfigured
station can also interfere with the very
satellites it serves. The firmware's own
warning stands: never transmit without
intending to, and do not enable TX
without the licence the band requires.
(Local rules vary; this guide does not
give legal advice.)

## A narrow kind of knowledge

The network hears **LoRa (and a few FSK
family) satellites only** — a deliberate
narrowness. The amateur satellites on
FM voice, the weather satellites on APT
or LRPT, the ISS, everything on VHF SSB:
all invisible to a TinyGS station, not
from failure but from design. SatNOGS
(chapter 13) is the wider net. Likewise
the telemetry is what it is — vital
signs, not payloads: you will learn a
satellite's battery voltage, not see
through its camera.

## And the small print of real stations

Boards are cheaply made and clones
vary; OLED screens fade over years
(hence the brightness advice); Wi-Fi
routers get replaced and take station
connectivity with them until the panel
is revisited; and the fleet churns —
this year's faithful satellite is next
year's silent orbit. None of this is
hidden by the project. All of it is the
texture of running a tiny piece of
space infrastructure from a windowsill,
which is, in the end, the hobby itself.
