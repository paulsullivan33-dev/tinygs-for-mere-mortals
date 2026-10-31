# Recipes

Small, complete jobs. Like everything
hands-on in this guide, these are written
from the project's documentation and the
firmware's own configuration surface —
labelled documented-only, as the lab had
no board to perform them on.

## Recipe 1 — First station, first evening

**Goal:** a working station on a
windowsill by bedtime.

1. Buy a TTGO/LilyGO LoRa32 or Heltec
   WiFi LoRa 32 in the **433 MHz**
   version (chapter 3).
2. Flash it with the web installer
   (chapter 6) and join its **My TinyGS**
   access point.
3. In the panel: station name, panel
   password, home Wi-Fi, time zone, and
   your latitude and longitude (chapter
   7). Confirm the board type was
   detected correctly — set it by hand
   for the V2 boards.
4. Get MQTT credentials from
   @tinygs_personal_bot (`/mqtt`) and
   paste them in.
5. Leave **automatic tuning** and
   **automatic updates** on, **TX off**,
   and the stock antenna fitted.
6. Check the dashboard after an hour,
   and your station's page on
   `tinygs.com/stations` the next morning.

## Recipe 2 — Give the station a better sky

**Goal:** turn a windowsill station into
a real one, in one weekend job.

1. Choose the highest point you control
   with open sky — roof edge, gable,
   chimney, attic if the roof is not
   metal.
2. Fit a band-matched omnidirectional
   antenna there; weatherproof the
   connector (self-amalgamating tape is
   the usual tool).
3. Decide the topology: short coax down
   to the indoor board, **or** the board
   in a weatherproof box at the antenna,
   fed by USB power — the second is often
   better at UHF, where coax is lossy.
4. Compare a week of station statistics
   before and after. Height shows up in
   the numbers.

## Recipe 3 — Follow one satellite

**Goal:** study a single satellite
instead of sampling the fleet.

1. Pick your satellite from
   `tinygs.com/satellites`.
2. In your personal area on the website,
   set your station's default modem
   configuration to that satellite's
   template.
3. Keep automatic tuning on — your
   default is prioritised — or turn it
   off to dedicate the station entirely.
4. Watch your statistics for that
   satellite grow over a fortnight; its
   page shows the whole network's picture
   for comparison.

## Recipe 4 — A station for an empty place

**Goal:** contribute coverage where the
map is blank — the highest-value station
there is.

1. Look at the world map. Find the gap:
   an island, a coastline, a region with
   no pins for hundreds of kilometres.
2. If you live there — or travel there
   with a windowsill you can use for a
   week — the recipe is recipe 1 at that
   location, with correct coordinates.
3. A travel station left running in a
   hotel window for five days will log
   passes the network would otherwise
   have missed entirely. Tell the
   community group where it is; new pins
   in empty places are celebrated there.

## Recipe 5 — Try receiving with what you already own

**Goal:** spend nothing new.

Meshtastic nodes and other ESP32 LoRa
gear in the drawer are usually the same
boards TinyGS supports (Heltec, TTGO,
T-Beam — chapter 3). Flash TinyGS to the
spare board (chapter 6) for a satellite
week; flash back whenever you like. The
board does not care which network it
served last Tuesday.
