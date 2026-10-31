# The Boards

You do not build a TinyGS station from
parts unless you want to. The normal route
is a ready-made development board that
already combines an ESP32, a LoRa radio
and a small screen on one piece of
circuitry, sold for roughly the price of a
restaurant lunch. This chapter explains
what to look for, and lists the boards
the current firmware knows by name —
read out of the firmware itself in this
guide's lab, not copied from a shop page.

## The two decisions hidden in a board

Every supported board is really two
choices soldered together:

**The radio chip.** The firmware works
with Semtech's SX127x family (SX1276,
SX1278) and the newer SX126x family
(SX1262, SX1268), plus the 2.4 GHz SX1280
in one build variant. The chip families
differ in sensitivity and features, but
for a buyer the practical difference is
the next item.

**The frequency band.** LoRa modules are
built for a specific slice of spectrum,
and satellites mostly live in the
**70-centimetre amateur band around
433–437 MHz** or in the sub-gigahertz
ISM bands (**868 MHz in Europe, 915 MHz
in the Americas**). Boards are sold in
variants: a "433 MHz" version and an
"868–915 MHz" version of the same board
are different hardware with different
radio front-ends and different antennas.
Chapter 5 explains how to choose; the
short version is that most TinyGS
satellites today shout loudest on
433 MHz, and the board must match the
band you intend to hear.

## The boards the firmware knows

Because one firmware serves all boards,
the firmware carries a table of every
board it understands — each entry is a
pin layout plus a radio type. The lab
read this table out of the release source
(`ConfigManager.cpp`): **29 named
variants**. The families in it:

- **Heltec WiFi LoRa 32 V1 and V2** — the
  project's original boards, in 433 MHz
  and 863–928 MHz versions, SX127x radios.
- **TTGO LoRa32 V1 and V2** (LilyGO) —
  the most common stations, 433 MHz and
  868–915 MHz, SX127x; a modified V2 with
  a hand-swapped SX126x module is also in
  the table.
- **TTGO T-Beam** (plus OLED, and the
  V1.0) — a board with GPS as well, in
  both bands; newer SX1262 T-Beam variants
  appear too.
- **LilyGO T3 V1.6.1** — both bands, plus
  a TCXO variant.
- **FOSSA 1W Ground Station** — a board
  made for this purpose by the Fossa
  community, in both bands.
- **Heltec LoRa32 V3** — the ESP32-S3
  generation, SX1262, covering
  150–960 MHz.
- **Custom builds** — ESP32, ESP32-S3 and
  ESP32-C3 development boards wired to
  bare SX126x/SX127x modules, with or
  without a screen.

The firmware usually **auto-detects**
which board it is on; the wiki warns that
a few (Heltec V2, TTGO LoRa32 V2) are
often detected wrong and must be set by
hand in the configuration panel, or the
radio will not work at all. If your board
is none of the 29, a **board template** —
a text description of its pin connections,
entered in the panel — teaches the
firmware a new board without recompiling,
and templates survive firmware updates.

## Screens, buttons and other details

Most boards carry a tiny OLED display
(0.96 inch is typical) that shows station
status, the satellite being tracked and
the last packet heard. It is a window,
not a control: everything configurable is
in the web panel, and a screenless custom
build is fully usable. The configuration
panel even has an OLED brightness setting,
with the project's sensible advice to run
it under 100 percent to extend the
screen's life.

Power is ordinary USB — the board runs
from a phone charger or any USB supply,
drawing little. There is no battery
requirement; T-Beam boards accept one,
which suits portable or solar experiments
but is not needed for a windowsill
station.

## What to actually buy

For a first station the community's
centre of gravity is a **TTGO/LilyGO
LoRa32 or Heltec WiFi LoRa 32, in the
433 MHz version** if your interest is the
satellite fleet in general: that is the
band where most supported satellites
transmit, and both board families are
auto-detected, well documented and cheap.
Buy from the maker's own store or a
reputable distributor where you can —
these boards are cloned often, and a
clone with a mistuned radio front-end is
a station that hears nothing and tells
you nothing about why. Keep the little
spring antenna that comes in the box for
first tests; chapter 5 is about what
replaces it.
