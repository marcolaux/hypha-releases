# Known limitations

This is the list of things to consider in the Hypha beta, written for someone deciding whether to trust it with their notes. None of it is a surprise to the author — everything here is a known state, and most of it is a deliberate trade rather than a bug waiting to be fixed.

If something here is a dealbreaker for you, that is the correct reaction, and
saying so is useful.

---

## Your data

**Keep your own backups.** All of the below assumes you have them.

**A vault credential is in the backup file** — a backup must restore on any device with
the passphrase, so the passphrase's strength is the backup's — Treat a backup
as sensitive.

**Weather is the one feature that sends a position off the device.** A daily
note's weather comes from Open-Meteo, which receives a position (a place you
typed, or your device's location cut to two decimals — about a kilometre) and
a date. The position is kept on the device only, in the app's own settings, and
never written into a note; but it is a third party, and it sees your IP address.
A position is refreshed in the background only when you have already granted
location, and at most once a day; hypha never raises a location prompt except
from the *Use my location* button in Settings. On iOS the position comes from a
CoreLocation bridge in the app's own shell that has not yet run on hardware —
the prompt, the reduced-accuracy grant and the "Allow Once" expiry are all
unverified on a device. On macOS the desktop app asks Chromium, whose
geolocation in Electron expects Google's network provider (which this build
does not carry) and is reported to hang without answering; the app gives up
after 8 seconds and falls back to the place you typed, so the weather is still
recorded — but *Use my location* may simply not produce a position on a Mac.

**Vault names are stored in the clear** in the local registry. This is needed for iOS so the share functionality lets the user choose a vault right in the share menu.

**There is no recovery for a forgotten passphrase.** None. Nobody can reset it,
including the author, because nobody else has anything to reset. This is the
direct cost of there being no server.

**The cryptography has not been independently audited.** It uses standard
primitives — libsodium, Argon2id, XChaCha20-Poly1305, Noise-XX, BLAKE2b — rather
than invented ones. That is a much weaker claim than "audited", and it is the
only claim being made.

---

## Sync

**Both devices have to be running so they can sync (if you don't use the peer relay).** There is no server holding a copy while one is asleep. If your laptop is shut and you write on your phone, the laptop gets it when it next opens and the two can reach each other — not before.

**Permanently deleting a note does not remove it from a relay immediately.** Your own
devices reclaim the note's text when you empty the trash on any one of them
(since 0.21.1), and refuse to take it back afterwards. An always-on relay is
different: it stores encrypted envelopes it cannot read, so it cannot tell that
one of them belongs to a deleted note, and it keeps them until its operator
prunes by age (`hypha-peer prune`, or `run --auto-prune-age`, which is off by
default). The content stays encrypted throughout, and no device will accept it
back — but if you want deleted notes gone from a relay you run, turn pruning on.

---

## Platforms

**macOS is Apple-silicon only.** No Intel build exists and none is planned.

**Windows and Linux builds are tested** occasionally 

---

## Features that are present but incomplete

**Semantic search does not work on the phone.** The machinery is partly built
and deliberately not wired up: the model is ~94 MB and it has never been
established what loading it costs in an iPhone WebView, so the phone gets
similarity but no semantic search box.

**Publishing to S3** has only ever been proven against a local MinIO server.
Real AWS addressing, temporary credentials and CDNs are unanswered, and the iOS
half has never run on hardware.

**The always-on relay does not keep partial transfers.** If a transfer *to*
the relay is interrupted it starts again from the beginning, because the relay
cannot tell whether the bytes it is holding belong to anything you still have.
Resuming *from* the relay works.

---

## What is deliberately absent

Not limitations so much as decisions, listed because their absence is sometimes
mistaken for an oversight:

- **No telemetry, no analytics, no crash reporting.** Nothing is sent anywhere.
  The cost is real and is worth stating: there is no automatic signal when
  something breaks for you, so a bug nobody reports is a bug nobody knows about.
- **No account, no cloud, no server.** There is nothing to sign up for.
- **No web version.**
