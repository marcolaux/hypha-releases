# Privacy Policy

**hypha**
Last updated: 29 October 2026

<!--
  THIS FILE IS THE SOURCE. It is published at
  https://github.com/marcolaux/hypha-releases/blob/main/privacy.md — GitHub's
  own markdown view of a copy in `marcolaux/hypha-releases` — which is the
  address the App Store listing points at. Do not edit the copy there by hand;
  run `npm run release:changelog`, which republishes this file verbatim.

  It was served by GitHub Pages at
  https://marcolaux.github.io/hypha-releases/privacy until 2026-09-04, when
  Pages was turned off on that repo. That URL now 404s, so the App Store
  listing has to name the one above.

  An HTML comment rather than a visible note: this text is for whoever edits
  the policy, not for whoever has to read it.
-->

## The short version

Hypha collects nothing. There is no account, no server, and no analytics. Your
notes are stored on your own devices, encrypted, and synchronised directly
between devices you have paired together. Nothing about you or your notes is
sent to the developer or to any third party; the two exceptions on record —
an engine's telemetry in five earlier builds, and the optional beta relay
service — are described below, as is every feature that makes a network
connection.

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
- contacts, calendar or health data;
- your location — with the exceptions you opt into, described under *Optional
  features* below: a coarse position, sent to a weather service or, on an
  iPhone or iPad, to Apple's geocoder for a place name, and never stored by the
  developer.

Hypha has no user accounts. There is nothing to sign up for and nothing for the
developer to hold.

Two things have to be disclosed against that list:

- **An engine's telemetry, in builds 0.99.25 to 0.99.30 (October 2026).** The
  search-by-meaning engine Hypha embeds (Microsoft's ONNX Runtime) enables its
  own usage telemetry by default, and those builds shipped without turning it
  off. While a model session was loaded they sent technical events about the
  engine itself (model loads, timings, device facts) to Microsoft's collector.
  No note content and nothing you typed was part of it. Every build from
  0.99.31 on has it switched off at both of the engine's switches.
- **The beta relay service, if you enrol with an invite code.** This is the
  one thing run by the developer that your device talks to, and only if you
  enter a code under Settings → Sync. It can see your sync key's public half,
  which vault route tags and context ids it maps to, connection and byte
  volumes, and your IP address (its web server's own logs included). It never
  sees vault keys, note content, or an email address — there is none to give.
  "Stop using" in the same place ends it.

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
  table (DHT). Joining it starts with a request to three public entry nodes
  (`hyperdht.org`, run by the makers of the DHT library), which see your
  device's IP address and the public half of its sync key, as does every peer
  the connection then passes through, as any peer-to-peer connection does. The
  contents of the connection are end-to-end encrypted using a Noise handshake,
  and only devices you have explicitly paired can join your vault.

If you never pair a second device, Hypha makes no network connections for
synchronisation at all.

## On-device Apple Intelligence

On a Mac or iPhone with Apple Intelligence (macOS 27 / iOS 27), Hypha uses the
system's **on-device** language model for three things, and never a server — not
Apple's Private Cloud Compute, not anyone else's:

- **Pictures in notes** get a one-sentence description of what they show, so
  search can find them. The text in a picture is read by the operating system's
  text recognition, also on the device.
- **Web clips** of pages that do not say what they are: the model reads the
  clipped page, decides which of your note types it fits, copies the facts the
  page states into the note's properties and writes a short summary. Values the
  page does not contain are discarded. This can be turned off in Settings →
  Capture & web clips.
- **The summary of the day**, only if you turn it on (each vault asks once):
  the model reads the notes you wrote or edited that day and writes a short
  summary into your daily note. The list of open and finished tasks next to it
  is taken from your notes, not from the model. The notification that brings
  you there carries a fixed text and nothing from your notes.

Nothing in any of these cases leaves the device. The descriptions, properties and
summaries are part of your notes: encrypted, and synced to your other devices
like the rest of the note.

**Note types** (Movie, Recipe, and the ones you make): their names and field
labels are stored the way tag and notebook names are, inside the vault's
encrypted database but not sealed a second time. The *values* of a note's
properties are additionally sealed with that note's own key, like its title.

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
- **Notifications on iPhone.** If you turn on "Notify me about new messages"
  for a vault, a notification about a new chat message, comment or mention
  travels from the device that wrote it, through a relay that vault uses, to
  Apple's push service and to your phone. The relay and Apple see only that
  something arrived, when, how large it was, and for which phone — never what
  was written or for which vault; the text they carry is encrypted to a key
  that exists only on your phone, which decrypts it on arrival to show who
  wrote. A relay that cannot deliver holds at most a handful of such
  notifications for a short while. Off by default. A build that names
  hypha's push relay sends notifications through it too, so they work without
  a relay of your own: it sees the same, plus your phone's IP address and the
  phone's own push identity, and because senders connect to it with a new key
  each time it cannot tell who notifies whom. No published build names one:
  hypha's own relay sends notifications only for vaults it was invited to
  sync, through that vault's connection.
- **Semantic search.** The language model ships inside the app; nothing is
  downloaded. The model runs entirely on your device; no note text is sent
  anywhere.
- **Web clipping.** If you save a web page, Hypha fetches that page, and may
  fetch images it references, from the sites that host them. When the page
  says what it is about (a film, a recipe, a book, a product, an event), Hypha
  reads that from the page itself and fills in the note's properties; for such
  a page it also fetches the page's main picture once, to use as the note's
  cover. No other site is asked for anything — details the page does not state
  stay empty.
  Some sites refuse every request that does not come from a web browser. When
  a site refuses Hypha that way, the Mac and PC apps open the page once more in
  a hidden browser window of their own: the page's scripts run and its
  pictures load (the site's check needs them), but it cannot use your camera,
  microphone, location or notifications or start a download, no video, audio,
  fonts or styles are loaded, and the cookies it sets are kept apart from the
  rest of Hypha and thrown away when Hypha quits.
- **Link previews in chat.** When you paste a link into the vault's chat, your
  device fetches the first part of that page to make the card (title,
  description, picture); the site sees your IP address, as visiting it would.
  The card then syncs with the message; the other devices fetch nothing.
- **External images, and web pages embedded in notes.** A note can point at an
  image on someone else's server, or embed a whole web page. Both are off by
  default, under Settings → Privacy: until you turn one on, or press
  the button on that particular image or page, nothing is requested. They are
  listed apart from everything above because they are the only ones that are
  not a single thing you asked for — loading them happens **every time the note
  is opened**, and notes arrive from the people you sync with, so what gets
  requested may be a site someone else chose. Turning either on tells the site
  your device's network address and when you opened the note; an embedded page
  additionally runs that site's own code on your device, inside a sandbox that
  cannot reach your notes, open windows, or use the camera, microphone or
  location.
- **Weather in daily notes.** A daily note can record its day's weather. To do
  that Hypha sends a position and a date to [Open-Meteo](https://open-meteo.com),
  a weather service, and nothing else — no identifier, no note text. The
  position is either a place you typed under Settings → General, or, if you
  allow it, your device's location reduced to about a kilometre before it is
  stored or sent. Nothing is sent until you have done one of those two things;
  the switch beside them turns the feature off. Open-Meteo sees your IP
  address, as any site you visit does.
- **A photo's place, on iPhone and iPad.** With "Note where I captured it" on,
  the place a photo was taken is given a name by Apple's geocoder, which is
  sent a position rounded to about a kilometre — when you open the photo's
  Info, and for a photo taken through Quick capture. With it off, nothing is
  sent and the place stays rounded coordinates.

## Permissions the app asks for

- **Local network** — to find and connect to your other devices on the same
  Wi-Fi. Declining it means local sync will not work; everything else does.
- **Camera** — only to scan the pairing code when you add a device.
- **Microphone / Photo library** — only when you choose to attach something.
- **Notifications** — when you first set a reminder, or turn on "Notify me
  about new messages" for a vault. Declining it means no reminder and no
  message notification is shown; everything else works.
- **Location** — only if you press *Use my location* under Settings → General,
  or turn on "Note where I captured it" on an iPhone or iPad, and only at
  reduced accuracy. It is used for the weather line in daily notes and for a
  photo's place name, and for nothing else. Declining it leaves everything else
  working; you can still type a place instead.

None of these send data anywhere except location, which goes to the weather
service and the geocoder described above. The rest are used to put data into
your vault.

## Children

Hypha is not directed at children and collects no data from anyone, including
children.

## Third parties

Hypha has no advertising, no attribution frameworks and no analytics
providers. The third parties it talks to on your behalf are the ones listed
above, each only for the feature named: the weather service and Apple's
geocoder (a coarse position), GitHub (update checks and release notes), the
DHT's entry nodes and the peers and relays of your vault (sync), the sites you
clip, preview or embed, and the storage you publish to. The developer receives
nothing, except through the beta relay service if you enrol in it.

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
