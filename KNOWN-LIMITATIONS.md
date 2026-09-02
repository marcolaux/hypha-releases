# Known limitations

This is the list of things that are wrong, missing, or unproven in the Hypha
beta, written for someone deciding whether to trust it with their notes. None of
it is a surprise to the author — everything here is a known state, and most of it
is a deliberate trade rather than a bug waiting to be fixed.

If something here is a dealbreaker for you, that is the correct reaction, and
saying so is useful.

---

## Your data

**Keep your own backups.** All of the below assumes you have them.

**A backup file discloses less than it used to, and still discloses the
credential.** Until 2026-08-19 a backup encrypted your *notes* and nothing else:
tag names, notebook names, reminder titles and descriptions, settings values,
attachment filenames, MIME types and sizes all sat in the file as plain text,
including in a backup taken while the vault was locked. Backup format **v2**
seals all of that. Two things have not changed: the **vault credential is still
in the file** — by decision (2026-08-30): a backup must restore anywhere with
the passphrase alone, so the passphrase's strength is the backup's — and a host
with no keychain slot for the backup key still writes
**v1**, which leaks everything the old format did — as does a vault that has
only ever been opened from the keychain since v2 landed (the wrap is written
when you type the passphrase). Settings → Backup now says which of the two
applies, and unlocking with the passphrase once ends the second. The full accounting, and
which halves are still open, is in `BACKUP-CONFIDENTIALITY.md`. Treat a backup
as sensitive.

**A restored vault is a fresh copy, not the vault your other devices know.** A
new device restores a backup from its first screen (*Restore a backup*, since
2026-08-30) and gets every note and every attachment the backup held — but the
backup carries no device secret, so the restored vault cannot rejoin the sync
room the original was in. If another device still holds the vault, **join** it
from that device's invite instead of restoring beside it; restore is for the
case where no other device is left.

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
Since 2026-08-29.

**Vault names are stored in the clear** in the local registry. Decided, not
overlooked — but if you would name a vault something revealing, don't.

**There is no recovery for a forgotten passphrase.** None. Nobody can reset it,
including the author, because nobody else has anything to reset. This is the
direct cost of there being no server.

**The cryptography has not been independently audited.** It uses standard
primitives — libsodium, Argon2id, XChaCha20-Poly1305, Noise-XX, BLAKE2b — rather
than invented ones. That is a much weaker claim than "audited", and it is the
only claim being made.

---

## Sync

**Both devices have to be running.** There is no server holding a copy while one
is asleep. If your laptop is shut and you write on your phone, the laptop gets
it when it next opens and the two can reach each other — not before.

**Desktop-to-desktop over the internet is unproven.** Everything tested so far
has been one Mac and one phone. Mac-to-Mac on the same network works; Mac-to-Mac
across the internet has never been run by anyone. If you try it, please say what
happened.

**A note deleted on another device while you have it open** goes read-only
with a banner saying so, and the tab stays where it is. It used to leave you
typing into a note that no longer existed, which then saved as a new "Untitled"
note; that was fixed on 2026-08-19. The tab is deliberately not closed under
your cursor — you can see what happened and restore the note.

**Abandoning an "add vault" by closing the window** on the desktop can leave a
prepared vault behind that nothing cleans up. Use the flow to completion, or
expect to tidy up.

---

## Platforms

**macOS is Apple-silicon only.** No Intel build exists and none is planned.

**There is no Windows or Linux build yet.** The release workflow carries both
legs — Windows x64 as an installer and a portable `.exe`, Linux x64 as an
AppImage and a `tar.gz` — but they run on GitHub's hosted runners, and no
release has ever been built through them: every published version so far is
macOS-only. They are expected from the first release built after that capacity
is available again. When they arrive, two things will be true of them from the
start: **Windows will be unsigned**, so SmartScreen warns on first run
("More info" → "Run anyway"), and on Linux only the AppImage self-updates — the
`tar.gz` is updated by replacing it.

**Notarization is done and checked.** Every published build is signed with a
Developer ID identity and notarized by Apple; `stapler validate` and `spctl`
both pass on the app inside the published `.dmg` (`source=Notarized Developer
ID`). So the first launch should NOT need a right-click → Open. If yours does,
that is worth reporting — it would mean the staple did not survive the
download.

**Auto-update has never been observed working end to end.** This is no longer
for want of anything to update *from* — three versions are published (0.13.0,
0.14.0, 0.17.0), each with a real `latest-mac.yml` beside the installers. Nobody
has yet watched an installed copy find, download and restart into a newer one.
The first person to see a new version arrive by itself will be the first
evidence either way. Until then, assume you may have to update by hand.

**iOS needs 16.4 or newer**, on an **iPhone** — there is no iPad build, because
the layout has never been run on one. iOS comes through TestFlight, which
expires builds after 90 days. TestFlight access is by invitation.

**The iPhone build's peer-to-peer stack runs on a JavaScript engine that is new
to it.** The networking that syncs your notes lives in a separate embedded
runtime, and it had to be swapped from JavaScriptCore to V8 for 0.13.0 — Apple
refuses to distribute the JavaScriptCore build, because it reaches Apple APIs
that are not public.

Phone-to-laptop sync **over the same Wi-Fi has been tested on the new engine**
and works. What has not been tested on it: syncing over the **internet** rather
than a shared network, attachment transfer, and how the phone behaves over hours
of ordinary use — battery and warmth included. Everything known about those was
measured on the old engine. If sync misbehaves, or the phone runs hot, this is
the first thing to suspect, and saying so is genuinely useful.

---

## Features that are present but incomplete

**Semantic search does not work on the phone.** The machinery is partly built
and deliberately not wired up: the model is ~94 MB and it has never been
established what loading it costs in an iPhone WebView, so the phone gets
similarity but no semantic search box.

**Standard Notes import has never been pointed at a real export.** It reported
"Imported 0 notes" as a success for most of its life. That specific bug is
fixed; the import path is still untested against an actual file from Standard
Notes.

**Publishing to S3** has only ever been proven against a local MinIO server.
Real AWS addressing, temporary credentials and CDNs are unanswered, and the iOS
half has never run on hardware.

**Large photos added before mid-2026 show a placeholder until you backfill
them.** Photos taken as camera raws or HEIC before the preview pipeline existed
carry no thumbnail, and only an iOS device can generate one. Settings →
Attachments has a backfill that fills them in; until you run it, on a vault from
before then, expect gaps.

**An interrupted attachment transfer resumes only if the other device is new
enough.** Both ends have to understand it. Against an older device the
transfer restarts from the beginning after a short false start of a couple of
megabytes, and the same is true when an always-on relay is *forwarding* the
transfer rather than serving it from its own copy. A transfer that would not
fit on disk is declined before it starts, rather than filling the disk and
failing part-way.

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
