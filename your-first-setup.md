# Your First Setup

A freshly flashed board wakes up as a
small island: it starts a Wi-Fi access
point called **My TinyGS** and serves its
configuration panel on it. This chapter
walks the setup the project's wiki
documents — which fields matter, why the
station asks for your coordinates, and
the one errand (MQTT credentials) that
takes you outside the panel for a minute.

## Joining the island

Connect a phone or laptop to the
**My TinyGS** network. Most devices pop
up the panel by themselves, as they do
with hotel Wi-Fi; if yours does not,
browse to **192.168.4.1**. The panel is
served by the board itself (this guide's
lab read its route table out of the
firmware: the configuration form lives at
`/config`, and the station dashboard at
`/dashboard`). You are configuring the
board directly — no account, no cloud,
nothing has left your desk yet.

## The fields that matter

From the project's configuration
documentation, in the order you will
meet them:

- **Ground Station name.** Any name you
  like, ideally unique — this is the name
  your station wears on the public map.
- **Ground Station password.** The
  password for the panel itself. The user
  name is always **admin**. Set a real
  one: this panel can retune and restart
  your station.
- **SSID and password.** Your home Wi-Fi,
  so the station can reach the internet
  and stop being an island.
- **Time zone.** So the station's clock —
  and its logs — make sense locally.
- **Latitude and longitude.** The heart
  of the setup. The server uses your
  coordinates to predict which satellites
  pass over *you*, and the map uses them
  to show where a packet was heard. A
  station with wrong coordinates will be
  tuned for somebody else's sky.
- **Board type.** Usually auto-detected;
  the wiki singles out the Heltec V2 and
  TTGO LoRa32 V2 as boards often detected
  wrong — with those, choose the board by
  hand or the radio stays silent.
- **Enable TX.** Leave it **off** unless
  you hold an amateur radio licence and
  know you need it (chapter 1). The
  station receives perfectly well without
  it and will never transmit by itself.
- **Automatic tuning** and **automatic
  firmware update.** Both recommended on
  by the project: tuning is chapter 8,
  updates are chapter 6's promise kept.
- **OLED brightness.** Cosmetic; the
  project suggests below 100 to spare the
  screen.

## The MQTT errand

Two fields are not yours to invent:
**MQTT user** and **MQTT password** — your
station's credentials for the project's
server (`mqtt.tinygs.com`, port 8883;
leave the server fields alone). The
project issues them through Telegram:

1. Join the TinyGS community group on
   Telegram (linked from the project
   site).
2. Open a private chat with the project's
   bot, **@tinygs_personal_bot**, and send
   `/mqtt`.
3. Type the credentials it gives you into
   the panel.

Under the surface, the board can also do
this itself: the firmware generates a
one-time code and exchanges it at
`api.tinygs.com` for credentials — the
lab read that mechanism in the source.
Either way, the credentials are *your
station's*, and they are what lets the
server collect your packets and manage
your station (including re-tuning it and
updating it, if you left those doors
open).

## What "done" looks like

Save, and the board restarts onto your
home Wi-Fi. From then on the panel lives
at the board's address on your network,
and the dashboard shows the station's
state: its console log, the satellite it
is listening for, and a world map of the
network. Your station also appears on the
public map at `tinygs.com` once it checks
in. It may hear nothing for a while —
chapter 4's appointments apply from the
first minute. Silence in the first hour
is weather, not failure; chapter 15 helps
you tell the difference after the first
day.
