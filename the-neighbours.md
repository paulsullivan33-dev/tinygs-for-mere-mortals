# The Neighbours

TinyGS sits in a busy neighbourhood of
volunteer radio and satellite projects.
This chapter places the ones a newcomer
is most likely to confuse it with, and
says plainly what each does that TinyGS
does not — and vice versa.

## SatNOGS — the big sibling

**SatNOGS** is the other great open
ground station network, run under the
Libre Space Foundation. The differences
are of scale and of radio:

- **Radios.** SatNOGS stations are built
  around software-defined radios (RTL-SDR
  and up) attached to a computer, often
  with rotators that physically track a
  satellite across the sky. They cover
  VHF, UHF and beyond, and many
  modulations — amateur satellites of
  every kind, not only LoRa.
- **Scheduling.** SatNOGS observations
  are scheduled jobs with waterfall
  recordings and vetting by the
  community; it is closer to a shared
  observatory than to a fleet of
  always-on listeners.
- **Cost and effort.** A capable SatNOGS
  station costs more and asks more.
  TinyGS's whole proposition is that a
  thirty-dollar board, unattended, is
  enough to matter.

Neither replaces the other: many LoRa
satellites are only in TinyGS's world,
and most amateur satellites are only in
SatNOGS's. This series' RTL-SDR and GNU
Radio guides are the on-ramp to the
SatNOGS way of working.

## LoRaWAN — a different thing with the same radio

**LoRaWAN** uses the same LoRa radio
modulation for ground-based sensors —
meters, trackers, soil probes — talking
to gateways run by networks such as
Helium or The Things Network. The shared
word "LoRa" causes endless confusion:

- LoRaWAN is a complete network
  protocol — addressing, encryption,
  roaming — for devices near the ground.
- TinyGS satellites mostly speak **raw
  LoRa**: each mission's own packet
  format over the plain radio modulation.
- A LoRaWAN gateway is not a satellite
  station, and TinyGS firmware does not
  turn a board into a LoRaWAN gateway.
  Same silicon, different universe.

## Meshtastic — same boards, sideways purpose

**Meshtastic** firmware turns the same
Heltec/TTGO/T-Beam boards into an
off-grid text-messaging mesh: boards
relay short messages for each other over
LoRa, phone in your pocket. It aims
sideways — at other people on the
ground — where TinyGS aims up. The
kinship is practical rather than
functional: the hardware is
interchangeable, and many a TinyGS
station began life as a Meshtastic node
(recipe 5). This series' Meshtastic
guide covers the mesh in depth.

## APRS and the amateur satellite world

Amateur radio's own small-satellite
culture — APRS digipeaters in orbit, FM
and linear transponder satellites worked
by licensed operators with hand-held
antennas — is the tradition TinyGS
descends from and politely differs from:
TinyGS listening needs **no licence**,
because it is reception, and its stations
are automatic where the amateur tradition
is hands-on. If TinyGS gives you the
taste, the amateur satellite world is
where it leads; this series' Ham Radio
guide is the door.

## Commercial and agency ground stations

At the far end of the scale are ground
station *services* — companies that sell
satellite teams contact time on
professional dishes worldwide. They are
TinyGS's opposite in everything except
geometry: the same need (a satellite is
only reachable from the ground it is
over) answered with money instead of
volunteers. That both exist tells you the
need is real.
