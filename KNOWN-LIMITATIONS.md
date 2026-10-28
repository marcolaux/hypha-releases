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

**ONNX Runtime's own telemetry shipped on, since the 0.99.25 desktop and iPhone/iPad
builds.** Search by meaning runs a Microsoft embedding engine (ONNX Runtime), and its
official builds enable Microsoft's usage telemetry by default — hypha did not turn
it off until 2026-10-27. While a model session was loaded, those builds sent
technical events about the engine itself (model loads, timings, device facts) to
Microsoft's collector — on the desktop this was observed live, an upload request
in flight right after a session was created; on the iPhone it was found because
its uploader crashed the app on a locked phone. Note content never left the
device through it, and the desktop's earlier WASM engine (before 0.99.25) and
every Windows desktop build never carried it at all. It is now disabled at both
of the engine's switches, in the app and in every tool that runs the model.
Weather remains the only feature that sends anything off the device at your
request — this one did it without being asked, and no build after 0.99.30 does
it at all.

**Vault names are stored in the clear** in the local registry. This is needed for iOS so the share functionality lets the user choose a vault right in the share menu.

**There is no recovery for a forgotten passphrase.** None. Nobody can reset it,
including the author, because nobody else has anything to reset. This is the
direct cost of there being no server. What there is: a device that keeps the
vault's key in its keychain keeps the passphrase beside it, and Settings →
Security → Show passphrase reads it back. On a Mac and an iPhone that
read always asks the device owner first: Touch ID / Face ID, falling back to
the login password or the passcode. A Mac or iPhone that cannot ask at all
(no password, no passcode) refuses. **Windows, Linux and Android show it
without a prompt** — Electron has no OS prompt to show there, and the Android
spike's keychain bridge has no gate yet. Copy puts the words on the clipboard
for one minute: on a Mac marked concealed so clipboard managers skip them, on
an iPhone for this device only. The words leave the screen after a minute or
when the window loses focus. A device that never kept the key (the opt-in off,
a Linux desktop without a keyring) has nothing to show.

Keeping the words at all is the same bet Anytype makes (it keeps the recovery
phrase in the keychain on every platform). It adds little for someone who can
already read this device's keychain — the vault key sits next to it — but six
words are easy to photograph and open every device and backup until the
passphrase is changed. That is why the display is gated, not the storage.

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

**A relay address reaches a device only after it has synced once.** The list under
Settings → Sync → Relays travels inside the vault itself, so a device that has
just joined learns it the first time it meets another device over the internet
or your Wi-Fi — not before. A phone with neither cannot find the relay by
address. If a member device overwrites the list, devices that already had the
real one keep it, and an owner device writes it again when it next syncs; a
device that joins in between sees no relays until then. The Mac's background
sync of a vault you have not opened does not dial relays by address yet.

**An address a relay announces is checked only for the relay's key.** A relay
run with `--public-url` can put its address in the list by itself (see
Settings → Sync → Relays). Before the app adds it, an owner device checks that
the address answers with that relay's key, so a wrong address leads nowhere. But
nothing checks where the address points, so a relay you invited could name a
host that sees your devices' IP addresses when they dial it. Remove the entry to
stop that. An iPhone accepts the address only with a certificate it trusts.

**A relay's storage limit counts attachments only, and frees late.** A relay
run with quota groups limits the attachment files it keeps for a group of vaults;
the encrypted notes and messages it forwards are not counted. A file you delete
frees its space on the relay only once an owner device of the vault has synced
the deletion. An app older than this version that is refused for a small file
(one sent in a single piece, up to 16 MB) sends the whole file again every time
it connects; newer apps wait a day, or until the relay has room.

**A relay you reach by address learns your IP address.** Over the address the
relay sees which device's IP (or the proxy's) connected when, and which of its
vaults that device wants — never what is in it. Behind a proxy that the relay is not told to
trust (`--trust-proxy`), every device shares the proxy's address: at most 32 can
be in the middle of connecting at once, and someone who holds those slots open
delays the others by up to ten seconds.

