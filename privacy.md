---
title: hypha — Privacy Policy
---


**hypha**
Last updated: 19 August 2026

<!--
  THIS FILE IS THE SOURCE. It is published at
  https://marcolaux.github.io/hypha-releases/privacy (GitHub Pages, from
  `marcolaux/hypha-releases`), which is the address the App Store listing
  points at. Do not edit the copy there by hand — run
  `npm run release:changelog`, which regenerates it from this file with the
  Jekyll front matter the page needs.

  An HTML comment rather than a visible note: this text is for whoever edits
  the policy, not for whoever has to read it.
-->

## The short version

Hypha collects nothing. There is no account, no server, and no analytics. Your
notes are stored on your own devices, encrypted, and synchronised directly
between devices you have paired together. No data is sent to the developer or to
any third party.

The rest of this page says the same thing in the detail a policy needs.

## Who is responsible

Marco Laux. Contact: **krst@riseup.net**.

## What data Hypha collects

**None.**

Specifically, Hypha does not collect, transmit or store on any server:

- personal information of any kind;
- your notes, their titles, or their contents;
- your attachments, tags, notebooks or reminders;
- usage, analytics, telemetry, diagnostics or crash reports;
- advertising identifiers, device identifiers or IP addresses;
- contacts, location, calendar or health data.

Hypha has no user accounts. There is nothing to sign up for and nothing for the
developer to hold.

## Where your data lives

On your devices, and nowhere else.

Notes are stored in an encrypted database on the device. Note titles and bodies
are encrypted with a key derived from a passphrase that only you know, using
Argon2id and XChaCha20-Poly1305. The developer cannot read them, and cannot
recover them if you forget the passphrase.

Some data alongside your notes — tag and notebook names, reminder titles and
descriptions, attachment filenames, and settings — is stored unencrypted on your
own device. It never leaves your devices, but it is not protected by your
passphrase. This is documented in the app's known-limitations page.

## Synchronisation

If you pair two or more of your own devices, Hypha synchronises directly between
them, peer to peer. There is no intermediary server that holds a copy.

- On the same local network, devices connect to each other directly.
- Across the internet, devices find each other through a public distributed hash
  table (DHT). Participating in that network necessarily exposes your device's
  IP address to peers it connects with, as any peer-to-peer connection does. The
  contents of the connection are end-to-end encrypted using a Noise handshake,
  and only devices you have explicitly paired can join your vault.

If you never pair a second device, Hypha makes no network connections for
synchronisation at all.

## Optional features that make network connections

These are off unless you turn them on or use them, and each is listed because it
is the only way data leaves your device:

- **Update checks.** The desktop app checks for a new version by requesting a
  file from GitHub. This reveals your IP address to GitHub, as visiting any web
  page would, and nothing about you or your notes is sent with the request. The
  check runs only when you open Settings → Updates or explicitly ask for it —
  never in the background and never at startup.
- **Publishing a note to the web.** If you explicitly publish a note, its
  contents are uploaded to storage that you configure and control. Only notes you
  choose to publish are ever uploaded.
- **Semantic search.** If you enable it, a language model is downloaded once from
  its own source. The model then runs entirely on your device; no note text is
  sent anywhere.
- **Web clipping.** If you save a web page, Hypha fetches that page, and may
  fetch images it references, from the sites that host them.

## Permissions the app asks for

- **Local network** — to find and connect to your other devices on the same
  Wi-Fi. Declining it means local sync will not work; everything else does.
- **Camera** — only to scan the pairing code when you add a device.
- **Microphone / Photo library** — only when you choose to attach something.

None of these send data anywhere. They are used to put data into your vault.

## Children

Hypha is not directed at children and collects no data from anyone, including
children.

## Third parties

Hypha has no third-party SDKs, no advertising, no attribution frameworks and no
analytics providers. It shares no data with anyone, because it holds none.

## Your rights

Because the developer holds no data about you, there is nothing to request,
correct, export or delete from any server. Your data is in your possession. You
can export it or delete it from within the app at any time, and uninstalling the
app removes it from that device.

## Changes to this policy

If this policy changes, the updated version will be published at the same
address and the date at the top will change. Material changes will be noted in
the app's changelog.

## Contact

**krst@riseup.net**
