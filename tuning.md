# Tuning — Who Decides What to Hear

A LoRa receiver hears one satellite at a
time, in one way at a time — and the fleet
of chapter 4 is a crowd, each member on
its own frequency with its own settings.
So the central question of running a
station is: **at this minute, what should
the radio be listening for?** TinyGS has
three answers, and this chapter explains
all of them, because which one you use
changes what kind of station you run.

## The string that decides

Everything reduces to the modem
configuration of chapter 2: one JSON
string naming the mode, frequency,
bandwidth, spreading factor, coding rate,
sync word and satellite. Whoever writes
that string — you, a template, or the
server — controls the station. The string
your station starts with is stored in its
configuration as **modem startup**, so a
rebooted station resumes listening for
something sensible even before the server
checks in.

## Answer 1 — automatic tuning

With **automatic tuning** enabled (the
project calls it experimental, and
recommends it), the server does the
thinking. It knows every supported
satellite's orbit and your station's
coordinates; it predicts passes, picks
the most promising satellite overhead,
and sends your board a fresh modem
configuration as the pass approaches —
then the next one, and the next. During a
pass the firmware adds Doppler
compensation, sliding the receive
frequency to follow the satellite's
motion.

Your station becomes, in effect, a
terminal of the network's scheduler: it
listens where the fleet most needs ears.
If you have a favourite satellite you can
still set a default configuration, and
the system prioritises it. For nearly
everyone this is the right mode: pass
prediction is exactly the work a network
should do once, centrally, rather than
every station owner doing it nightly.

## Answer 2 — templates from the web

From your personal area on `tinygs.com`
(log in through the Telegram bot's
`/weblogin` command, which issues a
passwordless link), you can edit your
station's parameters directly — including
choosing one of the **predefined
templates** for the supported satellites,
or pasting your own modem configuration
string. Changes travel down the same MQTT
connection the packets travel up. Mind
the interaction: with automatic tuning
on, your choice may be overridden when a
better pass comes over — by design,
though your default is prioritised.

## Answer 3 — by hand, for experimenters

The local panel exposes the modem startup
string directly, and the tuning guide
documents every field — for LoRa: mode,
frequency (MHz), bandwidth, spreading
factor, coding rate, sync word, transmit
power, current limit, preamble length,
gain, CRC, the low-data-rate flag, and
the satellite's name and NORAD number.
FSK satellites have a parallel set (bit
rate, frequency deviation, sync-word
array, OOK shaping). There is even a
register-level escape hatch for radios
that need individual chip registers
written — with the project's own warning
that an incorrect register value can
damage the device. That sentence is the
honest summary of manual tuning: it is
how new satellites get tested before they
join the supported list, and it is not
where a first station should live.

## Which should you choose?

Leave automatic tuning on, set a default
satellite if your heart is set on one,
and let the scheduler work. Revisit the
question only when you have a reason the
network cannot have: testing a brand-new
satellite, chasing balloons, or studying
one satellite's behaviour pass after pass.
The rest of this guide assumes the
automatic station — it is the station the
network was designed around.
