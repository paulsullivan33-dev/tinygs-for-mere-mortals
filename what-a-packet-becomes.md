# What a Received Packet Becomes

Everything so far exists for one moment:
the radio chip raises its hand and says a
packet has arrived. This chapter follows
that packet on its journey — through
your station, across the network, and
into the several afterlives a packet can
have. The lab read this path in the
firmware source; the journey is short,
and every step is checkable.

## Step 1 — the radio hears

The firmware's radio layer (built on
RadioLib) is parked on a frequency with a
modem configuration, applying Doppler
compensation as the pass unfolds. When a
preamble and sync word match what it is
listening for, the chip delivers the
frame: raw bytes, plus the signal's
report card — received signal strength
and signal-to-noise ratio. The firmware
records which modem configuration was in
force (its status keeps the "last packet"
modem info alongside the current one), so
a packet always knows which satellite
setting caught it.

## Step 2 — the station publishes

The station wraps the frame and publishes
it to the project's MQTT broker over its
encrypted connection (port 8883, with the
station's own credentials). In the
firmware, received packets go out on the
station's **rx** topic; the same client
sends **welcome** when it connects,
**ping** and **status** to report health,
and receives commands — retunes, status
requests, configuration — on subscribed
topics. That two-way street is the whole
relationship: the station is a sensor the
network can aim.

## Step 3 — the network decodes and tells

On the server, the frame joins the public
record:

- It appears in the **live packet
  stream** and on the map, credited to
  your station.
- If a **decoder** exists for that
  satellite, the bytes become telemetry —
  voltages, temperatures, counters — on
  the satellite's page, where the
  satellite's own team can use them.
- It is announced in the **Telegram
  telemetry channel**, and it increments
  your station's statistics: packets,
  satellites, days active.
- Where a satellite's operator has asked,
  and you have not opted out (the
  "Telemetry to third party" setting),
  the data is forwarded to the operator —
  often a university team. This sharing is
  not a side effect of the network; it is
  the network's stated purpose.

## What a packet is worth

One packet from one station is a small
thing: a single snapshot of a satellite's
health at one moment. The network makes
it valuable three ways. **Coverage**: a
packet over your town may be the only
copy anyone got of that transmission —
the satellite will not repeat it for
you. **Corroboration**: when three
stations hear the same frame, the record
is trustworthy. **Continuity**: strung
together, snapshots become a story — a
battery slowly failing, a satellite
recovering from a tumble — that no single
operator station could assemble alone.

This is also the honest answer to "what
should I optimise?" Not your station's
ego — the network's geometry. A modest
station in an empty region (an island, a
southern-ocean coastline, anywhere the
map is blank) contributes passes nobody
else can hear. The map's gaps are the
network's true to-do list, and chapter 12
makes a recipe of filling one.