**The enrolment service learns who you are to it, never what you write.** A
vault you enrol through hypha's relay stays end-to-end encrypted. The small
service behind the invite codes can see your key's public half, which vault
route tags and context ids it maps to, connection and byte volumes, and IP
addresses (the web server's own logs included) — never vault keys, note
content, or an email address (there is none).

**"Stop using" removes every relay on the service's host.** The enrolled
relay is told apart from your own relays by its address alone, so a relay you
run yourself on the same host as hypha's service is removed from this vault's
relay list with it — re-adding it by hand puts it back.

**Revoking a device is not instant everywhere.** Revoking is a row in the
vault's own device list, and it works by replicating: every device that receives
it refuses the revoked one from then on. A relay cannot act on it: the row
reaches the relay inside an encrypted envelope it stores and forwards without
being able to read. So a revoked device can still reach a relay you run, and
sync through it, until its own credential expires. That is 30
days at the outside, and usually much less. Your other devices refuse it
immediately. If you need the cut to be immediate, stop the relay (or
`hypha-peer leave` that vault on it) as well as revoking. A revoked **Owner**
device is the exception: its credential never expires, so for it you rotate
the owner key (below), which cuts it off a relay at once.

**Inviting a removed phone or computer again does not bring it back cleanly.** A
relay you removed and invite again comes back on its own, as a new device. A
phone or computer does not yet: the device that invites it lets it back in under
its old, revoked identity, and your other devices go on refusing it. To bring
one back, remove it from the vault on that device as well, and add it again as
a new device.

**A revoked owner device still holds a copy of the owner key — rotate it.**
Revoking a device that was added as an Owner takes away its place in the
device list, but the owner key itself is a copy it keeps, and with it the
device could still invite devices and sign for them. Settings → Sync →
Advanced → *Rotate owner key* gives the vault a new one: the record is signed by the old
key, the new key and the device that rotated, travels with the vault's data
and in every handshake, and every device checks that the rotating device is a
non-revoked Owner in its own device list before it follows. From then on the
old key invites nobody and signs nothing anyone honours. The dialog lists the
devices that keep their place; an unchecked device needs a new invite, every
checked Owner device is handed the new key when it next connects, and every
other device must meet an Owner device once to be renewed (until then it syncs
with Owner devices only). Revoke first, then rotate — the revoke dialog
offers both. What stays open, by design:

- *A relay follows whichever rotation reaches it first.* It cannot read the
  device list, so it cannot tell your device from the revoked one;
  `hypha-peer status` names the device that rotated. If that is a device you
  revoked, `leave` the vault on the relay and add it again with a fresh invite.
- *A device the revoked owner admitted before the rotation* stays in if you
  leave it checked — uncheck what you do not recognise.
- *Two rotations at once* (two of your own devices, or a revoked device
  racing yours) are a question the app does not answer on its own: each device
  shows both and asks you to keep one; revoking the device you do not trust on
  any Owner device settles it everywhere. While a device is asking, it stays
  on the previous key, which the revoked device still holds.
- *The notes themselves are not re-encrypted.* The vault key does not change
  with the owner key, so anything the revoked device already holds, or still
  obtains from a relay before that relay follows the rotation, it can read.

**A device that has not met an owner device for 30 days stops being admitted.**
Credentials are issued with a 30-day life, and only a device holding the owner
key renews them; meeting another member does not. So a phone that syncs only
with a laptop that is not an owner device will, after 30 days, be refused by
everything. This is not a lockout and nothing is lost: the next time it does
reach an owner device, that device renews it on the spot — even after the
credential has expired — and it resumes. The limit exists on purpose. It is what
makes revocation take effect on a device you can no longer reach to tell.

**Background sync of a vault you have not opened is Mac-only and needs its
key in the keychain.** With "Sync in the background" on
(Settings → Sync, on by default since 0.99.26), the Mac opens that vault when hypha starts,
with no window. It unlocks it from the keychain without asking, so while it
runs it holds the vault's keys exactly as an open, unlocked vault does
(`docs/DESKTOP-AT-REST.md` §8). What it does not do:

- A vault protected by Touch ID, or one whose key is not in the keychain, is
  not unlocked this way. It receives while locked instead (below), and syncs
  fully only while you have it unlocked.
- A vault that locks with no window open (its auto-lock delay after the last
  window closed, Lock in the menu bar, the Mac going to sleep) keeps
  receiving, still locked: what your other devices send is stored encrypted
  on disk and applied the next time you unlock it. The menu bar says
  "Locked — receiving", and a banner says only that the vault received changes
  — a locked vault cannot read what they are. While locked it sends nothing.
  What arrives this way: every change to notes, notebooks, tags and chat, and
  edits to the notes open on the sending device; the text of other notes
  catches up when you open them after unlocking. A vault that never synced on
  this Mac since the update does not receive while locked. The store holds at
  most 64 MB; beyond that the rest arrives after the unlock. A device you revoke
  on another device while this vault is locked can still deliver to it until
  you unlock it; what it sent is applied as any synced change is. The
  "received changes" banner can also appear when a device only re-sent
  something the vault already had (at most once every 30 minutes per vault).
- A window that sits at the unlock screen stops the receiving: the vault
  receives again once you close that window, and syncs fully once you unlock
  it there.
- A vault's background process that crashes, stops responding for three
  minutes with no window open, or fails with an error restarts by itself, after
  a growing pause; one that keeps failing stops and reads "Sync failed — open
  to retry". A process a window is using is never restarted behind it.
- A chat message that arrives while no window has the vault open shows who
  wrote it, never what. Messages that were already old when the Mac received
  them, for example after it slept, are summed up in one banner per vault, at
  most every 30 minutes per vault, even across a restart of the vault's
  background process. A message that was edited before this Mac received it
  gives no banner.
- Windows and Linux quit when the last window closes, so there is nothing to
  keep running there.
- **Message notifications on iPhone need a relay that forwards them.** With
  "Notify me about new messages" on for a vault, the phone registers with the
  relays that vault connects to; only a relay run with Apple's push credentials
  for the shipped app can forward a notification, and a self-hosted relay
  cannot (it needs our team's key). The notification shows who wrote and
  whether it was a message, a comment or a mention — never the text. One that
  arrives before the phone's first unlock after a restart, or that the phone
  already showed, reads only "New activity". A device revoked while the phone
  was away still verifies until the app next opens. A device removed from a
  vault can keep using a relay of that vault, for push as for sync, until its
  relay credential expires (up to 30 days): the relay is not told of the
  removal. hypha's own relay forwards notifications only for vaults it was
  invited to sync. The phone's queue of
  notifications it could not send is lost when the app is killed. Push has run
  on one iPhone, through hypha's relay; the rest of the checklist has not.
- **A mention in a note notifies the person you tag, with a delay.** When you
  type `@` and pick a person in a note, their devices get "… mentioned you in a
  note" (never the title) about 30 seconds after you stop typing, or when you
  leave the note or the app. A mention you delete or undo within that time
  sends nothing, and a pasted or dropped mention never sends. A mention in a
  note that has not been saved yet (its very first keystrokes) is not noticed.
  If you add the same mention on two of your devices at almost the same time,
  the person may be notified twice. Notes that stay on one device never notify
  anyone. An iPhone running an older version shows only "New activity".

---

**A relay that offers itself on your network is trusted exactly as much as one
you add by hand.** Since §4qz a relay run with `--advertise` announces itself
on the LAN and the vault's owner device asks you once. Saying yes gives that
relay the same owner-signed daemon credential a hand join gives: it stores and
forwards your ciphertext and sees the metadata every relay sees (note ids,
sizes, timings, device keys, your IP) — never your content. The only thing
that identifies the relay is the 96-bit fingerprint in the dialog; compare it
with what the relay's administrator published before you connect, because a
rogue device on the same network can advertise a relay of its own with a
convincing name. "Never for this relay" is remembered by that key on this
device. For the administrator: a relay that accepts joins from the network on
its own can have its slots occupied by anyone on that network who invents a
vault — each such vault is bounded by the default quota (attachment bytes; its
small `opaque.db` sits outside it, as for every vault) and dropped after a
week without a second device — a filter, not a wall: a squatter that also
connects a second device of its own keeps its slot — and `HYPHA_PEER_ADVERTISE_APPROVE=1` makes every
join wait for `hypha-peer approve`; advertise only on a network you own, since
behind a proxy or a VPC every source looks local. An older daemon that reads a
"held" entry treats it as a vault with missing secrets and does not serve it.

## Platforms

**macOS is Apple-silicon only.** No Intel build exists and none is planned.

**Windows and Linux builds are tested only occasionally.** They are built on
GitHub's runners for every release and are unsigned.

**macOS auto-update changed engines in 0.98.9 and has not yet been watched on a
client's Mac.** Until 0.98 the update was applied by Squirrel, which — when the
app folder was not writable by your account — restarted into the old version
without a word. Since 0.98.9 Sparkle applies it and asks for an administrator
password in that case instead. The switch itself, and the password prompt on a
standard account, have been proven on the developer's Mac only; a copy older
than 0.98.9 that came back on the same version after "updating" needs one fresh
install from the DMG.

**On the iPhone and iPad, the vault's "Reclaim storage" compaction is off**
(since the 2026-10-27 recovery pass), and Settings → Storage says so. The
compaction rewrites the whole vault in one go, in memory, with the app frozen;
it had never been run on the phone's storage before an iPhone vault came back
"database disk image is malformed" shortly after the offer. Whether the two are
connected is not known — the compaction has since been run on the same storage
stack in a headless browser without harm — but a phone has no automatic backup
to fall back on, so the offer stays off there until the safer shape (a copy
beside the vault, verified, then swapped) exists.

**Recovering a damaged vault on the phone is best-effort.** The start screen's
"Recover what is readable" copies every row SQLite can still read into a fresh
vault file and lists, per table, what it could not; a note whose row sat on a
damaged page is gone from that device, and nothing on the phone holds another
copy unless another device or a backup does. Search, previews and tasks are
rebuilt on the next start. The copy is only offered when SQLite's own check
passes on it.

**On the desktop, each vault runs in its own background process** (since
September 2026), and every window of that vault talks to it rather than opening
the vault itself. Search by meaning adds one more background process for the
whole app while it is indexing or answering; it quits after five idle minutes.
Activity Monitor or Task Manager therefore shows several hypha processes.

---

## Features that are present but incomplete

**An older build of Hypha shows your templates as ordinary notes.** Templates are now a kind of note rather than a note tagged "template", and an app from before that change does not know the kind: on it they appear in All Notes, in search, on the map and in the tasks list, and its Templates list is empty because the tag is gone. Update every device. A template made on an older build still arrives as a tagged note and is converted the next time the newer build syncs.

**An older build of Hypha cannot show note and person properties, rollups or formulas, and can misread a saved filter on
them.** A property that links to other notes or to people, a rollup and a formula are new: an app from before them shows
the property as "Empty" and never changes it, so nothing is lost. But a saved view that filters on such a property with
"is empty", "is not empty", "is" or "contains" is read by the older app as if the property were always empty, so that
view shows every note or none there. Update every device.

**Rollups do not count archived notes, and a note that cannot be opened stops them.** A rollup reads the notes in your
list; an archived one, one in the trash and a template are left out (its tooltip says how many). When a note's
properties cannot be read (the vault is locked, or a note's data is damaged), a rollup that might include it shows "—"
rather than a total that leaves it out. A rollup cannot add up its own value down a whole tree of notes (a
project's total over every level of sub-projects): a property that reads itself shows `#CYCLE!`, and a chain of more
than eight rollups and formulas reading one another shows `#NUM!`.

**A few Markdown constructs still paste as their raw text.** Footnotes (`[^1]`), headings underlined with
`===` or `---`, code indented by four spaces, and inline `$math$` are not converted when Markdown is
pasted or imported, and a `[[wiki link]]` pasted from another app becomes its plain text (there is no
note to point it at). Paste them into a code block, or retype the heading with `#`.

**The note map's Links view draws the links Hypha has recorded, which are not exactly the `[[links]]` in your notes.** A link added
only from a note's footer is drawn though it is not in the text, and a link you removed from the footer stays removed even if the
text still holds it. Links already in your notes are recorded once, in the background, the first time a vault is opened and
unlocked after the update, so a large vault fills in over a minute or so. Notes that are archived or in the trash are left out
of the map. A link you removed on one device can come back from another device that had not yet received the removal when it
recorded your notes' links, the same way opening a note that still contains the link would bring it back.

**Moving a table row or column while someone else is typing in it can lose their text.** Yjs has no "move": a moved row is
deleted and written again, so words a peer types into the row you are moving, in that same moment, are
lost. Rows you did not move keep their edits in the right place. Move a row when nobody else has the
note open, or let the edit land first.

**"Turn into" over a selection that starts in an item's sub-items converts that item's own line too.** When
a selection begins inside the sub-items of item A — not on A's own line — and runs on past A (into a later
item or the text below the list), A is converted as a whole, its line included, with its sub-items coming
along unchanged: a list item cannot be split between its line and its sub-items. Start the selection on
A's own line, or convert the sub-items on their own.

**Changing one item in the middle of a list can detach comments on the items after it.** Turning a list item
into a quote, heading or another kind of list splits the list in two, and under sync the half after the
cut is written anew, so a comment anchored in those later items loses its place and is shown with its
quoted text instead of a highlight. Comments on the items before the cut, and on the converted item's own
text when it stays in place, are kept.

**The table move keys can be taken by the system on Linux.** A table row or column moves with ⌘⌥⇧ and an
arrow (Ctrl+Alt+Shift on Windows and Linux). Several Linux desktops (GNOME, KDE) use Ctrl+Alt+Shift with an arrow to
move the window to another workspace, and the system gets the key first. The Table menu does the same moves.

**A device that has not been updated un-cancels a cancelled task when it edits it.** A cancelled task
(`- [-]`) is stored as an attribute that older versions do not know; an older device that types in that task
writes it back without it, and the task reads as open on every device. Update every device together.

**A device that has not been updated shows a task's priority as `!!`, not a chip.** A task's priority is the
`!` / `!!` / `!!!` at the end of its text, so nothing is lost on an older version — it just cannot draw or
set it, and a task whose text really ends in a lone `!` after a space reads as low priority on the new one.

**A device that has not been updated forgets a photo's date and place when it edits the file's Info.** An
older version that writes a picture's description (yours, or its own reader's) writes the file's info back
without the date and place, and they are gone on every device. Update every device together.

**Search by meaning on the phone needs the Mac updated first, or together.** This version rebuilds the
meaning index in a new form, and devices on different versions do not exchange it: a phone updated before
its Mac finds nothing by meaning until the Mac is updated and has rebuilt (it does so on its own, once).

**Who's here only knows about notes open in an editor.** A tab restored at
launch but never clicked, a tab pushed out of a pane's last twelve, and PDF,
attachment and search tabs do not show who is reading them. At "Only where I'm
typing" and "Invisible", another person's cursor can take up to about 15
seconds to appear on your screen, because your device announces nothing and
theirs only re-sends on its regular renewal. Someone who reaches you only
through a relay and leaves without quitting (a phone put away, a crash) stays
listed for up to 35 seconds. A device that has not updated shows by the name it
announces, always as viewing, never as editing. Inside a vault, any member's
device could claim another member's identity in its presence, appearing as
that person, or claim one of your devices and so be hidden from you as if it
were your own. Everyone in a vault already holds every note's key, so this is
the vault's existing trust, not a new hole.

**Desktop notifications need the app running.** A Mac, Windows or Linux
computer gets no notification while hypha is quit: notifications that reach a
closed app go through Apple to iPhones only. A comment notifies you on the
desktop only on a note you have taken part in (you commented there or were
mentioned there) or in a thread you wrote in; the iPhone's push still announces
every comment in the vault, and its per-vault switch is not yet split into
chat, mentions and comments.

**On the phone, search by meaning needs a desktop.** The phone never builds
the meaning index itself: it reads the index a desktop in the same vault
built and synced, and only turns your question into a vector on the device. A
vault that lives only on phones has full-text search but no search by meaning,
and a note written on the phone is found by meaning once a desktop has seen
it. The language model makes the app download about 135 MB larger on iPhone
and iPad (about 127 MB on the desktop).

**Picture descriptions need Apple Intelligence.** A picture's one-sentence
description comes from the on-device model of macOS or iOS 27, and the text in
a picture from Apple's Vision. Windows and Linux read neither — they read a
PDF's text only — and show a description another of your devices wrote. A
scanned PDF has no text layer, so nothing is read out of it.

**A long PDF is found by meaning through its first ~12 pages, by words
throughout.** Search by meaning embeds a file's description and the first
~5,800 words of its text; the rest of a long document is still found by its
words. Like notes, files are embedded by a desktop and synced to the phone.

**Word forms are found by simple endings, not by grammar.** "Word forms &
parts" removes a common ending from what you type (-n, -en, -e, -er, -s and a
few more) and looks for words that begin with or contain what is left. So
"kartoffeln" finds "Kartoffel", "Kartoffelpüree" and "Süßkartoffel". An
irregular form is not found: "ging" does not find "gehen". A short word can
match more than it should: "Mütter" also finds "Mutti". Only a word's 64 most
common longer forms are searched as word parts. A search that uses AND, OR,
NOT or NEAR, or has more than 12 words, shows exact matches only.

**A photo's place has a name only once an iPhone or iPad has seen it, with
location on.** The place a photo was taken is named by Apple's geocoder, sent
a position rounded to about a kilometre, when you open the photo's Info on an
iPhone or iPad with "Note where I captured it" on; the name then syncs. With
it off, nothing is sent and the place shows as rounded coordinates, as it does
on the Mac, Windows and Linux until a phone has named it. A photo picked with "Take Photo" in the file picker keeps no
place; Quick capture's camera does, with "Note where I captured it" on.

**The summary of the day needs Apple Intelligence and an open app.** It runs
on macOS or iOS 27 with Apple Intelligence turned on; elsewhere the setting is
hidden. The iPhone cannot write it in the background — the notification is
armed ahead, and the summary is written when you tap it and unlock. The Mac
writes it at the set time while hypha is running and the vault unlocked, and the
phone then finds it synced; a daily note that was never opened on the Mac is
left for the click. A note counts for the day it was LAST edited, so summarising
an earlier day misses a note that was edited again since. "Done today" knows
only boxes ticked after this update. The model sometimes words a note
clumsily, or leaves a note out of its paragraph — every note is still listed and
linked below it. Not yet tried on a phone.

**On the iPhone and iPad, a page that blocks automated visitors cannot be
clipped from a share.** A share from Safari hands Hypha the page's address,
and Hypha downloads the page itself; a site that refuses anything but a real
browser (IMDb, for one) then gives it nothing, and the link goes in as a link.
On the Mac the same page is clipped through a render window that runs the
site's challenge the way a browser does. Taking
the page Safari already shows was tried and does not work on iOS 27.2.

**A site that refuses even your own browser cannot be clipped.** The Mac's
render window runs a challenged page's own script, but it does not click a
checkbox for you, and some sites refuse a whole network outright — every
browser on it, yours included. (allrecipes.com did exactly this on
2026-10-25: the page asked every visitor on this network to wait forever.)
Hypha says so — "this site only shows its pages to a web browser" — instead of
clipping the challenge page. The images of a page that DID come through a
challenge stay linked online: Hypha's own image download is the one request the
site still refuses.

**Quick capture on iPhone has not been tried on a phone yet.** The Action
button, the Controls and the Home Screen quick actions are built and checked on
a Mac only. The Action button runs one action, so it gets one of the three
(recording is the suggested one), and a recording stops with a tap or a second
press — iOS tells an app nothing about the button being let go. A photo becomes a Product note
only on iOS 27 with Apple Intelligence; elsewhere it lands in the daily note as
a picture. Product details are what the photo shows (name, brand, a printed
price, the barcode) — nothing is looked up online. The place name needs a
connection; offline the note gets rough coordinates. The Controls always open
the vault that is active.

**Siri understands "Note in hypha" in English and German only.** Siri matches
a phrase only in its own language, and hypha ships those two. The dictated text
is held in memory until the app is open and unlocked; if iOS ends the app before
then, the note is lost.

**A recording is transcribed in one language.** It is your device's language,
or the one picked under Settings → Language → Speech language. Speech in
another language comes back as nonsense words in that language; nothing detects
the language you spoke.

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
