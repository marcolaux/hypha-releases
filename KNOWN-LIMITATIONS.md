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
in the file**, and a host with no keychain slot for the backup key still writes
**v1**, which leaks everything the old format did. The full accounting, and
which halves are still open, is in `BACKUP-CONFIDENTIALITY.md`. Treat a backup
as sensitive.

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

**A note open in a torn-off window while it is deleted on another device** can
leave you typing into a note that no longer exists, which then saves as a new
"Untitled" note. Known, has a fix designed, not yet built.

**Abandoning an "add vault" by closing the window** on the desktop can leave a
prepared vault behind that nothing cleans up. Use the flow to completion, or
expect to tidy up.

---

## Platforms

**macOS is Apple-silicon only.** No Intel build exists and none is planned.

**Windows and Linux builds exist from 0.15.0, and nobody has run them on real
hardware yet.** They are built by CI on GitHub's runners — Windows x64 as an
installer and a portable `.exe`, Linux x64 as an AppImage and a `tar.gz` — and
pass the same packaging checks as macOS, but no developer machine has opened a
vault on either. **Windows is unsigned**: SmartScreen warns on first run
("More info" → "Run anyway"). On Linux only the AppImage self-updates; the
`tar.gz` is updated by replacing it.

**Notarization is now done and checked.** 0.13.0 is signed with a Developer ID
identity and notarized by Apple; `stapler validate` and `spctl` both pass on the
app inside the published `.dmg` (`source=Notarized Developer ID`). So the first
launch should NOT need a right-click → Open. If yours does, that is worth
reporting — it would mean the staple did not survive the download.

**Auto-update has never been observed working end to end.** Still true, and it
cannot be tested yet for a structural reason: 0.13.0 is the first release, so
there is nothing to update *from*. The feed is real now — `latest-mac.yml` sits
beside the installers and resolves — but nobody has watched an installed copy
find, download and restart into a newer one. The first person to see 0.13.1
arrive by itself will be the first evidence either way. Until then, assume you
may have to update by hand.

**iOS needs 16.4 or newer**, on an **iPhone** — there is no iPad build, because
the layout has never been run on one. iOS comes through TestFlight, which
expires builds after 90 days. The first build (0.13.0, build 579) is uploaded
and accepted; TestFlight access is by invitation.

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

**Attachment transfers do not resume.** An interrupted transfer restarts from
the beginning. There is also no disk-space check anywhere before a transfer
starts.

---

## What is deliberately absent

Not limitations so much as decisions, listed because their absence is sometimes
mistaken for an oversight:

- **No telemetry, no analytics, no crash reporting.** Nothing is sent anywhere.
  The cost is real and is worth stating: there is no automatic signal when
  something breaks for you, so a bug nobody reports is a bug nobody knows about.
- **No account, no cloud, no server.** There is nothing to sign up for.
- **No web version.**
