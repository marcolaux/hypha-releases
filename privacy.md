# Privacy Policy

**hypha**
Last updated: 14 October 2026

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
- contacts, calendar or health data;
- your location — with one exception you opt into, described under *Optional
  features* below: a coarse position, sent to a weather service and to no one
  else, never stored by the developer.

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
  Notes.
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
- **Semantic search.** If you enable it, a language model is downloaded once from
  its own source. The model then runs entirely on your device; no note text is
  sent anywhere.
- **Web clipping.** If you save a web page, Hypha fetches that page, and may
  fetch images it references, from the sites that host them. When the page
  says what it is about (a film, a recipe, a book, a product, an event), Hypha
  reads that from the page itself and fills in the note's properties; for such
  a page it also fetches the page's main picture once, to use as the note's
  cover. No other site is asked for anything — details the page does not state
  stay empty.
  Some sites refuse every request that does not come from a web browser. When
  a site refuses Hypha that way, the Mac and PC apps open the page once more in
  a hidden browser window of their own: the page's scripts run, but it cannot
  use your camera, microphone, location or notifications or start a download,
  no pictures, fonts or styles are loaded, and the cookies it sets are kept
  apart from the rest of Hypha and thrown away when Hypha quits. On iPhone and
  iPad, sharing a page from Safari also hands Hypha the page as Safari shows
  it; that copy stays on your device and is used only when Hypha's own fetch
  of the page is refused.
- **External images, and web pages embedded in notes.** A note can point at an
  image on someone else's server, or embed a whole web page. Both are off by
  default, under Settings → Global → Privacy: until you turn one on, or press
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
  position is either a place you typed under Settings → Notes, or, if you
  allow it, your device's location reduced to about a kilometre before it is
  stored or sent. Nothing is sent until you have done one of those two things;
  the switch beside them turns the feature off. Open-Meteo sees your IP
  address, as any site you visit does.

## Permissions the app asks for

- **Local network** — to find and connect to your other devices on the same
  Wi-Fi. Declining it means local sync will not work; everything else does.
- **Camera** — only to scan the pairing code when you add a device.
- **Microphone / Photo library** — only when you choose to attach something.
- **Notifications** — when you first set a reminder, or turn on "Notify me
  about new messages" for a vault. Declining it means no reminder and no
  message notification is shown; everything else works.
- **Location** — only if you press *Use my location* under Settings → Notes,
  and only at reduced accuracy. It is used for the weather line in daily notes
  and for nothing else. Declining it leaves everything else working; you can
  still type a place instead.

None of these send data anywhere except location, which is sent to the weather
service described above. The rest are used to put data into your vault.

## Children

Hypha is not directed at children and collects no data from anyone, including
children.

## Third parties

Hypha has no third-party SDKs, no advertising, no attribution frameworks and no
analytics providers. The one third party it talks to on your behalf is the
weather service above, if you use that feature; it receives a coarse position
and a date, and the developer receives nothing.

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
