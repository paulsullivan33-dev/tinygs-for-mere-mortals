# Antennas and Placement

The board is the cheap part of a ground
station; the antenna and its view of the
sky decide what the station is worth.
This chapter is the honest version: what
the little antenna in the box can do,
what a better one buys, and the one rule
that outweighs all hardware — **a
satellite receiver needs sky**.

## The physics in one paragraph

A satellite a few hundred kilometres away
is, by radio standards, extremely far and
extremely quiet. The signal that arrives
is faint, and your receiver competes with
everything else your antenna picks up.
Two things decide whether a packet is
copied: how much of the sky your antenna
can *see* (a satellite below your roof
line does not exist, whatever your
hardware), and how well the antenna is
**matched to the frequency** — an antenna
cut for 433 MHz is a poor listener at
868 MHz, and the wrong-band antenna that
ships in a mislabelled box is the classic
cause of a deaf station.

## The antenna ladder

**The included spring or stub antenna.**
Most boards arrive with a small helical
or stub antenna. It works: community
stations have logged real satellite
packets with the stock antenna at a
window. It is the right antenna for your
first day — it proves the station works —
and the wrong one to judge the hobby by.

**A better omnidirectional.** A
ground-plane, dipole or collinear antenna
built or bought for your band, mounted
high and in the clear (a mast, a roof
edge, an attic), is the standard upgrade.
Omnidirectional matters: satellites come
from every direction, and you are not
there to point. Height matters more than
gain figures: clearing the roof and the
neighbours' roofs widens every pass and
adds low-elevation minutes at both ends.

**Directional antennas.** A hand-held Yagi
pointed at a pass can pull in astonishing
results, and people do it for fun and for
difficult satellites — but a fixed station
that must be pointed is a station that
misses everything while you are asleep.
Treat directionals as an experiment, not
the station.

## Placement rules that actually matter

- **Sky first.** Rank locations by how
  much open sky they see, especially low
  toward the horizons in all directions.
  An upstairs window with a clear outlook
  beats a technically better antenna in a
  basement or behind a metal roof.
- **Outdoors beats indoors.** Walls,
  foil-backed insulation and modern
  low-emissivity window glass all tax a
  faint signal. An outdoor antenna with a
  few metres of coax usually wins over an
  indoor antenna with none; the board
  itself can stay inside, near the cable
  entry.
- **Match the band to the board and the
  antenna to both.** A 433 MHz board, a
  433 MHz antenna. Cross-checking this
  triple is the cheapest troubleshooting
  there is (chapter 15).
- **Mind the cable.** Long runs of thin
  coax eat UHF signals. Keep the run
  short, or put the whole station —
  board, in a weatherproof box — up at
  the antenna, fed by USB power and Wi-Fi.
  Whole stations live in garden boxes;
  the board's only wired needs are power.
- **Lightning and weather are real.**
  An outdoor antenna is a commitment:
  weatherproof joints, drip loops, and
  think about static and lightning
  protection as your local conditions
  demand. This guide flags the topic; it
  does not teach electrical safety.

## Tempering expectations

Even a well-placed station hears in
appointments: a pass is minutes long,
and the gaps between interesting passes
are measured in tens of minutes to hours.
A station at a window might log a handful
of packets on a quiet day and dozens on a
good one; community reports of a station
left running overnight — hearing seven
different satellites — come from decent
placement and a busy fleet, not from
expensive hardware. The reward curve of
TinyGS is mostly *placement, then
patience*. That is also what makes it
satisfying: your station's statistics on
the website are a direct record of your
sky.
