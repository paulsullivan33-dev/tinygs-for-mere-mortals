# The Web Console and the World Map

A TinyGS station has two faces: the small
website it serves itself on your network,
and its reflection on the project's
public website. This chapter tours both.
The local half was mapped by this guide's
lab straight out of the firmware source;
the public half is described from the
project's documentation, labelled as
documented-only like everything in this
guide that needs a live station.

## The local panel, from the firmware

The board's web server (in the firmware
at `ConfigManager.cpp`) serves a handful
of pages:

- **`/` — the front door.** On first boot
  it is the captive-portal configuration
  page of chapter 7; afterwards it leads
  into the panel.
- **`/config` — configuration.** The full
  settings form: station identity, Wi-Fi,
  coordinates, MQTT credentials, board
  type and template, modem startup string,
  and the advanced parameters. This is
  the only place most settings live.
- **`/dashboard` — the station's face.**
  Status, a live console (the same log
  the serial port shows — what the radio
  is doing, satellite by satellite), and
  an embedded world map. Two helper feeds
  behind it, `/cs` and `/wm`, refresh the
  console and the map without reloading
  the page.
- **`/restart` — restart the board**
  from the browser.

Alongside the web panel, the board's
**serial console** over USB shows the
basic log — the panel's own fallback and
the first place to look when the network
side misbehaves (chapter 15).

The little OLED screen on the board is
the third, smallest face: current
satellite, signal readouts, last packet.
It tells you the station is alive at a
glance across the room; everything it
shows, the dashboard shows in more
detail.

## The public website

`tinygs.com` is where the network becomes
visible as a whole:

- **The world map and station list**
  (`tinygs.com/stations`): every station
  that has checked in, where it is, and
  its history — packets heard, satellites
  worked, uptime. Your station joins this
  page once it is configured and online.
- **The satellite list**
  (`tinygs.com/satellites`): the supported
  fleet of chapter 4, kept current by the
  project — the page to check before
  concluding a satellite has gone quiet.
- **The packet stream**
  (`tinygs.com/packets`): every packet the
  network receives, in real time, with the
  station that heard it and the decoded
  telemetry where a decoder exists.
- **Your personal area:** statistics for
  your stations, and the remote editing
  of chapter 8 — log in via the Telegram
  bot's `/weblogin` link.

Decoding deserves a word of its own: the
raw bytes from many satellites are just
numbers until a **decoder** — code the
project keeps in a companion repository —
turns them into battery voltages,
temperatures and positions. Not every
satellite has one, and a packet shown raw
is not a failure: it was still heard,
still forwarded, still counted, and the
satellite's own team can decode it
themselves.

## The Telegram channels

The network also speaks Telegram, and for
many station owners it is the liveliest
interface of all. Alongside the community
group and the personal bot (your source
of credentials and web logins), the
project runs two broadcast channels:
**@tinyGS_Telemetry**, carrying station
status and received packets as they
happen, and **@TinyGS_Test**, carrying
packets from stations in test mode. There
is a particular pleasure in seeing your
own station's name scroll past in the
telemetry channel seconds after a pass —
it is the network telling you, publicly,
that your windowsill just did a small
piece of space work.
