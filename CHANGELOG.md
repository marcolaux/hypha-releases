# Changelog

All notable changes to Hypha are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- **The always-on relay is now one command to run.** Hypha syncs your devices
  directly, which means both have to be awake at the same time — write on your
  phone with the laptop shut and the laptop gets it whenever you next open it.
  A relay is a third peer that is always awake, so that stops being a wait. It
  is published as a container image with a compose file and a filled-in example
  configuration on the releases page, so setting one up on a spare machine is
  four commands rather than a build from source. It holds **ciphertext only**:
  it joins your vault with no ability to read anything in it, and a stolen relay
  disk yields sealed blobs. It is a convenience, not a backup, and it is
  entirely optional — nothing about syncing changes if you never run one.

### Changed
- **The releases page no longer offers an iOS download.** It briefly carried an
  `.ipa` that nobody could install, including the author: from 0.13.0 the iPhone
  build is packaged in the format Apple accepts for TestFlight, which iOS
  refuses to side-load at all. It was there to make the checksums file complete
  and it only ever looked like a download that worked. iPhone installs come
  through TestFlight; the checksums file now covers exactly what is published,
  so verifying a download no longer fails on a file that was never there.
- **What the phone runs its networking on changed, and it has now been tested
  on a phone.** The peer-to-peer stack lives in a separate embedded runtime that
  had to be swapped from one JavaScript engine to another for this release —
  Apple will not distribute a build containing the old one. Sync between a phone
  and a laptop on the same Wi-Fi is confirmed working on the new engine. Syncing
  over the internet rather than a shared network, attachment transfer, and how
  the phone behaves over hours of use are not yet re-tested on it;
  `KNOWN-LIMITATIONS.md` says so plainly.

### Fixed
- **The test suite was failing at random, and none of it was the app.** The
  headless browser driving the phone tests — the Chrome installed on the build
  machine — quits by itself about thirty seconds after it starts, silently and
  with no error anywhere. Every test running longer than that died at whichever
  step happened to be underway, wearing whatever error fitted, so one cause
  looked like a series of unrelated bugs in the app's own screens. Three
  attempts at building this release died that way before it was identified. The
  tests now run against a pinned browser that does not update itself underneath
  them.
- **A test had been checking the wrong place for months.** An earlier change
  moved every "done" message in Settings out of a line at the foot of the
  section and into a dialog, because on a phone that line was several screens
  below the button you pressed. The test that checks backup and restore was
  still reading the old spot, so it reported that restoring a backup printed no
  confirmation — the confirmation was there, in the dialog, and nothing had run
  the test since the change.

## [0.13.0] - 2026-08-21

**This is the first build of hypha that anyone other than its author can
install.** Every version before it was a tag in a repository — built on one
machine, never signed for distribution, never uploaded anywhere. macOS comes as
a notarized `.dmg` with a working update feed; the phone comes through
TestFlight. Read
[Known limitations](https://github.com/marcolaux/hypha-releases/blob/main/KNOWN-LIMITATIONS.md)
before you put anything in it you would be upset to lose, and take your own
backups. The three that matter most: there is **no recovery for a forgotten
passphrase**, a backup file still carries the vault credential, and the
cryptography has not been independently audited. Sync between two desktops
across the internet has never been run by anyone, and neither has an auto-update
from one installed copy to the next — if you are the first to try either, saying
what happened is the single most useful thing you can do with this build.

### Added
- **Link to a note that does not exist yet, and Hypha writes it for you.** Type
  `@` or `[[` in a note, keep typing a title nothing matches, and the picker now
  offers "Create “…”" as its last row. The new note is not blank of context: it
  inherits the tags, the notebooks and the colour of the note you linked from,
  so a thought you spun out of a project note is already filed under that
  project. It is a one-shot copy at the moment of creation — retagging the
  original later does not reach it, because the two are separate notes from that
  point on. Picking an existing note is unchanged, and a title that already
  exists is never offered for creation.
- **Tags can have icons, like notebooks do.** Right-click a tag in the sidebar →
  "Set icon…", pick from the full icon set, and the `#` becomes whatever you
  chose; "Remove icon" puts the `#` back. Works on the phone too, where the
  picker is now sized for a finger. A pinned notebook or tag in your Shortcuts
  also shows its icon now — until now it showed the generic glyph, so the same
  notebook could appear under two different icons in one sidebar.
- **Colours can be recoloured.** Right-click a colour in the sidebar and there is
  now a "Change color…" entry alongside Rename — the same picker used when you
  create one, opened on the colour you clicked, with the preset swatches and a
  hex field. Until now a colour's swatch was fixed at the moment it was created:
  the menu could rename it and delete it, and that was all.
- **Archive and Trash select like every other list.** Shift-click a range,
  cmd-click to add and remove individual rows — the same as the notes list.
  Right-clicking inside the selection acts on the whole set, so you can unarchive
  or restore twenty notes with one menu and answer one confirmation instead of
  twenty. Right-clicking a row outside the selection still acts on just that row.
- **Hypha now asks before leaving a file behind.** Take a picture or a document
  out of a note, and if no other note is using it you get a dialog offering to
  delete it too, with a preview of what you are about to lose. The same question
  comes up when you delete a note out of the trash, when you delete several at
  once, and when you empty the trash — asked **once**, listing every file that
  would be left with nothing pointing at it, with Keep all and Delete all
  alongside the per-file choice. Keep is always the default and nothing is
  pre-ticked. Files you do delete go to the attachment trash, so this is not a
  decision you can get badly wrong in a hurry. If Hypha cannot read one of your
  notes at that moment — a locked vault, a note still arriving from another
  device — it says nothing and deletes nothing, because a note it cannot open
  might be the one still using the file.
- **A setting for downloading attachments over cellular, on by default.** Your
  phone has always pulled the full attachment for every file in the vault the
  moment it heard about it, whatever network it was on. That is often what you
  want, so it stays the default — but it was never a choice you could see or
  make. Sync settings on the phone now carries "Download attachments over
  cellular" underneath "Download attachments automatically". Turn it off and
  attachments wait for Wi-Fi: notes, notebooks, tags and note text still sync in
  full over cellular, and tapping an attachment still downloads it right then,
  because that is you asking for it. Walking back onto Wi-Fi picks up
  everything that waited, without reopening the app. A personal hotspot counts
  as cellular — it is somebody's data plan too. The toggle is not shown on the
  desktop, which has no way to tell whether the network it is on is metered.
- **Search on the phone, from any screen.** Tap the title at the top of any
  screen and it becomes a search field. It searches the *text inside* your
  notes, not just their titles — which the phone could not do at all before, and
  which the desktop has always had in its title bar. The command palette comes
  with it, so anything you can do from a menu you can now type the name of.
  While the field has focus a row of chips appears: Notes, Commands, Tags,
  Notebooks and Tabs, plus Archive, Trash, Reminders and Web Notes. The chips
  are there so you never have to reach the symbol keyboard — typing `>` for
  commands, `#` for tags, `@` for notebooks or `:` for open tabs still works
  exactly as it does on the desktop.
- **You can see where a drag will land.** Drag anything over a note — a word,
  a picture, a file from Finder — and an accent-coloured line shows the exact
  spot it will be inserted, following the theme in light and dark. The editor
  had no such indicator at all: it was switched off years ago on the grounds
  that the list-drag extension drew its own, and that extension has never drawn
  anything.
- **Double-click a picture to open it.** It opens as a preview beside the note,
  in a pane split off to the right, so the picture and the note it belongs to
  are on screen together. The attachment chip has behaved this way for a while;
  a picture did nothing at all. "Open in new tab" in the right-click menu now
  opens the same way, instead of replacing the note in the pane you were
  reading. Opening the same file twice reuses the pane it is already in.
- **Pictures can be resized.** Hover a picture in a note and drag any of its
  four corners: the width follows the pointer, the proportions are kept, and it
  will not grow wider than the column it sits in. Double-click a corner to give
  it its natural size back. The size is stored with the note, so it survives a
  reload and reaches your other devices like any other part of the note. Until
  now a picture was always painted at whatever size it happened to be, with no
  way to change it.

### Changed
- **Three test gates were failing and had stopped being read.** One pinned the
  editor's drop indicator as *disabled* — the state a comment claimed was
  deliberate and which actually left notes with no drop marker at all, fixed in
  this same release; the gate was holding the old broken shape in place. One
  matched an editor handler by an exact signature that had since gained a
  parameter, so it went red on a change that did not touch what it guards. The
  third was reporting a real defect nobody had looked at. All three now pass,
  and the two brittle ones gained a self-check that fails loudly if they ever
  start reading the wrong thing rather than quietly passing.
- **Settings tells you what happened, where you can see it.** Backing up,
  importing, restoring, rebuilding the search index, purging vector storage,
  saving a publishing target, changing your passphrase, filing older attachments
  — all of these used to answer in a small line at the bottom of the section. On
  a phone that is several screens below the button you pressed, so the button
  looked like it had done nothing. The answer now comes up as a dialog you
  dismiss, on the desktop and on the phone alike. What was never an answer to a
  click stays where it was: progress lines, the updater's state, the sync status
  block, and the "these two passwords differ" kind of message, which now sits
  beside the password fields it is about instead of at the foot of the section.
- **The picture in a note's list row moved to the right.** It used to sit on the
  left under the title, which made every row with a picture taller than the rows
  around it and shifted the text of those rows sideways. It now sits on the
  trailing edge beside the title and the preview text — the same place it has
  always been on the phone — so more notes fit on screen and the rows line up.
- **Archive and Trash open a note beside the list instead of pushing the list
  around.** Clicking a row used to unfold its text underneath it like an
  accordion, so opening a second note shoved the first one's rows down the
  screen and a long note buried everything below it. Both screens now look like
  the notes screen: the list on the left, the note on the right, read-only, with
  its title at the top and a close button. Clicking another row replaces what is
  shown rather than opening a second thing — there is one pane, never a stack of
  tabs. The list column is the same width as the one on the notes screen and
  moves with it, so switching between them no longer shifts the layout.
- **The search box under each list is gone; the title above it does the job.**
  Notes, Archive, Trash, Reminders and Web Notes each carried their own search
  box that only filtered the rows already on screen, matching titles but never
  the text inside a note. Searching from the title is strictly better on the
  notes list, and the Archive, Trash, Reminders and Web Notes chips cover the
  four lists global search cannot reach on its own — an archived or deleted note
  is deliberately excluded from ordinary search results. Each list gets a row of
  screen back.
- **Split-pane and detached-window commands no longer appear on the phone.**
  Five commands — split right, split down, close pane, cycle pane, detach pane —
  were only ever hidden there because the phone had no command palette to run
  them from. Now that it does, they are hidden properly: a phone has no split
  panes and no second window, and running one would have left an editor pane you
  could neither see nor close.
- **Faint text is readable now, on every theme.** Placeholder text — including
  the passphrase fields on the very first screen — was far below the
  accessibility standard on all ten built-in themes, in the worst case almost
  invisible. Muted text and some accent button labels were under it too. All of
  them now meet WCAG AA, lifted just far enough to get there and no further, so
  the themes still look like themselves. On the two light Monokai themes, accent
  button labels change from white to near-black; white was genuinely unreadable
  there.
- **Backups no longer hand out your tag, notebook and reminder names in the
  clear.** A backup was only ever encrypting your *notes*. Everything else —
  tag names, notebook names, reminder titles and descriptions, settings values,
  attachment filenames and sizes — sat in the file as plain text, including in
  a backup taken while the vault was locked. Since a backup is the one file
  you're told to put in Dropbox or iCloud, that was the wrong place for it.
  Backups now seal all of it, and still work while locked. Restoring is
  unchanged: on this machine it just works, and on a fresh install your
  passphrase opens it.
  **Older backups still restore** — nothing you already have becomes unreadable.
- **The note map is no longer written for whoever built it.** The one cramped
  toolbar row is now a panel down the left, laid out like the app's settings:
  headings, and a sentence under each control saying what it actually does. The
  two grouping methods lost their textbook names — they are "Natural groups" and
  "Fixed number" now, with a line explaining that the first finds however many
  groups exist and leaves loners out, and the second splits everything into
  exactly the number you ask for whether or not it fits. The technical names are
  still there, in the explanation, for when you want them. Seven settings that
  existed in the code and were reachable from nowhere now have controls: showing
  and hiding notes and colours, the smallest group size, and which of the four
  kinds of connecting line get drawn — turning off "Similar meaning" alone
  clears most of the thicket. The explanations sit behind an ⓘ next to each
  label rather than printed under every control, so the panel is a list of
  settings again instead of a page of prose, and the active grouping button now
  takes your accent colour — in the muted grey it used to wear it read as
  disabled rather than as the one that is on. Hovering an ⓘ shows its
  explanation and clicking one keeps it up until you dismiss it, so the text
  does not vanish the moment you reach for the scrollbar. There is a legend for the group colours, the map
  says "no groups at this setting" instead of showing you an empty cloud, and it
  offers a button that loosens the dial for you. Crowded areas no longer stack
  five titles into one unreadable smear: labels that would collide are dropped
  until you zoom in, and whatever you hover is always readable.
- **The map remembers how you like to look at each vault.** Every option you
  set is kept per vault on this machine and restored the next time you open the
  map, instead of snapping back to the defaults on every open. It does not sync
  — it is how *you* read *this* vault on *this* computer.
- **The default grouping distance was too strict to group anything.** On a real
  32-note vault the map came back with one group and everything else loose,
  which reads as "there is no structure in your notes" when it actually meant
  "this dial is set too tight". Loosened, the ceiling raised, and — more to the
  point — that state now explains itself rather than looking like an answer.

- **Open a note from the map and its own note map opens with it.** Clicking
  through to a note used to drop you into a plain editor, which is a dead end
  when you arrived by following connections; the note's sidebar now comes up on
  its local map so you can keep going. It only affects the note you opened — it
  does not change what the sidebar shows on every note you open afterwards.

### Fixed
- **The "delete this file too?" dialog opened behind the keyboard on iOS.** The
  question Hypha asks when you remove the last note using a picture is a
  full-screen dialog, and it had not been marked as one — so on a phone it laid
  itself out inside a box the keyboard was sitting on top of. Every other dialog
  carries that mark; this one, added in this release, did not.
- **A setting's name and its explanation ran together as one line.** In
  Appearance, "Stock themes" and the sentence explaining what resetting them
  does rendered as a single run-on line with no break between them — the label
  and its description were two inline boxes in a plain container, where every
  other row in Settings stacks them. It was wrong on the desktop too; the phone
  is only where it got noticed. The themes picker around it also got the touch
  treatment its controls never had: the toolbar stacks instead of wrapping its
  buttons up into the text above them, the search field no longer makes iOS zoom
  the page when you tap it, and the card grid adapts to the width it has instead
  of being locked at two columns.
- **Some panels had no spacing between their sections.** A layout helper built
  its gap size by string interpolation, which Tailwind cannot see when it scans
  the source, so four of the nine possible spacings silently compiled to
  nothing at all. Sync settings, Language settings and the note map's new
  options panel all had sections sitting flush against each other — which looks
  like a deliberately tight design rather than a missing stylesheet rule, and so
  had gone unnoticed.
- **The note map redrew itself differently every time you opened it.** The same
  vault, unchanged, produced a different picture on each open: clusters swapped
  colours, cluster numbers moved around, and nudging the K or density slider
  re-rolled the whole thing again. K-Means picked its starting centroids at
  random, and both clusterers numbered clusters in the order they happened to
  meet them — an order that tracked the notes list, which re-sorts as you edit.
  Opening the map fast rather than slow also raced the colour list, and a map
  built without the colour nodes projects every other node somewhere else. All
  four are pinned now: same vault, same map, and a given cluster keeps its
  colour between redraws. Adding or removing notes still rearranges things —
  the map is fitted to whatever is in it — and so does opening the map while
  the semantic index is still filling in, which is what the banner at the top
  is telling you.
- **Pasting text with an `@` in it hijacked the note-link picker, and could
  swallow the paste.** Paste a paragraph that happens to contain an `@` and the
  picker opened over it, treating everything from that `@` to the end of what
  you pasted as one long search. Pressing Enter then picked a note and deleted
  that entire stretch — most of the paste, gone, replaced by a note title.
  Pasting or dropping text no longer opens any of the three pickers: `@` for
  notes, `#` for tags and `/` for commands now open when you *type* the trigger,
  which is when you meant it. Typing a title with a space in it — `@meeting
  notes` — still works exactly as it did.
- **Note links no longer break code open.** Typing `@` inside a code block, or
  inside an inline `code` span, opened the note picker — and picking a note from
  inside a `code` span split the span in two and left the title sitting outside
  it, unlinked. Neither the picker nor the link is offered inside code now.
- **Closing a tab now takes you back to the tab you came from.** It used to jump
  to the first tab in the strip — not the one you were last reading, and not
  even a neighbour — so closing a file you had opened to check something threw
  you to the far end of the strip. Closing keeps walking back through the tabs
  you actually used, and closing a background tab leaves you where you are.
  Moving a tab to another pane reveals the last-used tab in the pane it left.
  After a restart the pane returns to the tab it was showing, and from there
  falls back to the neighbour on the left.
- **Dragging a picture inside a note moved nothing — it made a second copy that
  would not open.** Dropping it left the original where it was and inserted a
  duplicate, and right-clicking that duplicate to open it answered "no in-app
  preview for this file type". Neither was really about the drop: the editor
  never treated the drag as a drag at all, so the browser did it instead and
  pasted the picture as web markup, which carries no record of which file it is.
  Now dragging a picture, an attachment or an audio/video player **inside** a
  note moves it, and dragging one **into another open note** copies it there —
  pointing at the same file, not a second copy of it, and leaving the first note
  untouched. Dragging a file in from Finder or a picture in from a web page
  still adds it as a new attachment.
- **Tab in a note jumped out of the editor.** Pressing Tab anywhere that was not
  a list moved the focus to the notebook picker at the foot of the window
  instead of indenting, which in the middle of writing is the last thing it
  should do. Tab now indents and Shift-Tab outdents — in a paragraph, in a
  heading, across a multi-line selection and inside a code block — and lists,
  tables and code blocks keep the behaviour they already had. Tab in a note you
  cannot edit still moves the focus, as it should.
- **The editor collapsed runs of spaces.** Two spaces typed in a note rendered
  as one, and a line could not be indented at all: the stylesheet ProseMirror
  requires for whitespace was never loaded, so the editor ran at the browser
  default. Spaces now render as typed, on the desktop and the phone.
- **Settings on the phone.** The attachment list gave four buttons about half of
  every row and truncated the filename to a few characters — the one part that
  says which file it is; the buttons now take their own line and the name gets
  the width. A device row in Sync no longer squeezes the fingerprint you compare
  against your other device's screen. "Stock themes" and its description
  rendered as one run-on line (on the desktop too). The theme picker's search
  box, filter pills and import buttons wrapped into the text above them, and
  tapping that search box zoomed the whole page and did not zoom back. Section
  headings no longer have their summary line jammed in beside them.
- **Deleting an attachment asked with a system alert.** Every other destructive
  question in the app is hypha's own dialog; this one was the browser's, which
  on the phone means an iOS alert dropped into the middle of a sheet. It also
  means the sheet could not say "Delete" on the button that deletes.
- **A dialog with nothing to cancel offered Cancel on the phone**, and a
  three-way question — keep a file, move it to the trash, or delete it for good
  — silently lost its middle answer there while the desktop offered all three.
- **One day could end up with two daily notes — again.** This was reported fixed
  once already, and it came back the same week, because the previous fix guarded
  the two ways a daily note gets made against each other rather than removing the
  reason they could disagree. A daily note was recognised by its title and by a
  reserved "daily" tag, which meant deciding "does this day already have a note?"
  took several separate steps, and a `@today` link and the Daily Notes screen
  could each get part-way through that decision before the other finished — and
  both make a note. Which day a note belongs to is now written on the note
  itself, and looking the day up and creating it are one indivisible step, so
  there is no longer a gap for a second note to appear in. Three things follow
  from that, all of them things you could previously lose a note to: renaming a
  daily note no longer stops it being that day's note, duplicating one no longer
  puts a second note on the same day, and two devices that each made a note for
  the same day offline now agree on which one the day opens. Daily notes you
  already have are adopted as they are the first time you open them — nothing is
  moved, rewritten, or renamed. If a day in your vault already has two notes,
  both are still there and the older one is the one the day opens; the other is
  now an ordinary note you can merge in and delete.
- **The phone stopped reconnecting after you left Wi-Fi.** Walk out of the house
  — or just switch Wi-Fi off — and the phone would drop its link to the desktop
  and never pick it up again over cellular, until it was back on the same
  network. **Two separate faults produced that one symptom, and the first fix
  only removed one of them** — so if you read this entry earlier in the beta, it
  claimed more than it delivered.

  **On the phone, Hypha was refusing to reconnect.** It treated iOS's Low Data
  Mode or Low Power Mode on a cellular connection as "stop syncing entirely",
  and applied that rule at the worst possible moment, tearing down the working
  connection it had just been using rather than merely declining to open a new
  one. Low Data Mode and Low Power Mode no longer stop the phone syncing: it
  stays connected over cellular and your notes, notebooks, tags and note text
  keep arriving. How much data Hypha spends is decided by the two settings that
  were always meant to decide it — "Download attachments automatically" and
  "Download attachments over cellular" — and iOS's economy modes do not silently
  overrule what you set there. Nothing changes when there is genuinely no network
  at all: with no route off the device, Hypha still does not spend battery
  bootstrapping a connection that cannot complete.

  **At the other end, the rescue was being turned away.** The device the phone
  was trying to reach — a desktop, or the relay daemon — kept its Wi-Fi
  connection to the phone in its list of live connections after the phone had
  gone. A phone that walks out of range says no goodbye, so there was nothing to
  notice. But when the phone then found its way back over cellular, that arriving
  connection was compared against the one already listed, judged a redundant
  second copy of a phone that was already connected, and closed — and the phone
  was told to stop trying, which it obeyed. Every rescue attempt was refused the
  same way, so the phone could not get back in until the program at the other end
  was restarted. A connection arriving by a different route is now treated as
  what it is: evidence that the old one is dead. If the existing connection has
  shown no sign of life for 45 seconds, the new one replaces it instead of being
  turned away. And "stop trying" now lasts 30 seconds rather than until the
  program is restarted, so if this ever goes wrong again it costs half a minute.

  **What this does not yet fix**, so you can set your expectations by it: leaving
  Wi-Fi is still not a smooth handover. The other end can hold a dead connection
  for longer than it should — we know that happens and do not yet know why — and
  the phone rebuilds its cellular connection from scratch, which takes minutes
  rather than seconds. What has changed is that the reconnection is no longer
  refused, and that recovering from it no longer needs anything restarted. Give
  it a few minutes before assuming it has not worked.
- **Long-press menus in the phone's sidebar now open.** Holding a row in the
  sidebar was supposed to give you the same menu a right-click gives on the
  desktop — rename, delete, pin as a shortcut. It never did, on any row: the
  press did nothing and iOS took the gesture for selecting text instead.
  Notebooks and tags had no menu at all, and the shortcut and colour rows had
  one that could not be reached. Holding any sidebar row now opens its menu, and
  the colour menu has gained **Change color…** alongside Rename.
- **Links in notes: you can put the cursor in them, and on the phone they open
  at all.** Clicking a link went straight to opening it, which meant there was no
  way to place the text cursor inside link text to edit the words — the click was
  always taken as "follow this". On the phone the same click did the opposite and
  nothing happened at all: it tried to open the link in a way an iOS web view
  silently discards, so tapping a link in a note had no effect whatsoever.
  Clicking or tapping a link now puts the cursor exactly where you clicked and
  offers a small panel beside the link with **Open**, **Edit link…** and **Remove
  link**. Opening is a choice you make rather than something that happens to you,
  and it now routes properly on both platforms — a link to another note opens
  that note, a file opens in the system, and a web address opens your browser.
  Right-clicking a link on the desktop offers the same three actions.
- **Renaming a colour no longer wipes it out.** Renaming a colour in the sidebar
  made it look deleted: it lost its dot and the notes carrying it lost their
  tint. The colour was still there — the rename was saving the new name *and an
  empty colour* over it, because it only ever sent the name, and the part it did
  not send was blanked rather than left alone. It also quietly reset the
  colour's creation date. Renaming now changes the name and nothing else.
- **The rename box for a colour accepts more than one character.** Typing in it
  re-selected everything after each keystroke, so every new character replaced
  the one before it and you could never get past a single letter.
- **The phone no longer quits itself while you have it locked.** Lock the screen
  with Hypha open, come back half a minute later, and you were on the home screen
  with the app starting from scratch — losing whatever you had on screen. When
  the app went to the background it asked its networking engine to pause, and the
  pause takes out a permit from iOS that is only handed back once the engine has
  told iOS it has fully stopped. Hypha's engine never told it: a peer-to-peer
  engine is always listening, and nothing was closing its connections. So the
  permit was never handed back, and iOS terminates any app that holds one for
  about thirty seconds. Hypha now closes those connections when you lock the
  phone and opens them again when you come back, which is what lets iOS put the
  app away properly. Syncing picks up on its own after the unlock, about four
  seconds later, because the phone has to announce itself to your other devices
  again before they can find it. Confirmed on an iPhone: locked, left for a
  minute, unlocked, and still exactly where it was.
- **Opening a note no longer counts as editing it.** Simply opening a note wrote
  it back to disk a moment later, exactly as though you had typed in it — which
  bumped it up a list sorted by Modified, and sent the write out to your other
  devices. Reading a note is not changing it, and it now leaves no trace. The
  same care applies in the other direction: when another device's edit arrives
  and Hypha renders it into a note you happen to have open, that is the other
  device's edit and it keeps the other device's time. Only your own typing
  counts as your own edit — including when both land in the same second, where
  your keystroke wins.
- **A note you edit now stays at the top of the list, on every device.** Sorting
  by Modified, editing a note moved it to the top — and then it slid back to
  where it had been. Reopening the app put it back at the old position for good,
  and other devices never moved it at all: the phone showed the note exactly
  where it had been before you typed. The cause was that nothing was writing
  down *when* a note was last edited. Saving a note updated its text but left
  its modified date at the moment the note was created, so the jump to the top
  was only ever a guess your own screen was making, and the first thing that
  re-read the note from disk — a sync arriving from another device, or simply
  reopening the app — undid it. Editing a note's text or renaming it now records
  the time, so the order is the same everywhere and survives a restart. Notes
  you have not edited since this release keep the date they had; each one moves
  into its right place the next time you edit it. Pinning, favouriting or
  archiving still does not count as editing, and receiving someone else's edit
  keeps *their* time rather than stamping your own.
- **An open Settings panel now notices what your other devices did.** With
  Settings → Sync open, a device joining or being revoked somewhere else did not
  appear until you restarted the app — and the same was true of Settings →
  Attachments when a file was deleted on another device. Both panels stay open
  once you have visited them, so leaving the screen and coming back was not a
  way out of it either. Both now update as soon as a sync lands. Sync itself is
  unchanged and no slower: the device list is re-read on its own, without the
  keychain lookups that reading your room identity needs.
- **Deleting a note now shows up on the Trash screen straight away.** If the
  Trash screen was already open — in a second window, or beside the list you
  deleted from — the deleted note did not appear there until you navigated away
  and back, and a second window kept showing the note in All Notes as though
  nothing had happened. The Archive screen was taught this in the previous
  release and the Trash was not, so the same action behaved differently
  depending on which of the two screens you were looking at. Both now behave the
  same way, in every window.
- **A big sync no longer skips the Archive screen.** When a device came back
  after a while offline, or joined a vault for the first time, it took a
  shortcut and rebuilt the notes list in one go — and that shortcut stepped past
  the Archive refresh. So the sync that was most likely to be carrying archived
  notes was the one that left the Archive screen showing the old list. The same
  now applies when a single note cannot be read during a sync: the lists are
  refreshed rather than assumed unchanged.
- **The phone's log now says how much memory the app was holding when it went
  away.** iOS can kill a backgrounded app for several unrelated reasons that all
  look the same from the outside — you unlock the phone and you are on the home
  screen. The app now records its memory footprint and remaining headroom as the
  last thing it does before going to the background, and again when it comes
  back, so the two cases can be told apart from a device log instead of guessed
  at. Diagnostics only; nothing about the app changes.
- **Typing on the phone no longer drags the whole app around.** Tapping into a
  note brought the keyboard up and left the app with two scrollers: the note
  scrolled, and so did everything behind it, sliding the nav bar off the top of
  the screen while the formatting toolbar disappeared behind the keyboard. The
  cause was a single measurement. The app worked out how much of the screen the
  keyboard covered by comparing two viewport heights, and on iOS 27 one of those
  heights now shrinks with the keyboard — so the sum came out *negative*, which
  reads as "no keyboard at all". Nothing made room, and iOS scrolled the entire
  page up to keep the cursor visible. The app now asks iOS how tall the keyboard
  is instead of inferring it, and puts the page back where it belongs once the
  room has been made.
- **A device that was refused now says so, instead of pretending to sync.** If
  you joined a vault with an invite link that had already been used, or that had
  expired, or from a device the owner had since revoked, the join appeared to
  work: the vault was registered, your passphrase opened it, and the app looked
  entirely normal. It just never synced, forever, and said nothing — because the
  owner's refusal was a silent disconnect, which looks exactly like the owner
  simply being out of range. The only record of the real reason was a log line on
  the *other* person's machine. Three changes fix it. The refusal now travels to
  the refused device and says which of the reasons it was. Sync status shows
  "Not admitted" — ranked above "offline" and "no peers", because no amount of
  waiting or better Wi-Fi will repair it — with the reason in words and, on the
  phone, a button to remove the vault. And re-using your *own* invite link is now
  caught at the moment you paste it, before the vault is registered at all.
- **Daily Notes on the phone opens today's note.** Tapping Daily Notes in the
  sidebar landed on the day timeline, which is a date picker whose answer is the
  same every day — two taps to reach the note you wanted. It now opens today
  directly, and the timeline stays one back-swipe away for any other day. Tapping
  a day in that timeline also works properly now: picking the already-selected
  date, or any day that has no note yet, used to do nothing visible at all.
- **Reordering the sidebar shortcuts now reaches your other devices.** Dragging
  a pinned notebook, tag or favourite note into a different position was only
  ever stored on the machine you did it on — the order lived in local browser
  storage, where no sync path could reach it — so every other device kept the
  old arrangement forever. It is now stored with the rest of your vault and
  travels like anything else; resetting the order travels too. An order you
  already made on this device is adopted on first launch rather than thrown
  away, unless another device has since set one, which wins.
- **Settings changes no longer wait for an unrelated edit before syncing.** The
  same underlying fault held up everything stored as a setting: the sidebar
  colour order, date and time formats, the toolbar layout, your publishing
  target and profile. Each was saved correctly and then sat there, because
  nothing told the sync engine there was anything new to send — it went out
  only when some *other* change, like editing a note, happened to push it. That
  made it look intermittent rather than broken. Settings now announce
  themselves like every other change, and cross in about a second.
- **A selected image shows it.** Clicking an image in a note gave you no sign it
  was selected — the video player has always drawn a ring when you pick it, and
  the image, which is all picture and has no caret to read, had nothing at all.
  It now draws the same ring, on the picture's own edge rather than the full
  width of the line, and on the placeholder if the image is still arriving.
- **The window buttons on macOS sit on the same line as the title-bar icons.**
  The red/yellow/green buttons were drawn two pixels above the row of icons
  beside them, which is exactly the kind of misalignment you see without being
  able to name it. They are now centred on the icons. The sidebar toggle also
  gets room to breathe: it sat about six pixels from the green button and now
  sits eighteen, so it no longer reads as crowding the window controls.
- **Every theme is on the page; the theme list no longer scrolls inside a
  scrolling page.** Settings → Appearance capped the theme grid at a little over
  half the window height and gave it its own scrollbar, so you were scrolling a
  small box inside a scrolling pane and the wheel went to whichever of the two
  the pointer happened to be over. The grid now grows to its full height and the
  settings pane scrolls it, like every other section.
- **Tapping a phone search result opens that note, at the line it found.** On
  the phone, picking a result from the new title-bar search moved to the editor
  but left whatever note was already open sitting there — and picking a command,
  a tag or a notebook ran the wrong one, whichever happened to sit at that
  position in the unfiltered list. The overlay emptied the result list before it
  read which row you had touched. It now reads the row first and clears
  afterwards; the layer still disappears the instant you tap. A picked note
  opens and scrolls to the match, as it does on the desktop.
- **Checklists put the text next to the checkbox again.** Every row in a
  checklist rendered its checkbox on its own line with the text underneath it,
  in the editor on the desktop and on the phone. The stylesheet had a block of
  checklist rules that had never matched anything: it was written for a custom
  checklist component that was never built, while the rows are actually drawn by
  the stock editor's own markup. The rows are now laid out as a line — checkbox,
  gap, text — with the text wrapping under itself rather than under the box,
  nested checklists indented, and a ticked row dimmed and struck through.
- **The "Checklist" list type lost everything typed into it.** Choosing
  *Checklist* (as opposed to *Simple checklist*) produced a list that showed no
  rows at all, and the text in it was dropped on the way to storage — a
  checklist saved by an earlier version came back empty, or as an empty bullet
  list. Both halves are fixed — the rows render, and they survive both saving
  and re-opening. Text that an earlier version already wrote away cannot be
  brought back; the *Simple checklist* type was never affected.
- **A note someone else trashed or archived turned your typing into duplicate
  "Untitled" notes.** With a note open on this device and the same note trashed
  or archived on another, the open editor quietly stopped being bound to it and
  became a *draft*: every few seconds of typing forked a brand-new "Untitled"
  note holding the whole body, and none of the edits reached the real note. The
  tab now stays bound to the note, turns read-only, and says which it is — "In
  trash" or "Archived" — with a one-click Restore or Unarchive. The tab is
  deliberately not closed: closing it under the cursor would discard whatever
  was being written, which is the same loss from the other side.

- **A note trashed on another device stayed in All Notes.** The sync path
  decided a note was still live by asking whether the database still returned
  it — but a trashed note *is* still returned (the row is a tombstone, not an
  absence), so a peer's trash was read as an ordinary edit and the note was put
  straight back in the list. Trashing now replicates to the list on both the
  sync path and the between-windows path; previously neither carried it.

- **macOS packaging never ran: the notarization block was written in the previous
  electron-builder's syntax.** electron-builder 26 made `mac.notarize` a plain
  boolean; the `{ teamId: … }` object it replaced is not deprecated there, it
  fails schema validation, so every `--mac` leg died in the config validator
  before packaging started. It has been that way since notarization was wired,
  because the next full release run is the first thing to read the block. The
  team id moves to the environment, which is where 26 looks for it.

- **The release build failed at the iOS bridge-frame gate.** The user's
  diagnostic-logging flag (`__hyphaLoggingEnabled`, shipped in 0.12.0) is the
  fifth non-bridge user script the shell injects into all frames, alongside the
  `crypto.randomUUID` shim, the CPU probe and the two debug flags — but it was
  never added to the gate's allowlist, so `release:local` refused every build
  after it landed. It registers no handler and exposes no native capability;
  only the allowlist was out of date, not the injection. The shell's own comment
  said "four" and now says five, and names the file that has to agree.

- **"Back up now" worked once and then seemed to do nothing.** On the phone the
  first manual backup landed and the second changed nothing at all: the button
  stayed enabled, tapping it produced no file and no message. Three things in
  Backup & Export were each enough to cause that on their own, and all three are
  fixed. The section never caught a failure, so when the platform refused to
  write — an unreachable folder, a payload it turned down — the refusal vanished
  and the button simply re-enabled itself; it now says what went wrong, in the
  platform's own words. Every outcome, including "Backup saved", was printed at
  the very bottom of the section, several screens below the button that caused
  it, so on a phone it may as well not have been there; each message now appears
  beside the control it belongs to. And the format picker (notes only / with
  attachments) reset itself to "choose a format" every time you left the section
  and came back, which on the phone is every time — so the second backup asked
  for a format again, in a message you could not see. It remembers your choice
  now.

## [0.12.0] - 2026-08-19

### Changed
- **Hypha's licence has changed, and Hypha is no longer open source.** It is now
  *source available* under the Hypha Source Available License 1.0. In plain
  terms: you may use Hypha for anything, including at work; you may read it,
  change it, and share it and your changes with anyone, free of charge. You may
  not charge for it, sell it, bundle it into something you charge for, or defeat
  the mechanism that decides which features an install has. Those rights stay
  with the author.

  Two things prompted it. Releases now go out as binaries while the source stays
  private, and the AGPL promised anyone holding a binary a copy of the source
  they could not actually get. And there is going to be a paid tier, which the
  AGPL cannot carry and which its network clause makes incompatible with the App
  Store outright.

  **This does not reach back.** Versions 0.1.0 through 0.11.0 were released under
  the AGPL and those grants stand for those versions permanently. Nothing you
  already have is withdrawn.

- **The brand is written `hypha`, in lowercase, and the App Store listing is
  called "hypha notes".** The name "Hypha" was already reserved by someone else
  on the App Store, and the listing name has to be globally unique — so the
  store entry carries the longer name while the app on your home screen is just
  **hypha**. Every place the app writes its own name now uses the lowercase
  form. Nothing about your notes, files or settings is affected.

- **The iOS app has a new identifier, so it installs as a new app rather than an
  update, and it has to re-join your other devices.** It changed from
  `app.hypha.mobile` to `app.miniml.hypha.ios`, under a new Apple developer
  account. Two consequences, both unavoidable: iOS treats a different identifier
  as a different app, so the old one stays on the phone until you delete it and
  its notes do not come across; and the app's keychain entry is scoped to the
  developer account, so the new install cannot read the old vault key. Pair the
  phone with a desktop again and let it sync. This is done now, before the beta,
  precisely so it never has to happen to anyone but us.

- **The desktop app also has a new identifier** (`org.hypha.desktop` →
  `app.miniml.hypha.desktop`). Your notes are untouched — macOS and Windows
  treat the old and new data directories as the same place — but macOS sees a
  new app and will ask for **Local Network** permission again the first time you
  sync.

- **Automatic backups are a desktop feature now; on iPhone, backups happen when
  you ask for them.** The schedule was never going to work on a phone and the
  way it failed was the bad way — quietly. iOS suspends an app shortly after you
  leave it, and a suspended app runs no timers, so "back up daily" only ever
  fired if you happened to open Hypha and leave it open. You set a guarantee and
  got a coincidence.

  Nothing else about backups on iPhone changes. "Back up now" writes exactly the
  same backup the desktop does, in both formats, to a folder you pick; both
  restore paths work; the backup folder and the number of backups to keep are
  still yours to set, because they apply to the backups you take by hand too.
  The Backup screen now says why the schedule is gone rather than just dropping
  it.

- **A new app icon on both platforms**, drawn from the redrawn `hy` monogram.

- **macOS 12 (Monterey) is now the declared minimum.** It was always the real
  floor, inherited from Electron; it just was not written down, so the installer
  would happily install onto a Mac the app then crashed on at launch.

- **"Full offline mode" is gone; in its place is "Download attachments
  automatically", and unlike its predecessor it does something.** The old
  checkbox's value reached a parameter no syncer ever read — there was no
  consumer of it anywhere, on either host, for its whole life — while the
  behaviour it claimed to control ran unconditionally: every connection swept
  the whole vault for attachments, so a phone joining pulled down every file in
  it. The new setting is on by default and genuinely gates that sweep. Turn it
  off and notes still sync in full; an attachment is fetched when you open it,
  because "do not download files I did not ask for" is the policy and opening
  one is you asking. Serving other devices, and deleting attachments you have
  removed, are unaffected either way.

### Added
- **macOS builds can now be signed and notarized.** With a Developer ID
  certificate in place, Gatekeeper stops demanding right-click → Open on first
  launch, the app keeps a stable identity across updates — so the Local Network
  permission is no longer re-requested every time — and auto-update can replace
  the bundle at all, which it previously could not.

- **Documentation for people who want to install Hypha, rather than build it.**
  There was none: an install guide covering the right-click → Open step macOS
  currently needs and how to check what you downloaded; a security page saying
  precisely what is encrypted and what is not; a known-limitations page
  collecting, in one place, everything that is missing, unproven or deliberately
  absent; and a privacy policy. The honest headline from the security page is
  that only *notes* are encrypted — tag and notebook names, reminder text and
  attachment filenames are stored in the clear, including inside a backup file.
- **A list of the third-party components Hypha includes and their licences.**
  This was owed before and had never been written.

- **Type `@today` in a note to link to that day's daily note.** The `@` menu that
  links to another note now understands `@today`, `@tomorrow` and `@yesterday`,
  and offers the matching daily note — creating it if it does not exist yet.
  `@date` offers today plus a date picker, so any other day is two keystrokes
  away. The rows appear as soon as the word is recognisable, so `@tod` is enough.

- **Archive, Trash and Web Notes look like the notes list now, and their rows
  open.** All three drew their own cramped list with actions that only appeared
  on hover, and in Archive and Web Notes clicking a row did nothing at all. They
  use the same row as the notes list, and clicking one opens it: read-only in
  Archive and Trash, in the normal editor in Web Notes.

### Fixed
- **On iPhone, the on-screen keyboard covered the bottom of the note you were
  typing in.** iOS does not shrink a web page's layout for the keyboard, so the
  lower part of every screen — the note's text above all — was laid out behind
  it. Text appeared where you could not see it, and the only way it came back
  was the whole app sliding around under your finger. The app now ends exactly
  where the keyboard begins, and the line you are typing scrolls back into view
  when the keyboard opens over it.
- **The `/` menu in the editor listed a code word beside every entry.** Typing
  `/` at the start of a line opens a menu of formatting actions, and each row was
  printing the internal *name* of its icon as text — "remove-formatting Clear
  formatting", "list-ordered Numbered list". It now draws the icon, as the
  toolbar always did.

- **Sync settings put the master switch below everything it switches off.** The
  "Enable sync" and "Full offline mode" options sat at the bottom, under the
  whole list of paired devices. With sync off, every row above them is inert —
  and you only found the switch that explained it after scrolling past all of
  them. The options now come first.

- **An archived note did not show up in Archive until you restarted the app.**
  Archiving removed the note from All Notes immediately and reached your other
  devices immediately, but the Archive screen itself only rebuilt its list when
  you navigated to it fresh — so if you were already looking at it, or looking at
  a second window, the note simply was not there. It appears at once now, whether
  the archiving happened here, in another window, or on another device.

- **Archived notes were fully editable.** "Archived" meant the note left the main
  list and nothing more: a tab left open when you archived, or a link to an
  archived note, gave you an ordinary editor that saved and synced every
  keystroke. Archived notes are read-only now, like notes in the trash, with an
  Unarchive button where the formatting toolbar used to be.
- **A note could end up with its own text twice, permanently, on every device.**
  A note's text lives in two places, and a note opened before its text had
  arrived from your other device would convert the copy it had into the shared
  document — producing a second copy of something that was already there. It is
  data, not a drawing mistake: reopening the note or restarting the app kept it.
  Three doors led to it and all three are shut. Opening a note in the seconds
  after launch, before the app has finished re-connecting to your devices, no
  longer counts as "nobody has this text". Two devices converting the same note
  at the same time now produce a result that merges to one copy rather than two.
  And a note whose text exists on no device — a web clip, an import, a daily
  note made from a link — no longer sits waiting four seconds for a copy that
  is never coming: the app now recognises when every device has answered "I do
  not have it" and opens straight away.

- **One day could end up with two daily notes.** The daily note reached from
  the `/date` menu and the one on the Daily Notes screen were found by two
  different routes that could not see each other's work, and each remembered
  its answer. A daily note created in another window, or arriving from another
  device, read as "there isn't one" — so a second was made, and afterwards the
  link took you to one note while the list opened the other.

- **Sync could stop between two paired devices until you restarted the one that
  was refused.** After the device that owns the vault restarted, the other one
  went on presenting the invitation it had already used up, rather than the
  credential it had since been issued — so every reconnection was refused, for
  ever, and nothing but relaunching the refused device cleared it. Two related
  faults made the failure loud as well as permanent: a refused device was
  re-dialled several times a second rather than held off, and the hold-off that
  was added first only covered the side doing the refusing, leaving the refused
  device dialling back in at the same rate.

- **A packaged build still printed diagnostic logs.** The switch in Settings →
  Updates → Logging only ever reached the app's main window. The three other
  places that log — the desktop app's background process, the iPhone app's
  native shell, and the two components that draw note content — had no switch
  at all, so a released build wrote diagnostics regardless, and on iPhone those
  lines were kept in the system log on the device. All four now follow the one
  setting, which stays off in a released build; errors still print always.

- **The *What's New* window showed a stale, built-in copy of the release notes.**
  It fetches them from a public repository, and that repository was empty — no
  branches at all — so the fetch had been failing for every installed copy of
  Hypha since the source moved private. Nothing surfaced the failure: the app
  quietly fell back to the notes baked in at build time, which is exactly why it
  went unnoticed. The repository now carries the notes, and the fetch works.

### Removed
- **The "check for new versions" setting, which never checked anything.** The
  setting existed, defaulted to on, and promised a daily check — but the code
  that would have performed it had never been written, so turning it off changed
  nothing and leaving it on got nothing. Updating still works as it always did;
  only the setting that misdescribed it is gone.

### Tooling / Dependencies
- **Release credentials can live in a gitignored `.env`.** A signed and uploaded
  release needs six App Store Connect and notarization variables, and a shell
  export is lost the moment the terminal closes — discovering that after a
  20-minute build is the failure this prevents. `.env.example` documents every
  key with no values. A variable already set in the environment always wins, so
  a stale line in the file cannot silently beat what was just typed.

- **The version bump now cuts the changelog, and the public copies have a sync
  step.** Bumping a version left the notes for it under `[Unreleased]`, which
  the *What's New* window skips — so a new version would have appeared in the
  app with nothing under it. The bump now cuts the section under the new version
  number and refuses outright when there is nothing to cut. Separately, there is
  now one command that syncs the public copies of the changelog and the privacy
  policy, and a release checks them against it before it builds.

## [0.11.0] - 2026-08-18

### Added
- **A way to find out what an extra open vault costs.** Nothing on the desktop
  has ever been measured — every power instrument this project has is for the
  iPhone — while on the desktop each open vault quietly runs its own network
  stack. There is now an opt-in probe that reports, every thirty seconds, what
  each vault is holding and what each process is using, so the question can be
  answered with a number instead of a guess. It is off unless asked for and
  changes nothing about how the app behaves; `docs/DESKTOP-COST-RUN.md` is the
  procedure, including the rule for when the answer is "this costs less than we
  can measure, leave it alone".

### Fixed
- **Leaving the house stopped sync until you restarted the desktop app.** With a
  phone and a computer paired on the same Wi-Fi, walking out with the phone left
  the two unable to reach each other over the internet — the phone showed "no
  peers" indefinitely, and quitting and reopening the desktop app was the only
  thing that brought sync back. Force-quitting the app on the phone did nothing,
  because the stuck side was the computer.

  Three separate faults had to line up, and all three are fixed:

  - **Nothing ever noticed a device had left.** A phone that walks out of Wi-Fi
    range sends no goodbye of any kind, so the computer held the connection open
    forever, kept reporting the phone as connected, and — worse — went on
    refusing its attempts to reconnect over the internet, because as far as it
    knew it already had it. Both devices now probe a quiet connection and let go
    of one that has stopped answering.
  - **The phone kept using a network connection that no longer existed.** When
    the phone moved from Wi-Fi to cellular, the internet sync channel carried on
    using the network address it had on the old network. It is now rebuilt when
    the network changes — without the expensive full restart that an earlier
    version of this repair did once a minute and that cost a great deal of
    battery out of coverage.
  - **The pause was never lifted.** While two devices are on the same Wi-Fi they
    deliberately stop chasing each other over the internet, and that pause was
    only ever lifted by the local connection closing cleanly — which is exactly
    what does not happen when someone walks away. It is now also lifted whenever
    the network changes or a device has no peers at all, and a failed attempt to
    lift it is retried rather than lost.

  The phone's own log now says which of these is happening, in a release build
  and not only a debug one.
- **An incoming connection that failed at the wrong moment could take the
  desktop app down with it.** Connections over the internet spent the first
  moments of their life with no error handling attached, and a connection reset
  in that window — which is exactly what a peer changing network produces — was
  an unhandled crash rather than a dropped connection.

## [0.10.1] - 2026-08-18

### Added
- **Hypha has an icon.** Until now the desktop app showed Electron's generic
  icon in the Dock, the app switcher and every file dialog, and the iPhone build
  had none at all. Both now carry the handwritten *hy* mark. The two are drawn
  differently on purpose: macOS icons supply their own rounded shape, while
  iPhone icons must fill the square and let the system round them.

### Changed
- **The screen you see before your vault exists now names its fields.** The
  passphrase boxes on the first-run screen were labelled only by the grey hint
  text inside them — which vanishes the moment you type, is the faintest text in
  every theme, and is not a name a screen reader can announce. On the create
  screen that meant two identical unlabelled password boxes. Each field is now
  properly named. Nothing moves and nothing looks different; the names are there
  for assistive technology and for the moment the hint disappears.

  The hint text's low contrast is a separate, wider issue that has not been
  changed here, because it is an appearance decision across all ten themes.
- **"What's New" and the update check point somewhere they can be read.** Both
  pointed at a private location, so the release-notes fetch and the link to a
  release both failed silently for everyone; the window quietly fell back to the
  notes built into the app, which is why this was not visible. They now point at
  the public releases location. Until that location is populated the update
  check still finds nothing — it is not yet a working updater, it is a working
  address.

### Security
- **A web page embedded in a note could reach into the app on your iPhone.** A
  note can hold an embedded web page, and notes arrive from the people you sync
  with — so the page inside your note may be someone else's website. On the
  phone, that page could talk to the app's own connections into iOS: reading,
  writing and deleting files in the folder you picked for Hypha, making network
  requests from your phone, opening its network connections, posting
  notifications that looked like they came from Hypha, clearing reminders you
  had set, and writing into the phone's diagnostic log. Your keys were never
  reachable this way — they were already protected separately, and that
  protection is what everything else has now been brought up to. Every one of
  those connections now answers Hypha's own screen and refuses anything else.
  Nothing changes about how you use Hypha, and embedded pages still work exactly
  as before; they simply cannot talk to the app any more.

  That limit is now closed. The second half of the check — the one confirming a
  request came from Hypha's own address — used to let a request through if the
  phone declined to say where it came from, because refusing those without
  knowing what the phone actually reports could have made the app go silent
  everywhere at once and look like a freeze. A run on a real phone answered it:
  the phone does name Hypha's own address, so the allowance was covering a case
  that does not happen, and it is gone. Both halves of the check are now strict.
  Both were also watched turning something away on a real phone, rather than
  only being reasoned about.
- **Your search terms and the names of files you opened were kept in plain text
  on your iPhone too.** The same problem fixed on the computer in 0.10.0 was
  still there on the phone: the record of your open tabs held the exact text you
  last typed into search, the real filename of any attachment you had open, and
  a fingerprint of that file's contents — unencrypted, in the app's own files,
  which is exactly what a computer you have trusted can copy off the phone.
  Those details are now removed before anything is written. A phone that already
  holds the old record does not have to wait for you to change anything: it is
  rewritten the next time Hypha opens. Which notes were open, and how you had
  the screen split, are still recorded — those are not the vault's contents.
- **The app's own screen could have been replaced by another web page on
  iPhone.** Nothing was known to be able to do this, and that is the point: what
  kept it from happening was three unrelated details of how links, windows and
  pop-ups happen to be set up, none of them written down as a rule and any of
  them changeable by accident. The rule is now written down and enforced —
  Hypha's screen may only ever load Hypha, and anything else is refused. It also
  means the check added above, the one that makes each connection into iOS
  answer only Hypha's own screen, now has something behind it rather than being
  the only line. Embedded pages inside notes are unaffected and still work
  exactly as before. Not yet confirmed on a real phone.
- **Every reminder you had set was sitting in the iPhone's own notification
  store, with its title, months ahead of time.** When you set a reminder, the
  phone has to be told about it in advance — that is the only way it can alert
  you while Hypha is closed. It was told the note's title and description, and
  it keeps that text from the moment the reminder is set until it fires, in a
  place that is not part of Hypha's own protected files: outside what the app
  encrypts, included in the diagnostic reports iOS can be asked to produce, and
  on the lock screen of a phone set to show previews — which is how phones come
  out of the box. A reminder now tells the phone only that Hypha wants you at
  that time. It alerts exactly when it did before, and tapping it still opens
  the note it belongs to.

  The cost — the alert no longer says *which* note — is now yours to choose.
  **Settings → Notifications → "Show reminder details in notifications"** turns
  the title and description back on, on the phone and on the computer alike. It
  starts off, and it is set per device: a phone you keep private and a laptop at
  work can answer differently, and turning it on in one place does not turn it
  on everywhere.

  Worth knowing before you turn it on, because the switch cannot say it: on the
  phone this is not a smaller version of the old behaviour, it is the old
  behaviour by choice. The phone still has to be told about reminders in
  advance, so with details on, the text of every reminder you have coming sits
  in the phone's notification store until each one fires. Turning the setting
  back off clears it from the ones already waiting. On computers the text only
  ever reaches the system once a reminder has actually gone off, so the same
  setting costs less there — and the computer no longer writes the note's title
  into its own log file when a reminder fires, which it did regardless of this
  setting.
- **Joining a vault left an invisible, empty leftover vault behind every time,
  and a mistyped passphrase left the app pointing at a vault you had never
  opened.** When you add a vault, Hypha has to prepare one before it can ask
  whether you are making a new one or joining someone else's. If you joined, that
  prepared one was abandoned — an empty encrypted database and a key in the
  Keychain, never listed anywhere, so nothing in the app could ever clean it up.
  One per join, accumulating. Worse, getting the passphrase wrong on a join
  returned you to an empty screen that now believed you were in the vault you had
  just failed to open. Both are fixed: what a window prepares is now tracked and
  erased if you do not use it, and nothing is pointed at a vault until its
  passphrase has proved it is yours. One case is left and is named in the code —
  on the desktop, closing the "Add a vault" window instead of finishing still
  strands the prepared vault.

### Fixed
- **A file that had finished transferring to your phone was reported as never
  having arrived.** A 64 MB attachment reached the device, was stored, and took
  up its 60 MB — and every attempt to open it answered "this attachment's file
  hasn't reached this device yet". The transfer said it worked and the app said
  the file was missing, about the same file, at the same moment.

  The cause: when two of your devices add the same file independently, each
  locks it with its own key, so the same file has two legitimate encrypted
  forms and each is stored under its own name. The part that receives a file
  accepted either name. The part that reads one only ever asked for one of
  them. When your phone received the copy the *other* device had made, the
  reader was asking for a name nothing on the disk had. Nothing was lost and
  nothing was corrupt — the file was simply invisible to the app holding it.

  It now looks for the file under every name it could legitimately have,
  including one left by a copy you have since deleted while another note still
  uses it. Attachments in this state on your device become readable again the
  moment you update; nothing needs re-syncing, and nothing is re-downloaded.
  The app also now records how many files were in this state, so the size of it
  is known rather than guessed.
- **An attachment inside a note could not be opened on iPhone.** The file chip
  in a note's body responded only to a double-click, and on iOS a double-tap
  inside text is how the system selects a word — so the tap never reached the
  app and the chip did nothing at all, while still showing the pointer that
  says it can be clicked. Tapping it once now opens the file.

  Behind that, opening it would not have worked either: the chip asked the app
  to split the editor into two side-by-side panes and put the file in the new
  one — something the phone has no way to display. So the file would have
  opened into a pane that is never drawn, which is a worse outcome than nothing
  happening. Both halves are fixed together, and on a phone the file now opens
  in place. On desktop nothing changes: double-click still opens the file in a
  split pane.

## [0.10.0] - 2026-08-18

### Security
- **Adding a photo to a note left a full-size copy of it, GPS and all, sitting
  in the app's files on the phone.** Not a thumbnail and not encrypted — the
  original image, under its own filename, with everything the camera recorded in
  it: the model of phone, the date and time, and where you were standing. It
  stayed there after the photo was in the note. This was found by looking at a
  real phone rather than at the code, and it could not have been found any other
  way: the copy is made by the system's own photo picker, not by Hypha, so
  nothing in Hypha's own files mentions it. It is now cleared away, along with
  anything else the picker leaves behind. One honest limit: the copy still
  exists for up to an hour, because deleting it sooner risks deleting it while
  the picker is still reading it — which would break adding photos altogether.
- **Your search terms, and the names of files you opened, were kept in plain
  text on your computer.** The file that remembers your open tabs also
  remembered the exact text you last typed into search, the real filename of any
  attachment you had open, and a fingerprint of that file's contents. None of it
  was encrypted, and it survived locking the vault — so a vault you had locked
  still told anyone with the file what you had been looking for. It is now
  sealed with the same protection as the rest of your keys, and where a computer
  offers no keyring it is written with those details removed rather than not
  written at all.
- **Opening an attachment in another app left the decrypted file where other
  people using the computer could read it.** Hypha writes the file out so the
  other app can open it. That file, and the folder holding it, were readable by
  every account on the machine — and on Linux the folder was the shared system
  temp folder, so its contents could simply be listed by name. Both are now
  private to you, and they are cleaned up when Hypha starts and when it quits,
  instead of only the next time you opened something.
- **The folder holding your attachments was readable by other accounts on the
  computer, and its filenames give away what is in it.** The files themselves
  are encrypted and reveal nothing when opened — but each is named after a
  fingerprint of its contents, so being able to *list* the folder answers "does
  this person have this exact file". The same was true of the sync daemon's copy
  and of its saved passphrase. All are now private.
- **The list of your vaults' names was readable by other accounts too**, and is
  now private. It stays unencrypted on purpose: it has to be readable before any
  vault is unlocked, or you could not choose which one to open.
- **Your notes were readable in the phone's own files, with no key needed at
  all; the database on the phone is now encrypted.** Moving the keys into the
  Keychain (below) was the smaller half of this problem. The search index the
  phone builds so it can find your notes quickly held the **title and the full
  text** of every note you had opened, in plain readable form, and it sat in a
  database file with no encryption on it. So did the list previews, and the
  material that protects your vault passphrase against guessing. Anyone who
  could copy the app's files off the phone — which is a normal thing to be able
  to do from a computer you have trusted — could read your notes without needing
  any key, any passphrase, or the Keychain.

  The phone's database is now encrypted as a whole, with a key held by the iOS
  Keychain. Nothing readable is left in the file: not note text, not titles, not
  even the marks that identify it as a database. This is what the desktop has
  always done, and the phone now matches it.

  **This is not an automatic upgrade**, for the same reason as the keys below:
  a vault created before this change cannot be opened by this version, and it is
  not converted in place — converting the only copy of your notes is exactly the
  operation you do not want going wrong halfway. The app says so plainly instead
  of failing obscurely. Remove the vault on the phone and re-join it from your
  computer.

  Files the app creates on the phone are also now marked with iOS's strongest
  protection class, so they stay unreadable while the phone is locked. That is
  worth having, but it is not the fix — the encryption is.
- **The iPhone kept your vault's keys in plain text; they now live in the iOS
  Keychain.** Everything that protects a vault on the phone — the key that
  decrypts your notes, this device's identity, the owner key that proves who may
  invite others, the shared sync secret, the membership credential and any
  stored invite — was written to ordinary browser storage inside the app, with
  no encryption of any kind. Anyone who could reach the app's files, including
  anyone who could plug the phone into a trusted computer, could read them.

  They are now held by iOS itself, in the Keychain, marked so they are readable
  only while the phone is unlocked and so they never travel to another device in
  a backup. The desktop has always done this with the operating system's
  keychain; the phone now matches it.

  Two supporting changes came with it. The app used to claim its storage was
  encrypted whether or not it was, and the "stay unlocked on this device" option
  trusted that claim — so on the phone it cached your vault key into plain text
  by default. That option now switches itself off wherever there is no real
  protected storage to use. And an invite link waiting to be opened — which
  carries enough to join a vault — was being kept in plain storage until it was
  used, or forever if it never was; it is now protected the same way and expires
  after thirty minutes.

  **This is not an automatic upgrade.** No attempt is made to move the old
  cleartext keys into the Keychain: doing that safely is delicate, and doing it
  *unsafely* can silently split a vault's chain of trust. They are deleted
  instead. Remove the vault on the phone and re-join it from an invite on your
  computer.

- **Correction: a backup file is not fully encrypted, and never was.** Hypha's
  own notes said a backup "is always encrypted", on the grounds that it carries
  the database's own already-encrypted contents. That is true of your **notes** —
  their titles and their text are sealed in the file and cannot be read without
  your passphrase. It is not true of everything else. Your tag names, your
  notebook names, your **reminders — both the title and the description you
  wrote** — your settings, and the **filenames, types and sizes of your
  attachments** are all in a backup file in plain readable form.

  Nothing about this changed in this release. The claim was wrong, we found it,
  and we are telling you rather than quietly correcting a comment — because you
  may have put backup files somewhere on the strength of it. If you keep backups
  in a shared or cloud folder, that folder can be read for the names of your
  notebooks, the text of your reminders and the names of every file you have
  attached, by anyone who can list it, without your passphrase.

  A backup also carries the material needed to *try* passphrases against it
  offline. That part cannot simply be removed: it is the same material that lets
  a backup be restored onto a new computer that has never seen your vault, using
  only your passphrase. A file that can do that is, unavoidably, a file that a
  determined attacker can attack — so the practical protection is a strong
  passphrase and a private place to keep the file. Sealing the rest of the
  contents *is* possible and is designed and written down; it is a change to the
  backup file format and will come as its own release.

- **The iPhone's app switcher held a picture of the note you last had open.**
  When iOS sends an app to the background it photographs the screen, so it has
  something to show on the app-switcher card — and it stores that picture among
  the app's own files. Everything else done in this release protects what is
  *in* the vault; none of it touches a photograph iOS took of the screen while
  the vault was open. So for whichever note you had been reading, a readable
  picture of it sat on the phone.

  Hypha now covers the screen with a blank sheet of its own background colour
  the moment iOS makes the app inactive, and uncovers it as soon as you come
  back. The app-switcher card shows the blank sheet instead of your note. You
  will also see that blank sheet flick past when you pull down Control Centre or
  open the photo or files picker — that is the same protection doing its job,
  not a glitch.

- **Attachments you opened in another app, and photos you inserted, were left
  unprotected in the phone's files.** Opening an attachment in another app, and
  exporting or backing up, both write a decrypted copy into a working area
  first; inserting a photo writes the **full-size original** there, which for a
  camera photo or a raw file can be very large. Hypha's own notes said those
  copies were written with iOS's strongest protection so they stay unreadable
  while the phone is locked. They were not — the note said so, and nothing in
  the app ever did it. They got the ordinary default, which is readable any time
  the phone has been unlocked once since it was switched on.

  They are now marked properly, and kept out of iCloud and iTunes backups.
  Separately, the tidy-up that removes those working copies only ever ran when
  you did the *same thing again* — so if the app was interrupted part-way
  through sharing a file or adding a photo, the leftover copy stayed until your
  next share or your next photo, which for some people is never. Hypha now
  sweeps them whenever you return to the app.

- **A stored attachment's filename revealed which file it was.** Attachment
  contents have always been encrypted. But each stored file was *named* after a
  fingerprint of its unencrypted contents — so anyone who could see a list of
  those files, and who already had a copy of some document, could work out
  whether that exact document was in your vault, without decrypting anything.
  Hypha has been renaming these to a fingerprint of the encrypted contents for
  some time, which does not reveal anything, but the renaming only moved a small
  batch each time you unlocked: a vault with a few thousand attachments would
  have taken months of daily use to finish. It now runs through the whole vault
  in one go, gently and in the background.

  Two things this does not reach, said plainly: **backup files taken before
  this** still carry the old names, and nothing on your computer can rename
  files that are already in a cloud folder; and a relay you sync through keeps
  whatever name it was given.

- **On desktop, the keys to your vault could be written unencrypted — and one
  badly-timed crash could destroy them.** Hypha stores the key that decrypts
  your notes in your operating system's keychain. When no keychain was available
  — a Linux desktop without one installed, or a portable Windows build — it fell
  back to writing that key, and your vault's master and owner keys, in plain
  text into a file beside your notes, behind a warning message nobody sees. On
  macOS this never happened; the fallback was there all the same. Hypha now
  refuses, and says what to do about it, rather than quietly doing the one thing
  the keychain exists to prevent.

  The more serious half was not a leak. That file was rewritten in place, and if
  anything interrupted the write — a crash, a full disk, a laptop switched off
  at the wrong moment — the file was left truncated. Hypha then read it, saw
  nothing, concluded this was a fresh install, and generated a **brand new** key
  — after which your existing encrypted database could never be opened again. It
  is now written safely (in full, then swapped into place, readable only by
  you), and a file that cannot be read is reported as a problem instead of being
  treated as an empty one.

### Fixed
- **Your reminder titles, your search terms and your attachment filenames were
  being written to the iPhone's system log.** Hypha forwards its diagnostic
  output to the iOS log so that problems can be investigated on a real device.
  That forwarding was never supposed to carry anything you wrote — but several
  ordinary log lines named the thing they were about, so scheduling a reminder
  recorded its title, searching inside a note recorded what you typed, and
  adding a photo recorded its filename.

  These went to the device's own system log, which lives outside the vault, is
  not covered by the vault's encryption, survives closing the app, and can be
  read back later by anyone who can collect a diagnostic report from the phone.
  It applied to normal installs, not just development builds.

  Every one of those lines now reports the *kind* of thing instead of its name —
  the file's format rather than its filename, how many reminders were scheduled
  rather than what they are called, how long a search was rather than what it
  said. That is what the lines were actually for. Nothing that identifies your
  content reaches the log any more, and a new check makes it much harder for a
  future log line to start doing so again.

## [0.9.0] - 2026-08-17

### Added
- **Scan an invite QR with your iPhone to join a vault.** Point the Camera at the
  code another device is showing, tap the notification, and the phone creates the
  vault and joins it. If it is a vault the phone already has, it says so instead.

  This is what the QR was always for, and on iPhone it had never once worked:
  the phone did not tell iOS it could open `hypha://` links at all, so scanning
  produced "no usable data found" — the same answer you would get from a code
  belonging to another app entirely. Pasting the invite link into "Join a vault"
  was the only route in, and still is if you prefer it.

### Fixed
- **Settings showed one vault's sync and devices under another vault's heading.**
  With more than one vault, Settings lists each vault's sections separately —
  but clicking Sync under a second vault kept showing the first one's owner
  fingerprint, its device list, its connected peers and its last-synced time.
  The settings behind them were always stored per vault; only the panel was
  stale, so what you read was another vault's answer under the name of the one
  you had selected.

  The most serious version of this was the invite: a QR generated for one vault
  stayed on screen after switching to another. Handing that code to someone
  would have added their device to the wrong vault — the panel named one vault
  and the code granted access to a different one. Every section now re-reads
  when you switch vaults, and a generated invite never outlives the vault it was
  made for.

  Also fixed underneath: the list of devices seen on the network was written
  back to whichever vault happened to be selected at the time, so switching
  vaults could copy one vault's device list into another's and leave it there.

- **The sidebar kept showing the vault you had just left.** After switching
  vaults, the sync line in the sidebar went on reporting the previous vault's
  connected devices and its last-synced time. Both are read fresh now. The panel
  half of the same problem is described above; this was the half with no section
  to reopen.

- **Finishing an invite left you on a blank screen, on any device.** Accepting an
  invite — by link or, now, by scanned code — tried to open a Settings page that
  no longer exists, and rendered nothing at all. Desktop and phone alike, for
  months. It lands on Sync now, where the device you just added is listed.

- **"Remove orphaned" could delete files that were still in use.** The list of
  unused attachments is worked out by reading every note and seeing which files
  they mention. If a note had reached this device but the text of that note
  hadn't arrived yet — normal for a minute or two after a new device joins, or
  after a spell offline — the app read it as a note that mentions nothing at
  all, and any file only that note used was put on the unused list.

  Deleting an attachment removes it from **every** device and cannot be undone,
  so this could throw away a photo that was sitting in a note you had open
  somewhere else. The app now recognises that it hasn't finished reading, and
  reports nothing as unused until it has — the same caution it already applied
  when the vault is locked.

- **Trashed notes show their real titles again.** Every note in the trash listed
  as "Untitled" with "no additional text" underneath, whatever it was actually
  called and whatever it contained. Titles are stored encrypted, and the trash
  was the one list in the app that never decrypted them — so it showed nothing,
  and what it showed looked like an empty note rather than a mistake. The trash
  now lists each note under its own title, with the first line of its text.

- **The trash lists files as well as notes.** Deleted attachments now appear
  there alongside notes and notebooks, and can be restored or deleted for good
  from the same place.

- **You can read something before deciding to delete it.** Clicking an item in
  the trash opens a read-only preview — the note as it actually looked, with its
  headings, lists, formatting and images, or the name, type and size of a file.
  Nothing in the trash can be edited: the preview has no way to save.

- **Deleting an attachment can be undone.** Until now, deleting a file from
  Settings → Attachments erased it immediately, on every one of your devices,
  with no way back. There was no trash for attachments and no undo.

  Deleted attachments now go to the trash instead. Nothing is erased and nothing
  is told to other devices — the attachment simply shows as trashed everywhere,
  and you can restore it from any of them. It is erased for good when the trash
  empties, which happens on the same schedule as trashed notes, or straight away
  if you empty it yourself.

  **"Remove orphaned" now asks** whether to move the unused files to the trash or
  delete them outright, because the two are genuinely different: the trash is
  reversible, and deleting is what actually frees the disk space right away.

- **Attachments in the trash are no longer treated as unused.** A note in the
  trash can be restored, but the app had stopped counting it as a user of its
  own pictures and files. So "Remove orphaned" offered those files up for
  deletion — and deleting one removes it from every device with no way back, so
  restoring the note afterwards gave you the note with its images missing. On a
  real vault this was two thirds of the library.

  A note now keeps its attachments for as long as it is in the trash. Emptying
  the trash, or a note ageing out of it, is what releases them — so the
  reversible step stays reversible, and the irreversible one is the one you
  choose.

  The Attachments screen agrees with this: a file used only by trashed notes
  shows those notes with an **In the trash** label and says that emptying the
  trash will release it, instead of reporting it as used by nothing. The
  confirmation for removing orphaned attachments now also mentions that the
  files are deleted on every synced device.

- **The Peers popover in the sidebar is readable.** Clicking the sync line at
  the bottom of the sidebar opens a small panel listing the devices in your
  vault. It had no background of its own: the note list showed straight through
  it, so the device names and the "no devices connected" hint were sitting on
  top of note titles and timestamps. It now looks like every other panel that
  floats over the app — the right-click menu, the search dropdown, a
  confirmation dialog — a solid background, a hairline border and a soft shadow.

  It also sits where it should. The panel used to be positioned as though it
  were always the same height, so with nothing in it there was a gap of about
  150 pixels between the panel and the line you clicked, and with several
  devices listed it ran down over that line instead. It is now pinned just above
  the sync line whatever it contains, and a long list of devices scrolls inside
  it rather than off the screen.

- **The frosted-glass panels had no frosting.** When the window is translucent,
  panels like the Settings cards and the vault passphrase screen are meant to be
  a tinted sheet of glass — you see your desktop through them, dimmed. They were
  drawing no tint at all: the panel was a plain hole onto whatever was behind
  the window, and the text sat directly on your wallpaper. On the passphrase
  screen — the first thing a new install shows — this could leave the heading
  and the hints barely visible.

  The tint is now drawn, at the 65% the themes always specified. Fourteen panels
  gain it: the passphrase screen, the invite-QR panel, and every card in
  Settings. Nothing changes if you have transparency switched off in Appearance,
  and nothing changes on iOS or Linux, where the window is always opaque.

- **The invite QR could grant more than the panel said it did.** When you added
  a device, the role you picked and the code on screen could disagree: the QR
  and link were only generated when the panel opened or when you pressed the
  button, so changing the role afterwards left the previous code sitting under
  the new label. In the harmless direction that was confusing. In the other
  direction it was not — pick **owner**, then switch back to **member**, and the
  panel read "member" while the code still carried an owner invite, which hands
  whoever scans it full control of the vault.

  The code and link are now regenerated the moment you change the role, on both
  screens that offer them, and the old one is cleared first so a stale code is
  never on display. Changing the expiry regenerates them too — it used to claim
  a new expiry over a link that still had the old one. Choosing **owner** still
  asks you to confirm, because that grants full control; declining now puts the
  selector back where it was rather than leaving it reading "owner".

- **More colours that only worked on a dark theme.** Pinned and starred markers,
  shortcut and favourite icons, the reminder chips, the daily-notes dot, and the
  error messages in Publishing and the changelog were all drawn in fixed colours
  chosen against a dark background. On the three light themes they ranged from
  faint to unreadable — the reminder chip text measured barely distinguishable
  from the panel behind it. Each now has a light-theme counterpart, so they read
  on all ten themes.

- **On a light theme, the "delete permanently" buttons were invisible.** In the
  trash, the archive, the reminders list and web notes, the button that destroys
  an item for good was drawn in a pale pink that had been picked to sit on a
  dark background. On any of the three light themes it was pale pink on cream —
  present, clickable, and effectively unreadable. It now uses the theme's own
  error colour, so it reads on all ten.

- **"Search by meaning" missed everything that arrived from another device.**
  Notes you wrote on this computer were understood by search; notes that synced
  in from your phone or another laptop were not, and neither were notes brought
  back from history. They were still found by their words — only the "means
  something similar" half was missing, so the gap looked like the feature simply
  being imprecise. The part of the app that reads a synced note into the index
  had never been able to save what it read.

- **"Rebuild search index" left search by meaning worse than it found it.** It
  cleared the index first and then failed to refill it, so the button you press
  when search feels wrong was the one that emptied it. It repaired itself on the
  next launch, slowly, by re-reading the whole vault.

- **Notes were being read by the model twice, and with the feature switched
  off.** Every save ran the text through the language model once for a result
  that was then thrown away, and again to store it. Worse, that first pass
  ignored the "Search by meaning" switch entirely: with the feature off, saving
  a note still ran the model, and on a computer that had never used it, that
  meant downloading a ~94 MB model for something you had turned off. Both are
  gone.

- **A file too big to sync was offered over and over.** When one device holds an
  attachment larger than another will accept, the second correctly declines it —
  and then asked for it again every time the two reconnected or exchanged
  changes. On a phone that was a large transfer starting and being abandoned
  every few minutes, for a file that could never arrive. The refusal is now
  remembered until the app restarts, and the file is still shown as "too large to
  sync" exactly as before.

- **Sync failures never reached the sync indicator.** When syncing failed for a
  reason that isn't a single file — a vault that can't be opened, a peer that
  can't be understood — the app was supposed to stop claiming everything was
  fine and show "Sync error". That message was wired to a signal nothing was
  listening for, so a broken sync went on reading "Synced 3m ago" indefinitely.
  It now says so.

- **Search by meaning now notices when the way it reads notes changes.** The
  index records what built it — the model, its settings, and how notes are split
  into passages — and rebuilds itself when any of those change. Until now that
  record had to be updated by hand, and a forgotten update would have left two
  incompatible sets of results mixed together, each looking perfectly confident.
  One consequence: the index rebuilds once on the next launch, in the
  background, while ordinary word search keeps working.

### Changed
- **iPhone: the vault switcher is not a settings section any more.** It used to
  sit at the bottom of Settings, below a screenful of scrolling, built from the
  same rows and chevrons as everything above it — so it read as a section called
  "Vaults". It is the opposite of one: every section above it applies *to* the
  vault it names. It now sits at the top, and looks like the control it is.

- **Settings: "Devices" and "Sync" are now one section.** They were two places
  answering one question. Devices held who is in the vault — start or join,
  invite, revoke; Sync held the connection — last synced, sync now, the offline
  toggles — and, at the bottom, a second list of the same devices showing which
  ones were currently connected. So your laptop appeared twice, in two sections,
  keyed the same way, and neither list on its own told you what you wanted to
  know: *is my laptop actually talking to my phone right now?*

  There is now one **Sync** section, and one list of devices in it. Each device
  is a single row that says what it is (owner or member, when it joined) and how
  it's doing (connected, when it was last seen, or that it hasn't connected
  yet — which is a different thing from having dropped out, and used to have no
  row at all). A device that tried to connect but isn't a member of the vault —
  a stranger, or one you revoked that hasn't noticed — is still listed, under
  its own heading, so nothing that used to be visible has gone away.

  An old link straight to the Devices section now lands on Sync rather than
  quietly dropping you on Appearance.

- **iPhone: adding a device is one tap from anywhere.** Tapping the sync dot in
  the navigation bar used to open a sheet that told you the state of things and
  then, if you wanted to do anything about it, sent you to Settings → Sync.
  The most common thing it had to report was *"connected, but no other device is
  reachable yet"* — and the answer to that is to add one, which was four taps
  and another screen away. On the desktop it is a single button in the title
  bar.

  The sheet now carries the invite itself: pick a role and an expiry, generate,
  and the QR code and link appear in place, with the code scrolled into view so
  you can hold it up to the other device straight away. The link is shown as
  selectable text next to the copy button, so a copy the system refuses is
  something you can still work around rather than a button that does nothing.
  Everything else on the sheet — the state, the reason, when it last synced, the
  list of connected devices — is unchanged, and Settings → Sync is still there
  for the device list and the toggles.

  On a phone that *joined* a vault rather than starting one, the sheet says who
  owns it — by the same short fingerprint the owner's own device list shows —
  instead of offering controls that device cannot use. Only the vault owner can
  add devices, and that has not changed.

## [0.8.1] - 2026-08-16

### Fixed
- **iPhone: the app could stop finding your other devices, and stay that way.**
  0.7.1 made this one visible — if the app failed to claim the network port it
  listens on, it said so instead of pretending all was well. This is the fix.

  It turned out not to be the rare accident it looked like. Whenever the app
  re-established its connection to the network — which it does by itself, every
  time it notices it can't see any of your devices — it tried to claim that port
  again a fraction of a second before it had finished letting go of it. On an
  iPhone that is not allowed, so the claim failed, and the phone went deaf to
  every other device until something made it try again. The cruel part: the
  thing that triggered the re-connection was *not being able to see any
  devices*, so the attempt to recover was the very thing that guaranteed it
  couldn't.

  The app now holds the port across that handover. Verified on an iPhone: five
  re-connections in a row, none of them lost the port, where before the first
  one did.

### Changed
- **iPhone: version history now slides up from the bottom of the note instead of
  covering it.** It used to open as a full screen with its own back button,
  which hid the very note you were comparing against — and it arrived carrying
  the desktop's sizes: entries you could barely tap, and a "Restore this
  version" button about half the size Apple asks for.

  It is now a drawer. It rests over the lower half of the screen with the note
  still readable above it, and you can drag it up by the handle to fill the
  screen when you're reading a long history, drag it down to put it back, or
  flick it away. Tapping outside it or the × closes it too, and restoring a
  version closes it for you so you can see what changed. The entries themselves
  are now sized for a thumb.

## [0.8.0] - 2026-08-16

### Added
- **Attachments can be tagged, filed in notebooks, and given a colour — and
  they do it themselves.** A file used to carry nothing but its name, its type
  and its size, so the only way to find one was to remember what it was called.
  Now it carries the same three things a note does.

  You rarely have to set them. A file you put into a note takes on that note's
  tags, notebooks and colour on the spot, and keeps up as you re-file the note
  afterwards. That includes a file you paste into a *second* note: it picks up
  what the second note is filed under too, without losing what it already had.
  Nothing is ever taken away automatically — un-tagging a note leaves its files
  alone — and a file that already has a colour keeps the one it has.

  You can also set them by hand in **Settings → Attachments**, which now shows
  each file's tags, notebooks and colour, lets you change them from the same
  menus the note list uses, and can narrow the list to one of them. Files that
  were already in your vault before this are not left out: **File older
  attachments**, on that same screen, walks your notes and hands each one's
  filing to the files inside it.

  In the note list, selecting a tag, notebook or colour still shows notes and
  only notes. Tick **Files** on the filter chip (or "Files" in the list menu on
  a phone) and the files filed under it are listed underneath; clicking one
  opens it. It all syncs, so a file tagged on your laptop is tagged on your
  phone.
- **iPhone: "Colorize blocks" can now be turned on for a single note.** The
  device-wide default was in Settings, but the per-note switch lives in the
  desktop editor's toolbar — and the phone replaces that toolbar with the bar
  above the keyboard, which has nowhere to put it. So on a phone, half the
  feature had no door at all. It is now in a note's "⋯" menu, next to version
  history.

### Changed
- **The editor no longer tells you that it saved.** It used to read "Saved" from
  the moment you typed your first character until you closed the note, flipping
  to "Saving…" every time it wrote — a word blinking beside your text for the
  whole time you were writing, to report the thing that is true of every save.
  On the phone it also appeared and disappeared inside the top bar, nudging the
  "⋯" button sideways as you typed.

  Saving is silent now. The editor speaks up only when it has something you can
  act on: "Saving…" if a write is somehow still going after a couple of seconds,
  and "Not saved" if one actually failed. Your notes are saved exactly as often
  as before.
- **iPhone: Hypha now requires iOS 16.4 or later** (it was 16.0). No iPhone is
  left behind by this: iOS 16.4 came out in March 2023 and runs on every device
  iOS 16.0 runs on, so any phone that could open Hypha before can still open it
  after a free update it has already been offered. The reason is your data — the
  version of Safari inside iOS 16.4 is the first that lets the app write your
  vault to disk as it goes, rather than saving a copy of the whole thing on a
  timer and risking the last stretch of work if the app is killed.
- **iPhone: your vault is now written to disk as you work, instead of being
  saved as a whole copy on a timer.** Until now the phone kept your entire vault
  in memory and wrote the whole thing out again shortly after you stopped making
  changes — which meant the cost of saving grew with the size of your vault, and
  anything written since the last copy existed only in memory. Now each change
  goes to disk as it is made, the way it always has on the desktop. Two things
  follow: a force-quit or a crash can no longer take the last stretch of work
  with it, and saving does not get slower as your vault gets bigger.

  Your existing notes move across by themselves the first time you open this
  version. Nothing is asked of you and nothing is thrown away — the old copy is
  only removed once the moved-across vault has been opened and read back.

### Fixed
- **iPhone: a note you had just written could be lost if the app was killed
  moments later — and a vault you had just created could vanish entirely.** The
  phone keeps your vault in memory and writes it out shortly after you stop
  making changes. Since 0.6.0 that wait was two seconds, so anything done in the
  last two seconds before the app was force-quit, crashed, or was shut down by
  iOS was still only in memory. Worst case: create a vault, leave immediately,
  and come back to the create-a-vault screen with the whole thing gone.

  The wait is back down to a quarter second. It costs nothing — the measurement
  behind the two-second delay assumed typing writes constantly, and it doesn't
  (20 seconds of solid typing turns out to produce a single write), so the longer
  wait was postponing your data reaching disk without saving any work.
- **iPhone: the bar above the keyboard could sit behind the keyboard.** Tapping
  into the middle of a long note raised the keyboard over the formatting bar,
  which then only reappeared once you had scrolled back to the top. Introduced
  in 0.7.1, as a side effect of removing a blur effect that rendered nothing —
  the blur was also, invisibly, the only thing keeping the bar drawn on top.
- **A failed save could quietly stop a note from receiving edits from your other
  devices.** If a write failed, the editor went on believing one was still in
  progress — and while it believes that, it refuses to take in changes arriving
  from another device, to avoid overwriting what you are typing. That belief was
  never reset, so the note stayed deaf to your other devices until you closed
  and reopened it. Nothing was lost; it just stopped arriving.
- **iPhone (development builds only): launching from the home-screen icon showed
  a blank white screen.** A build started from the icon gets none of the settings
  Xcode passes in, so it looked for a development server on the phone itself,
  where nothing is listening. It now loads the built app in that case, which is
  what a release build has always done.

### Tooling / Dependencies
- **Releases now run every iPhone test, and the linter, before they build.**
  They already ran three of the nineteen iPhone tests, but only if you passed an
  extra flag — and one of those three had been failing all along over the data
  loss fixed above. It was a correct test, reporting a real bug, and three
  releases shipped straight past it because nothing obliged anyone to turn it on.
  All of them now run by default, and the list is discovered rather than written
  down, so a new test enrols itself instead of waiting to be remembered. The
  linter, which was not a release gate at all, is one now.
- **A mobile smoke that kills the app without warning — landed deliberately
  red.** The phone keeps its vault in memory and writes the whole thing out on a
  timer, so anything written since the last write-out is lost if the app dies
  uncleanly. That window has been argued from the code for three passes and never
  demonstrated, because every existing smoke exits *cleanly* — through a reload or
  a browser close, both of which give the app a chance to save. `unclean-kill-smoke`
  crashes the renderer outright instead: it writes 24 notes in a burst, kills the
  process with no warning, reopens, and finds all 24 gone. `npm run smoke:mobile`
  is now **19 of 20 by design**; a 20 of 20 means the smoke was weakened, not that
  the bug was fixed. Closing it is the storage migration scoped in
  `docs/MOBILE-SQLITE-VFS-MIGRATION.md`, and this is that work's acceptance test.

## [0.7.1] - 2026-08-16

### Fixed
- **iPhone: a discovery problem that could hide itself.** If the app failed to
  claim the network port it listens on for other devices — which can happen when
  Wi-Fi changes at just the wrong moment — it carried on as though nothing had
  gone wrong, and simply never heard another device again. It looked exactly like
  the other device not being on the network. It now says so instead.

### Changed
- **iPhone: the app does less drawing and fewer wakeups while idle.** Every row
  in every list was permanently held in the phone's graphics memory in case you
  swiped it, and the bar above the keyboard was applying a blur effect over a
  background you can't see through — invisible, but not free. Neither is needed
  until you actually swipe. The app also stopped demanding the processor wake up
  on an exact one-second schedule to look for your other devices; it now lets iOS
  fold that in with other work, which is easier on the battery.

  You shouldn't notice any of this. It's tidying up after the real fix in 0.7.0.

## [0.7.0] - 2026-08-16

### Fixed
- **iPhone: the app no longer heats up the phone.** This is the real fix for it.
  The part of the app that finds your other devices was asking the system "can I
  send data yet?" — and the system, having nothing to send, answered "yes" **38,000
  times a second**, every second the app was open. Answering that question over
  and over kept a whole processor core busy doing nothing at all, which is what
  made the phone hot, and why it was just as hot sitting idle as it was while you
  typed. It now asks only when it actually has something waiting to send.

  Measured on the device: the app went from using more than a full core to
  **0.5%** — with syncing fully switched on and working exactly as before.

  **The 0.6.0 note below was wrong** and is corrected there: those changes are
  real improvements, but they were not what made the phone hot.

## [0.6.0] - 2026-08-16

### Added
- **Indent and outdent buttons in the editor toolbar.** Nesting a list used to
  need the Tab key, which is fine on a laptop and impossible on a phone — the
  iPhone keyboard doesn't have one. So a nested list written on your computer
  could be read on the phone and never made there. The two buttons sit next to
  the list button in the toolbar, and in the formatting bar above the phone's
  keyboard. They're greyed out when there's nothing to indent.

### Fixed
- **iPhone: the app does much less work while you type.** *(Corrected: this was
  first published as the fix for the phone getting hot. It was not — see 0.7.0.
  The improvements below are real, but the heat had a different cause entirely.)*
  The phone used to rewrite your *entire* vault to storage every time anything
  changed — while typing, about once a second, and the bigger your vault the more
  it cost. It now saves after you pause, and at most every 30 seconds during a
  long stretch of typing. Nothing is lost: it still saves immediately whenever
  you leave the app or switch away.

  Several smaller things on the same path were doing the same work over and over
  for every single character — re-reading the whole note several times to update
  the word count, re-encoding the whole note to send it to your other device, and
  a leftover diagnostic that scanned the note three times just to log three
  numbers it usually threw away. All of them now happen once per pause instead of
  once per keystroke.

  *(This entry originally added a paragraph insisting the device-finding
  connection was not the cause. That was exactly backwards — see 0.7.0. The
  connection genuinely does stay open on purpose, so syncing carries on the
  instant you leave Wi-Fi range; what was wrong was how it waited.)*

- **Bullet lists show their bullets again.** Every bulleted list in every note
  was rendering as plain indented text with no dots at all, on the computer and
  on the phone. Nested levels now step through `•`, `◦` and `▪` the way they
  should, and numbered lists gained a third level (`1.` → `a.` → `i.`).
  Checklists are untouched — their checkboxes were never the problem.

- **iPhone: the Collections screen is one screen again.** Three things on it
  were wrong at once. The favourite ★ on a notebook or tag row was half the size
  of the ★ on a colour row just below it. The `+` buttons on those rows were a
  10-pixel speck — too small to reliably hit with a thumb. And the "Collections"
  title sat on its own line, with the arrow that moves you forward stranded on
  the empty line above it, reading as two separate headers. The stars and pluses
  are now one size with a proper touch target, and the title and the arrow share
  one row.

### Changed
- **iOS: the app no longer zooms like a web page.** Pinching with two fingers
  magnified the whole app — the note list, the nav bar, settings — the way a web
  page zooms in a browser, and there was no way to undo it: the zoom stuck across
  every screen and nothing in the app could put it back. Pinch and double-tap now
  do nothing to the app's own layout, which is how every other iPhone app
  behaves.

  Images are the exception, deliberately: open an image attachment and you can
  still pinch it as large as you like. For making the app itself bigger, iOS's
  own magnifier still works over Hypha (Settings → Accessibility → Zoom).

## [0.5.3] - 2026-08-15

### Fixed
- **The iPhone no longer gets hot looking for a network it doesn't have.** Out of
  coverage — a train, a tunnel, a day out with one bar of 5G — the app kept
  trying to reach the wider internet every minute, forever. Each attempt started
  a small background engine, failed, and started it again. On a long trip with no
  signal that was enough to make the phone warm and, eventually, to make the app
  close itself.

  Hypha now asks iOS whether there is a network before it tries. With no usable
  connection it doesn't start the global sync engine at all, and after a few
  fruitless attempts it stops retrying and simply waits — waking up the moment
  the network changes, you return to the app, or something actually goes wrong.

  Sync over your local Wi-Fi is untouched by all of this. A network with no
  internet, or an iPhone plugged into a Mac by cable, still finds the computer
  next to it.

- **Devices stop dialling each other over the internet when they're already
  talking on the local network.** When your phone and computer are on the same
  Wi-Fi they find each other twice — once locally, once over the wider internet —
  and Hypha keeps the local connection because it's faster. It was then throwing
  the second one away and immediately accepting another, over and over: twelve
  connections in twenty seconds, measured on a phone, all to a computer it was
  already synced with. That ran the whole time sync was working normally, and
  cost battery on both ends.

  Now the redundant channel is told to stand down, and told to resume the moment
  the local connection drops — so falling back from Wi-Fi to mobile data is
  faster than it was before, not slower.

### Changed
- **The phone tells you what sync is doing, from every screen.** There is now a
  small status dot in the top bar of every screen — green when a device is
  connected, grey when there's nothing to talk to, red when something is wrong.
  Tapping it opens a panel with the connected devices, when sync last ran, the
  reason it's paused if it is, and a shortcut to the sync settings.

  Three screens that previously had no top bar at all — Daily notes, Notebooks
  and Tags — have one now, which also gives them a back button.

  The dot never blinks or pulses. An animation that's on screen all day costs
  battery, which would rather defeat the point.

- **On cellular, sync respects Low Data Mode and Low Power Mode.** Ordinary
  mobile data is fine and syncs as usual; it's only when you've also asked iOS to
  economise that Hypha stays off the wider internet until you're back on Wi-Fi.

- **The app recovers if iOS reclaims the page while it's in the background.** On
  a busy phone iOS can throw away a background app's screen contents to free
  memory. Hypha relied on being *told* when that happened, and iOS doesn't always
  say — so it could come back to a blank screen and stay there. It now checks for
  itself each time you return, and reloads if the page is gone.

## [0.5.2] - 2026-08-15

### Fixed
- **Sync works again on the computer.** Since 0.3.0, the desktop app has not
  synced with anything at all: starting sync failed immediately, every time, on
  every vault. Nothing was lost and nothing was corrupted — the notes were only
  ever staying put, and any device that could still sync (an iPhone) kept its
  own copy correct. But two computers, or a computer and a phone, have not
  exchanged anything for three releases.

  The cause was a piece of internal plumbing: a change in 0.3.0 taught the sync
  engine to ask "is there room on disk before I accept a large attachment?", and
  on the desktop — the one place where that question has to travel between two
  halves of the app — nobody was there to answer it. Asking threw, and the throw
  happened before sync could start, so it took everything with it rather than
  just the disk-space check.

  If you have been wondering why a note written on your phone never appeared on
  your computer, this is why, and it is fixed.

## [0.5.1] - 2026-08-15

### Fixed
- **The iPhone stops doing search work it then throws away.** Semantic search
  was switched on by default there, but an iPhone has nowhere to keep the
  embeddings it depends on — so on every single launch the app treated every
  note as unindexed, downloaded a ~94 MB language model, and worked through the
  whole vault computing embeddings that were discarded as fast as they were
  made. On mobile data that is a large download and a flat battery for nothing,
  and it ran in the part of the app iOS shuts down when memory runs short,
  which is what loses unsaved edits. Search on the iPhone was always the
  lexical one — matching titles and text — and that is unchanged and unaffected.
  Settings → Search now says so plainly instead of offering a switch that could
  not do anything, and the first-run question about semantic search no longer
  appears on a device that cannot answer it.

  On a computer nothing changes: semantic search works exactly as before.

### Changed
- **Settings → Search names the right model.** It still described
  `snowflake-arctic-embed-s` at "~33 MB"; the app has since moved to
  `granite-embedding-97m-multilingual-r2`, which is ~94 MB.

## [0.5.0] - 2026-08-15

### Fixed
- **Saving a large file out of a note works again.** In 0.4.0, Download did
  nothing for any attachment over about 32 MB — it stopped with an error about
  the file being too large, on exactly the files most worth getting back out.
  Smaller files were never affected, and nothing was lost: the file stayed in
  the note the whole time. This is a mistake introduced in 0.4.0 itself, by the
  change that made Download stop loading files into memory.

### Changed
- **Opening a file in another app no longer loads it into memory first.**
  "Open externally" used to read the whole attachment at once before handing it
  over — the same thing Download stopped doing in 0.4.0. It now passes the file
  along in small pieces, so opening a large video no longer depends on having
  room for a second copy of it. On the iPhone this also removes an outright
  limit: files over 256 MB refused to open at all.
- **Backups copy attachments in pieces too.** Taking a backup with attachments,
  and restoring one, used to hold each file whole while it was copied. Both
  now work through it a piece at a time. A backup interrupted part-way through
  a file also no longer leaves a half-copied attachment behind that later
  backups would have skipped as already saved.
- **Quitting during a save no longer leaves a stray file behind.** Closing the
  app while a file was being saved out of a note left the half-written copy on
  disk. It is now cleaned up on the way out, and files staged for "Open
  externally" are cleared out after an hour rather than kept forever.

## [0.4.0] - 2026-08-14

### Added
- **You can add audio and video to a note on the iPhone.** There was no way to
  at all: the formatting bar above the keyboard offered images and nothing else,
  and dragging a file or pasting one — the two other ways in — are not things you
  can do on a phone. The button sits next to the image one, opens the same
  picker filtered to sound and video, and what you pick becomes a player in the
  note you can tap to play. Everything behind it already worked; nothing could
  reach it.
- **Photos that show a grey placeholder can be given a picture, on the iPhone.**
  Camera raws, and every iPhone photo added before 0.3.0, were stored exactly as
  you gave them and nothing on any device could open them to draw — so they show
  a placeholder in the note and a blank tile in the list, permanently. Settings →
  Attachments now has **Missing previews**, which makes a small viewable copy of
  each one and links it to the photo. The original is never changed, moved or
  replaced. The copies sync, so a photo fixed on the phone stops being a
  placeholder on your computer too, without doing anything there.

  It reports what it did rather than just finishing: how many were fixed, and,
  for each one it did not fix, which of five reasons applied — over the size
  limit, the file is not on this device, it already had a preview, no note uses
  it, or a copy could not be made. It is safe to run again later; anything
  already fixed is skipped. **Large camera raws are the one thing it cannot
  fix**, and it says so: reading a 95 MB photo to make a copy of it is the exact
  thing that used to crash the app on a phone, so it is deliberately left alone.
  Photos from an iPhone are the ones this is for, and they are all well under the
  limit.

### Changed
- **Downloading an attachment no longer loads it into memory first.** Saving a
  file out of a note used to decrypt the whole thing at once — fine for a
  photo, and the reason a very large video could fail on a device with less
  memory than the file. It is now decrypted straight into the file you chose, a
  piece at a time, so the size Hypha can save out stops depending on how much
  memory it can spare. Files stored before this change still take the old route
  and are unaffected either way; the difference applies to what is added from
  here on. If a download fails part-way, the partly-written file is removed
  rather than left looking finished.

### Fixed
- **A file you have just added can no longer be deleted as "unused".** Adding an
  attachment and writing it into a note are two separate steps, and in the moment
  between them nothing in your notes referred to the file yet — so "Remove
  orphaned" in Settings → Attachments would offer it up and delete it, on every
  device. Anything added in the last ten minutes is now left alone. Files that
  really are unused are still reclaimable; they just wait a few minutes first.

### Tooling / Dependencies
- More of the same groundwork, and still **nothing you can see**: Hypha can now
  *write* the new storage layout as well as read it, but no build turns that on.
  It stays off until every device you sync with is running a version that can
  read it — a device that wrote the new layout to one that could not would
  produce attachments that transfer, verify, and then refuse to open. Files
  already in your vault are untouched either way.
- Sync logs now say when a file transfer was abandoned partway — which file, how
  far it got, and why. Previously a transfer that was interrupted eleven times
  and one that ran once looked identical in the log, which is the measurement
  needed before Hypha can resume an interrupted transfer instead of restarting
  it.
- Groundwork for playing and exporting very large videos, with **no change you
  can see yet** — recorded here because it is a change to how attachments can be
  stored, not because it does anything for you today. An attachment is currently
  sealed as one box, so opening any part of it means unsealing all of it, which
  is why files above a per-device size say "Too large to open on this device"
  rather than playing. There is now a second storage layout that seals a file in
  independent 256 KiB pieces, so a future version can decrypt just the part it
  needs. **Hypha can read that layout; nothing writes it yet, and no existing
  attachment is affected or ever will be** — the layout can only apply to a file
  added after it is switched on, because every device verifies an attachment
  against a fingerprint of its stored bytes and re-sealing one would look like
  tampering to all of them. The reader ships first, and on purpose: a device that
  wrote the new layout to one that could not read it would produce files that
  transfer, verify, and then refuse to open.
- The release build now packs the iPhone's peer-to-peer worklet itself. It never
  did, and the check that noticed stopped the 0.3.0 build after every test had
  run — with a fix-it command the release script does not run.

## [0.3.0] - 2026-08-14

### Added
- **Your iPhone now syncs over the internet, not just your own Wi-Fi.** Until
  now the phone could only reach your computer when both were sitting on the
  same network — leave the house and everything you wrote stayed on the phone
  until you came back. It now finds your other devices the same way they find
  each other: through a distributed lookup, over the internet, wherever it
  happens to be. Confirmed on a phone with Wi-Fi switched off entirely, syncing
  notes in both directions with a laptop elsewhere, neither device reachable
  from the outside and no server in between.

- **Large photos, videos and files now actually reach your other devices.**
  0.2.3 could only tell you when a file was too big to send; sending it was
  named there as the next piece of work, and this is it. An attachment now
  travels in pieces rather than as one message, so neither device ever holds the
  whole file in memory to move it, and a transfer that is interrupted does not
  take the connection down with it. Up to 1 GB between computers and 128 MB to
  an iPhone, where storage is shared with your notes. The file is verified
  against its own fingerprint before it is filed away, so a partial or altered
  transfer is discarded rather than saved; until it has been, nothing on the
  receiving device points at it. An always-on relay passes the pieces along the
  same way.

- **Swipe in from the right edge to get back to your note (iPhone).** Going
  forward from the list to the note you were just editing meant finding its row
  and tapping it again — the list is nothing but rows, and rows already use
  leftward drags for their own reveal actions, so there was no forward gesture
  at all. A drag that begins within a thumb's width of the right edge now moves
  forward to the editor, mirroring the swipe that takes you back.

- **Hypha now checks there is room before accepting an attachment.** Nothing in
  the app had ever asked how much storage was left. A phone with 40 MB free
  would happily accept a 300 MB video, write as much of it as fit, and fail
  partway through — and on iPhone, where attachments share their storage
  allowance with the notes database itself, filling it up put more than the
  download at risk. An incoming file is now declined before a single byte is
  written unless there is room for it, for the copy the phone makes when it
  files it away, and for a reserve on top. The device that asked for the file
  says so on the placeholder: "No room on this device", with the size, rather
  than the old and quite wrong "Not available from the other device" — the other
  device is fine, and it is still holding the file for whenever you make space.
  An always-on relay does the same, and keeps passing files along to everyone
  waiting for them even once it has stopped keeping its own copies.

### Fixed
- **Devices could only ever sync on the same Wi-Fi.** Hypha is meant to find your
  other devices two ways: directly over the local network, and over the internet
  through a distributed lookup — the second being what lets a laptop at home and
  a laptop at work stay in step, and what an always-on relay exists to be found
  by. The second way had never once worked, on any version. Three separate
  faults in the same fifteen lines each produced the identical symptom — nothing
  happens — so each one hid the other two, and the local network quietly carried
  every sync anyone had ever seen. All three are fixed: two devices now find each
  other over the internet in well under a second. If you have been running a
  relay and wondering why nothing reached it unless you were sitting next to it,
  this is why. The iPhone is now on that same internet path too — see Added.
- **A file too big for your iPhone was sent to it anyway, over and over.** When
  a computer held an attachment larger than the phone would accept, the phone
  said so, the computer agreed — and then sent the entire file regardless. Every
  time the two reconnected. On a home network this was invisible waste; over the
  internet it was enough to knock the connection over, which made syncing away
  from home look unreliable when the only thing wrong was one oversized file
  being pushed on repeat. The refusal is now respected: the transfer stops
  within a fraction of a second instead of running to the end.
- **Syncing went quiet for a while after your iPhone had been asleep.** Locking
  the phone kills its connection to your computer, but the computer carries on
  believing the two are still talking — so when the phone tried to reconnect, it
  was turned away as a device that was already connected. It sorted itself out
  after a while on its own, which is why this read as "sync is sometimes slow"
  rather than as a fault. The computer now recognises a genuine new connection
  from a device it thinks it already has, and takes it.
- **An always-on relay sent every attachment to every device in the vault.**
  When two computers moved a large file through a relay, every other device on
  the vault — your phone included — was sent the whole thing, whether or not it
  had asked for it or had any use for it. On a phone that is somebody's mobile
  data and somebody's battery. The relay now passes a file only to the devices
  that actually asked for it.
- **A device syncing through an always-on relay could not turn a file down.**
  When a device decides it does not want an attachment — it already has it, or
  the file is bigger than that device can open — it says so, and the sender
  stops. Sent to a relay daemon, that refusal was misread as a corrupt message
  and thrown away, so the file was pushed anyway: bandwidth spent on a photo the
  device already had, a "Too large to sync" placeholder for something it never
  asked for, and enough unwanted transfers at once to crowd out one it actually
  wanted. Two devices syncing directly to each other were never affected.
- **Very large attachments could quit the app when you opened them.** Since large
  files started syncing between devices, a phone could receive a file far bigger
  than it could open — and playing or previewing one loads the whole thing into
  memory at once, several times over. Hypha now says "Too large to open on this
  device" and names the size, instead of stalling or shutting the app down. The
  file itself is untouched: it stays in your notes, it keeps syncing, it opens on
  a computer, and Download and "Open externally" still work everywhere. The
  limits are 256 MB on the desktop and 32 MB on iPhone, where memory is much
  tighter.
- **Photos kept in their original format still had no thumbnail on your other
  device.** 0.2.3 fixed this only on the device the photo was added on; the note
  list on the *other* device went looking for the original file, which no
  computer can open, and left a blank tile — after doing a lot of work to find
  that out. The list now uses the viewable copy everywhere.
- **Quitting the app could lose whatever you had typed in the last few seconds.**
  Your note itself was always safe — this was the saved *version* in note
  history, which is supposed to capture where you left off when you quit, and
  never once did on the desktop. Three separate things had to go right and none
  of them did: the database was closed before the request to save was sent, note
  windows opened in their own window were never asked at all, and nothing waited
  for the writing to finish before the app disappeared. Quitting now asks every
  window, and waits.
- **A note opened in its own window did not sync what you typed in it.** The
  edit was saved, and it appeared in your other windows on the same computer —
  it just never left the device. Anything written in focus mode stayed there
  until you happened to edit that note from the main window as well. Every
  window now reports its edits, whichever one you are typing in.
- **Version history sat on "…" instead of showing the version you opened.** The
  older version had already loaded; the panel simply did not notice, and kept
  its placeholder until something unrelated made it redraw — at which point
  every version you had opened appeared at once. It reads as a fluke, which is
  why it survived so long.
- **Daily notes could stop working entirely on a device.** A single note whose
  title had gone missing was enough: the code that keeps daily notes in order
  gave up on the whole list rather than skipping that one note, so today's daily
  note stopped being found or created. Seen on an iPhone and in an account
  window.
- **Six toolbar buttons were blank on iPhone.** Undo, redo, code block, table,
  insert date and clear formatting drew nothing at all — the buttons worked if
  you knew where to press. Two of them named symbols that do not exist, and the
  rest only appeared after some other part of the app had loaded its full set of
  symbols, which made them look intermittent rather than missing.
- **The always-on relay could not be installed by following its own
  instructions.** Two breaks on the way to a running `hypha-peer`, both in the
  first five minutes: the daemon had no `--help` at all, so the check the deploy
  guide gives you for a successful install could never pass and reported a
  correct install as broken; and the documented `npm install -g` step is
  something npm refuses outright for a workspace package. `--help` now exists
  (and lists every command and option), and the install is the one that actually
  works — drop the bundle and its dependencies in a directory, with a wrapper at
  the path the systemd unit expects.

### Tooling / Dependencies
- Switching `better-sqlite3-multiple-ciphers` between the Node and Electron ABIs
  no longer recompiles it. The two runtimes contend over one hoisted
  `better_sqlite3.node` — `test:contract` wants Node's ABI (147), the app wants
  Electron 43's (148) — so alternating between the tests and the app meant a
  ~20 s node-gyp build every time, and forgetting it meant ~450 unrelated vitest
  failures or an app that dies at `sqlite.open`. A build for a given (runtime,
  version, arch, package version) is immutable, so each one is now acquired once
  and kept in `node_modules/.cache/hypha-sqlite-abi/`; every flip after that is a
  file copy (~150 ms, offline). New `scripts/sqlite-abi.mjs` owns this for both
  directions — cache, then `prebuild-install` (upstream publishes `node-v147`,
  but only up to `electron-v146`, so Electron 43 still compiles the first time),
  then a real build. `scripts/rebuild-electron.mjs` keeps the Electron binary
  fetch and delegates the rest; `pretest:contract` calls it instead of
  `npm rebuild`. The marker records the ABI actually observed in the file, so an
  `npm install` that quietly restores the host-Node prebuild is detected and
  re-flipped rather than trusted. `HYPHA_FORCE_REBUILD=1` still forces a genuine
  from-source rebuild, and now bypasses the cache.

## [0.2.3] - 2026-08-12

A day of running Hypha on a phone and a Mac side by side. Two things came out
of it: photos from an iPhone now work properly on both devices, and syncing
between them stops going quiet on you.

### Fixed
- **Edits made on the iPhone often never reached the other device.** Typing on
  your phone would quietly stop reaching your Mac — while edits made on the Mac
  kept arriving on the phone, so syncing looked like it was working. Every save
  was starting a second copy of the syncing machinery without shutting the first
  one down, and the copy holding the connection was not the one watching your
  note for changes. Nothing was ever lost: the edits were always saved on the
  device you made them on, and they travel as soon as both devices are talking
  again.
- **Syncing did not come back after the phone had been locked for a while.**
  iOS shuts down a sleeping app's network connections without telling it, so the
  phone stopped announcing itself and nothing tried again. It now notices it has
  lost the other device and re-establishes the connection within a few seconds
  of you picking the phone up. A quick lock and unlock never dropped anything
  and still doesn't.
- **Adding camera raws (DNG) or very large photos quit the app on iPhone.** A
  raw file is small on disk but enormous once opened — a 95 MB DNG becomes
  186 MB of image in memory — and Hypha opened every picture it was given, at
  full size, before deciding what to do with it. iOS shut the page down
  mid-insert, which cost a deletion and four photos in one sitting.
- **Adding several photos at once quit the app on iPhone.** Picking three or
  four pictures from the photo library reloaded Hypha with an empty note and
  nothing saved. Two separate causes: storing a photo read it several times over
  and decoded it in full more than once, and *showing* it then made several more
  copies and never released them. Photos are now read once, decoded once, and
  released when they go off screen. Adding a batch is faster on the desktop too,
  which had the same waste and just enough memory not to notice it.
- **Images in a note leaked memory every time you opened it.** Each visit kept
  another full copy of every picture in the note until the app was restarted.
  Long sessions with image-heavy notes should feel steadier.
- **iPhone photos kept as originals were invisible on the desktop.** Photos from
  an iPhone are HEIC files and no desktop browser can open one — so a photo
  added on the phone and kept in its original format synced correctly, arrived
  correctly, and showed as a broken image on your Mac. Hypha now makes a
  viewable copy of every HEIC photo, the same way it already did for camera
  raws, and shows that copy everywhere. *Photos you chose to compress were never
  affected — compressing already converted them.* Photos added before this
  update show their filename instead of a broken image; adding them again fixes
  them.
- **Photos kept in their original format had no thumbnail in the note list.** A
  camera raw or iPhone photo displayed properly inside the note but left a blank
  tile in the list beside it. The list now uses the same viewable copy.

### Added
- **Camera raws and iPhone photos now work, and you choose what to keep.** Hypha
  makes a viewable copy of each one — an iPhone does this without ever unpacking
  the full picture, so a 95 MB raw becomes a sharp 1.4 MB copy in about two
  seconds — then asks once per batch whether to keep the originals as well. The
  copies are what you see in the note, what appears in the note list, and what
  reaches your other devices. "Only keep the copies" never stores the original at
  all, so four raw photos cost a few megabytes instead of two hundred. Keeping
  the originals is fine too, but note they stay on the device that added them for
  now, since files that large cannot yet be sent between devices.
- **A photo or video too big to send now says so, instead of looking broken.**
  Files above Hypha's transfer limit were refused by the device holding them, and
  the device waiting for them was never told — so a picture added on your phone
  showed up on your laptop as a blank grey box that never resolved, looking for
  all the world like a slow connection. It now reads "Too large to sync" with the
  file's size, on both the picture and the video player, so you can tell a
  transfer that is still running from one that is never going to happen. Sending
  large files between devices is the next piece of work.

### Changed
- **The keyboard's grey ↑ ↓ ✓ bar is gone on iPhone.** iOS adds that bar for web
  pages with lots of form fields, so you can jump between them — a note has one
  field, so both arrows did nothing and it sat on top of Hypha's own formatting
  bar taking up a row of screen. Use the formatting bar's chevron to put the
  keyboard away.

## [0.2.2] - 2026-08-11

Six iPhone fixes from a day of actually carrying the app. Nothing here changes
syncing or your notes — it is all the app being usable in one hand.

### Fixed
- **Taking a photo into a note crashed the app.** Insert image → "Take Photo"
  quit Hypha instantly, every time: iOS shuts an app down on the spot if it
  reaches for the camera without declaring why it needs it, and we never did.
  The camera and microphone are declared now, so taking a photo — or recording a
  video — works and asks permission the normal way. *Choosing an existing photo
  was never affected.*
- **The keyboard covered things you needed to tap.** On iOS the keyboard slides
  over the page rather than making room, so anything anchored to the bottom of
  the screen ends up underneath it. That hit the menus the formatting bar opens
  (headings, lists, colours — which looked like they simply did nothing), the
  compress-images question when pasting a picture, the reminder editor's own
  Save button, and every other dialog with a text field in it. They all sit
  above the keyboard now, and a long one scrolls inside itself instead of
  running off the top of the screen.
- **The formatting bar itself sometimes ended up under the keyboard.** Two
  causes: pinch-zooming while typing dropped it, and a keyboard change the app
  was never told about — coming back from another app, typically — left it
  parked where it was. Both fixed.
- **Tapping the note you just came back from did nothing.** Open a note, go back
  to the list, tap that same note: nothing happened, and it stayed unreachable
  until you opened a different note first. Tapping a pinned notebook had the
  same bug from the other direction — it opened whatever note was already open
  instead of showing the notebook.
- **Returning to the app looked like it had restarted.** A white flash and the
  app starting over. iOS reclaims memory from backgrounded apps and Hypha's page
  is a fat target; the recovery is a reload, which is fine, but it ran while the
  app was still off-screen and flashed white on the way back. It now waits until
  you return, and paints your theme's own background instead of white — on
  launch, too. *Your writing is not affected: it is saved when the app leaves
  the foreground.*
- **The × on the suggestions bar was too small to press.** It, the suggestion
  chips, and the related-note buttons are all thumb-sized now.

## [0.2.1] - 2026-08-11

Three sync fixes found by running 0.2.0 on a real iPhone. Every one of them was
invisible to the automated tests, and two of them made syncing look broken in
ways that were easy to blame on the network.

### Fixed
- **An iPhone that had joined a vault could never reconnect after being
  restarted.** Joining worked, and syncing worked for as long as the app stayed
  open — but the permission slip the other device issues on first contact was
  never saved. On the next launch the phone had nothing to identify itself with,
  so it presented its original invitation again; invitations are single-use, so
  it was refused, every time, for good. The phone sat on "syncing" and the
  laptop showed it as disconnected. The credential is now stored, so a phone
  reconnects on its own after a restart, a crash, or a phone reboot.
  *If you hit this, the invitation really is used up: remove the vault on the
  phone, make a fresh invitation, and join again. Nothing is lost — the other
  device holds everything.*
- **The note that was already open when you started the app didn't sync your
  edits.** Reopening the app restores whichever note you had open, and that
  happens before syncing has finished starting up — so that one note was never
  registered for live sync. Typing in it reached no other device, while edits
  *from* the other device still appeared, which made it look like sync had half
  failed. Opening any other note worked normally. The request is now held until
  syncing is ready.
- **A note open on two devices could stop showing the other device's changes
  once you started typing.** Incoming changes are never applied on top of what
  you are in the middle of writing — but they were then forgotten rather than
  applied a moment later, so they stayed invisible until the note was closed and
  reopened. Nothing was ever lost: the changes were already saved, just not
  shown. They now appear as soon as your own typing has been saved.

## [0.2.0] - 2026-08-11

The first release since the 0.1.0 alpha, and mostly a correctness one: forty
landings' worth of defects that a green test suite could not see, several of
which lost or hid data. Read the two callouts below before upgrading — one asks
you to republish, the other is about what has and has not been confirmed on an
iPhone.

> **The iPhone fixes in this release are unconfirmed on hardware.** Hypha's
> automated tests cannot run the native part of the iOS app; everything there
> compiles and typechecks, and the layer above it is proven headlessly, but a
> device has not run this build. Each affected entry says so where it stands.

### Fixed
- **Adding the same file on two devices before they synced left one copy of it
  unreadable — on both.** Attachments are encrypted individually, so two devices
  that add the same picture while apart each produce a *different* encrypted
  file from the same original. Hypha stored them under a name derived from the
  original, so the two collided: whichever arrived second overwrote the first,
  and one of the two attachments would not open no matter which device you were
  on. Worse, the two kept displacing each other — opening one made the other
  fail, and fetching the missing one undid the repair. Encrypted files are now
  stored under a name derived from the encrypted bytes themselves, so both fit
  side by side and both open. Existing attachments are moved to the new naming
  quietly in the background after you unlock, a little at a time, and stay
  readable throughout; nothing is re-encrypted and nothing is deleted until its
  replacement has been written and read back.
- **A note Hypha could not decrypt looked like an ordinary untitled one.** If a
  note's key cannot be unwrapped — a note carried over from another vault, a
  half-restored backup — its title cannot be read, and the note was shown with
  the same blank "Untitled" every note you never got around to naming shows.
  There was no way to tell the two apart, and typing a new title over it looked
  like it worked while silently changing nothing. Such a note is now labelled
  "Unreadable title", with the reason next to it, in the notes list, the archive,
  the tab bar, the quick switcher and on iPhone; its title field is read-only,
  because the note cannot be written to at all. Nothing about the note is
  altered or removed — it is left exactly as it is, in case the key turns up.
- **A paired iPhone could stop syncing entirely.** A bug introduced in the last
  round meant that the moment another device was found, an internal error threw
  in the middle of the introduction — so the connection was abandoned before it
  finished. Every device was dropped the same way, so an iPhone could sit next to
  a laptop on the same network, both apparently fine, and never exchange a single
  note. Fixed, and the two checks that would have caught it are now part of the
  routine test run rather than an optional extra.
- **A single bad message could make an attachment permanently unreadable.**
  Because an attachment's file is encrypted before it travels, the receiving
  device cannot tell a genuine file from a forged one until it opens it — and
  once it had stored anything under that attachment's name, it never asked
  anyone else for the real one. The attachment listed correctly and failed to
  open, forever, on that device. Now a file that fails to open is remembered as
  bad: the next time a device that has the real one connects, it replaces it, and
  the attachment opens again. Nothing is deleted in the process — the file that
  would not open is kept until a good one arrives to replace it.
- **With two vaults open, one vault's reminders never fired.** Reminders were
  scheduled for the whole app rather than per vault, so whichever window most
  recently updated its reminders took ownership of all of them — and the other
  vault's simply never went off. A reminder that did fire could also be delivered
  to the wrong window, which is how a notification could open a note that did not
  exist there. Each vault now keeps its own reminders, they arrive in the window
  they belong to, and closing a vault's window puts its reminders away with it.
- **The Find bar reported "NaN / 3".** The match counter was reading a value that
  did not exist, so the position never showed a number — for the whole life of
  the feature. It now reads "1 / 3". In the same pass: leaving the Find bar open
  and switching to another note left it counting the *previous* note's matches
  and no longer responding to typing; it now follows the note you are looking at.
- **Cancelling "Attach file" leaked a little memory each time.** Dismissing the
  file chooser without picking anything left an invisible element behind; enough
  cancelled attempts in one session added up. It is now cleaned up whether you
  choose a file or not.
- **Leaving or switching a vault did not stop it looking for that vault's
  devices.** Hypha kept the network listener and the announcement running for the
  vault you had left, and kept the connection to the old vault's devices wired up
  behind the scenes — so a session that switched vaults a few times was still
  announcing every one of them. On desktop the same teardown could also fail in a
  way that took the app down in the background. Leaving a vault now shuts all of
  it down properly, and the app waits for that to finish before opening the next
  one. Related: a device that dropped off the network in the middle of connecting
  was reported as having failed a handshake several seconds after it had gone.
- **On iPhone, connections that could never succeed were never given up.** Trying
  to reach a device that had left the Wi-Fi network left the attempt — and its
  open socket — in place for as long as the app ran, once per attempt. Switching
  vaults left the previous vault's listener and announcement running underneath
  the new one. Both are now closed down.
- **On iPhone, an error at the wrong moment could stop syncing silently and
  permanently.** If the phone reported a failure whose text ran onto a second
  line, the message it sent back to the app was malformed and thrown away, so the
  operation that was waiting for it waited forever — with nothing shown and
  nothing logged. Those messages are now built safely, and any request that gets
  no answer within fifteen seconds fails with a real error instead of hanging.
- **On iPhone, the app announced itself to other phones only once, at startup.**
  It should announce itself every second, so that devices that arrive later — or
  after the Wi-Fi drops and comes back — can find it. Two iPhones could therefore
  fail to find each other entirely; a phone and a laptop kept working only because
  the laptop announces itself continuously.

  *These four iPhone fixes are in the native part of the app, which our automated
  tests cannot run. They compile and typecheck, but they have not yet been
  confirmed on a device.*

### Security
- **A device on the same network could make Hypha chase peers that were never
  there.** To be found by your other devices, Hypha announces itself on the local
  network in the clear — that announcement has to be readable before any keys are
  exchanged, so anything on the same network can send one too. Hypha believed
  each one enough to remember it and to try connecting, and it remembered every
  single one, forever. A stream of invented devices could therefore make it hold
  an ever-growing list and open an unlimited number of outgoing connections to
  addresses of the sender's choosing. Announcements are now checked for being
  even plausibly a device before anything is remembered, only a fixed number of
  devices are tracked at a time (far more than anyone owns, and a device you
  really do hear from keeps its place), and only a handful of connection attempts
  can be in progress at once. None of this decides whether a device is *trusted* —
  that has always been the encrypted handshake's job, and it is unchanged.
- **An iPhone could be killed by the system while catching up on a big sync.**
  Data arriving from another device was accepted as fast as the network delivered
  it, with no way to say "wait" — so a large catch-up landing while the phone was
  busy drawing the screen piled up in memory until iOS shut the app down. Hypha
  now tells the receiving side to pause while it works through what it already
  has, and resumes when it has caught up. If the pause cannot be honoured for any
  reason, that one connection is dropped and retried instead of the whole app
  going down with it.
- **A device on the same network could exhaust Hypha's resources.** Anything that
  could reach the app's sync port could open connections and simply never
  complete the introduction — each one holding a slot open indefinitely, with no
  limit on how many. Enough of them would stop the app from opening files at all.
  Incomplete connections are now dropped after ten seconds, and there is a cap on
  how many can be waiting at once, which is far above what real use needs.

- **A large vault could not sync at all.** Above roughly thirty thousand notes,
  tags and notebooks, the batch of metadata one device sends another outgrew what
  a single message can carry — and instead of sending it in parts, Hypha reported
  a sync error and sent nothing. Every reconnect failed the same way, so a new
  device paired to a big vault stayed permanently empty. Metadata is now sent in
  as many parts as it takes, in timestamp order, with the sender continuing until
  the other device holds everything. Smaller vaults are unaffected — they still
  travel in one piece — and no device needs updating for this to work: the parts
  look exactly like ordinary sync messages to the receiving side.
- **Note history never saved a single version.** The history sidebar — the
  timeline, the per-version diff, the Restore button, on desktop and iOS alike —
  had nothing behind it: no version was ever written, for the whole life of the
  feature. It always said "No saved versions yet", which reads as a true answer
  about a new note rather than a broken feature, and Restore reported success
  while doing nothing at all. Hypha now saves a version per editing session —
  when you stop typing for a couple of minutes, switch notes or tabs, close the
  app, or lock the vault — keeping the last 30 per note, and Restore really does
  put an earlier version back. Versions stay on the device that made them: they
  are your own undo history, not something every paired device needs a copy of,
  and they are encrypted at rest like the note itself, so a locked vault shows
  them as locked rather than as text. A restore is itself undoable — the version
  you restored *from* is saved first. Deleting a note permanently deletes its
  history with it; moving it to the trash and back does not. Also: the "5m ago"
  timestamps in that sidebar were never translated, and the restore confirmation
  was a raw browser dialog that froze the window — both fixed.
- **"Open externally" on an attachment did nothing on iPhone but show an error.**
  Opening a file Hypha cannot preview — a PDF, a spreadsheet, an archive — is
  handed to the operating system on the desktop, and on iOS there was nothing
  behind the button at all. It now stages the decrypted file and raises the
  iOS share sheet, so an attachment can be opened in another app, saved to
  Files, or printed. The staged copy is protected by iOS Data Protection while
  the device is locked, excluded from backups, and cleaned up an hour later —
  and it is the only file Hypha will hand to another app, so a link inside a
  note cannot be used to pass anything else along.
- **The spell-check settings on iPhone were controls that did nothing.**
  Language settings offered a spell-check switch, a status line and a language
  list, none of which iOS lets an app change — the switch flipped back, the
  status stayed "off" and the list was always empty. That whole block is gone
  on iOS; the interface-language picker above it is unchanged. Nothing is lost:
  iOS spell-checks and autocorrects through the keyboard already. The command
  palette's "Toggle spell check" is hidden there for the same reason.
- **Importing from Standard Notes produced nothing at all.** Settings → Import
  walked the export folder, matched up the media files, and then reported
  "Imported 0 notes" as a success, on desktop and iOS alike — the converter at
  the centre of it returned an empty document for every note, and an empty
  document is what the importer treats as "not a note" and skips. The converter
  is now real: paragraphs, headings, all six formatting marks, text colour,
  links, quotes, code blocks with their language, bullet, numbered and nested
  lists, checklists with their tick state, tables with header rows, horizontal
  rules, and attached images, audio, video and files. Hashtags in a note become
  real Hypha tags linked to it. Inline pasted images are stored as proper
  encrypted attachments instead of being left as base64 in the note body, and an
  attachment that cannot be found is now named in the import summary instead of
  vanishing quietly.
- **Images could disappear from a note permanently.** An image's link to its
  stored file was dropped every time a note was loaded from HTML rather than
  from its live document — which is what happens to any imported note, and to a
  note that has not yet been opened on that device. The first load left an image
  that could never display again; the second removed it from the note outright,
  and because the emptied note is what gets saved and synced, the loss spread to
  every device and could not be undone. File attachments and their filenames
  were lost the same way. An image's stored dimensions and file size are also
  kept now, where before both were discarded on save.
- **Reminders never actually fired — on any platform.** The function that
  computes a reminder's next fire time was a placeholder that always answered
  "never", and it is the only input to the schedule every platform arms from.
  Every reminder listed, synced and looked healthy while no notification was
  ever scheduled, on desktop as well as iOS. It is now implemented for one-off,
  daily, weekly, monthly and yearly reminders. A monthly reminder set for a day
  a given month does not have (the 31st in April, 29 February in a common year)
  now waits for the next month that does, rather than firing a day early.
  The reminders list also sorts by next fire time again, which the same
  placeholder had quietly disabled.

### Added
- **Photos from a phone can now be compressed when you attach them.** The
  Settings → Attachments compression preference already existed and nothing read
  it; it works now, and it understands the formats phones actually produce
  (HEIC and AVIF, alongside JPEG and PNG). It refuses anything where re-encoding
  would lose something: animations, drawings that scale, images whose
  transparency would be flattened, and small files that would only grow. One
  format is platform-dependent: HEIC compresses on iPhone but is kept as-is on
  desktop, because the desktop app has no decoder for it. Everything else,
  AVIF included, compresses on both.
- **iOS: Backup & Export, Restore and Import.** These settings sections were
  hidden on iOS because the platform had no file picker behind them. iOS can now
  save a backup to Files, restore one, and import a Standard Notes export
  folder; a chosen backup folder is remembered across app launches, so scheduled
  backups work there too.
- **iOS: reminders that alert on the device.** Reminders were synced items only:
  one created on a phone could alert a paired desktop, but never the phone.
  They now schedule real iOS notifications, fire with the app closed, and open
  the linked note when tapped. Permission is requested when you save your first
  reminder, not at launch.

### Changed
- **"Monographs" is now "Web Notes".** The inherited name is gone from
  the whole tree — the sidebar entry, the `/web-notes` route, the command
  palette entries, the `WebNote` contract type, the `WebNotesFacade`, the
  `hypha://webNote/<id>` deep-link kind, and the `webNotes.*` translation keys.
  Nothing about how publishing works changed.

> **Anything published before this release must be republished.** The rename
> reaches the stored row: a published note is persisted as an item of type
> `"webNote"` at an id derived from that same string, and no migration converts
> the old rows. Concretely, after upgrading:
>
> - Previously published notes disappear from the Web Notes list and lose their
>   globe badge in All Notes.
> - **Their pages stay live in the bucket.** The old URL keeps serving, and the
>   app can no longer unpublish it, because unpublish resolves the row by id.
>   Republishing mints a fresh share id, so the old page and the new one coexist
>   at different URLs.
> - **Unpublish everything before upgrading**, then republish afterwards. If you
>   have already upgraded, delete the stale objects from the bucket by hand.
> - Peers must upgrade together: an old and a new build write different item
>   types for the same feature and will silently stop agreeing about what is
>   published. Backups taken before the rename restore successfully, but their
>   published-note rows restore as orphans.

## [0.1.0] - 2026-08-08

First alpha. Everything below is the 0.1.0 development history; nothing has
shipped under an earlier version.

> **Peers must share a build.** The wire format changed during this cycle (see
> "bulk wire length prefixes widened to u32" under Fixed). Two devices on
> different builds fail loudly at the handshake rather than corrupting data, but
> they do fail — update every device and any relay daemon together.

### Added
- **Publish to S3 (Phase 8) — the last product thread.** Publish a note as a
  self-contained static page to any S3-compatible bucket (AWS S3, MinIO,
  Cloudflare R2, DigitalOcean Spaces, Backblaze B2), configured under
  Settings → Publishing. The publish UI already existed and had always called a
  stub; it is now real, backed by a new pure `packages/s3-publish` (hand-rolled
  SigV4 over WebCrypto — no AWS SDK — plus the page renderer, an egress
  sanitizer, and the upload plan) and a `WebNotesFacade` in the engine.
  - **Passphrase protection is real encryption**, not an unguessable link: the
    bucket gets a prompt page plus an AES-256-GCM payload with every attachment
    inlined, so nothing readable is left beside it. The in-browser decryptor can
    only use a KDF WebCrypto ships, so it is PBKDF2-SHA256 at 600k iterations —
    which is why the dialog generates a strong passphrase by default rather than
    inviting a memorable one. Republishing a protected note requires a
    passphrase; the old one was never stored.
  - **Expiry instead of self-destruct.** A plain bucket has no view counter, so
    "self-destruct after first view" was not deliverable and was replaced by
    time-based expiry, swept client-side by every configured device.
  - **Republishing is incremental** — assets are named by content hash and
    therefore immutable, so editing a sentence in a note with 20 MB of images
    costs one small upload. Unpublishing deletes by listing the prefix, so an
    asset dropped from the note in an earlier publish cannot be left online.
  - **No `public-read` ACL by default.** R2 rejects ACLs and AWS Block Public
    Access fails the upload, so the usual default breaks the two most common
    targets; grant read with a bucket policy (a legacy toggle exists for older
    S3/MinIO). Path-style addressing is on by default for the same
    works-everywhere reason.
  - Bucket credentials live in the vault's replicated settings, so configuring
    one device configures them all and any device can unpublish — the settings
    screen says so before the keys are typed.
  - **Publishing works on iPhone and iPad**, not only on the desktop. The
    credentials you already configured replicate to the phone with the rest of
    your vault, so publishing a note there needs no extra setup. (Requests leave
    through the app rather than the web view, for the same reason clipping does:
    a bucket is a different origin, and a browser will not let the page talk to
    it directly.)

- **Backup & restore (Phase 7) — the feature that looked finished and was not.**
  The Settings panel, the per-account scheduler, the deduplicated attachment
  pool, rotation and garbage collection had all been built against a data engine
  that returned nothing: **every backup Hypha wrote was empty**, and it reported
  success. The engine half is now real, and the format is Hypha's own rather
  than an inherited shape.

  A backup is **your database's own ciphertext, copied out**. It is therefore
  always encrypted — there is no toggle to leave off, and no code path that can
  write a readable note into a synced folder — and it can be taken **while the
  vault is locked**, so scheduled backups run on a machine nobody has unlocked
  since boot. Your vault passphrase is what opens a backup, because it is the
  same data your vault holds.

  Restoring **merges** rather than overwrites. A backup replays through the same
  path a peer's sync data takes, so restoring an old backup onto a device you
  have kept using adds back what was lost without discarding this week's edits;
  restoring the same backup twice does nothing the second time; and a restore on
  one device converges with your others instead of being undone by them. Notes
  you deliberately deleted stay deleted.

  Because the notes travel encrypted, a backup belongs to the vault it came
  from. Restoring onto a fresh install adopts that vault, and your existing
  passphrase opens it — this is the disaster-recovery path. Restoring into a
  machine that already has a *different* vault is refused with an explanation,
  rather than importing notes that would list correctly and never open.

  Backups are named `<date>.hypha` (notes only, one file) and
  `<date>.hyphafull` (with attachments, a folder). Attachment blobs are stored
  once per account and shared across backups, so an unchanged attachment costs
  nothing on the next run.
- Initial Hypha repository bootstrap (Phase 0): brand-clean desktop shell with
  a stubbed data engine, clean-room editor, own-model contracts, and AGPL-3.0
  licensing. Local-first CRDT + P2P architecture scaffolded for the upcoming
  phases.
- Direction record for first-run onboarding and the sync/account model: Hypha is
  local-first and peer-to-peer with no central auth server — one vault
  passphrase is the only credential, and further nodes are paired as peers via
  `hypha://invite` tokens. README carries the same direction statement.
- **iOS app (`apps/mobile`) — runs on real hardware.** A Swift WKWebView shell
  around the *desktop renderer*, reused through per-file Vite alias swaps rather
  than a second UI: the sql.js/sqlite-wasm engine replaces the Electron SQLite
  bridge, and a swipe stack of Sidebar / List / Editor replaces the fixed
  three-column shell. Noise-XX stays inside the WebView — a `sodium-native` /
  `sodium-universal` shim over libsodium-WASM lets `@hyperswarm/secret-stream`
  run in a browser, wire-compatible with the desktop's native sodium — and the
  native side is only a byte relay (TCP via `Network.framework`, the UDP
  discovery beacon via BSD sockets, since `Network.framework` cannot broadcast).
  Verified end-to-end on an iPhone 17 Pro: the app boots, opens its vault, and
  its LAN transport reaches a desktop peer over real Wi-Fi. Seven headless
  smokes (`smoke`, `wire-smoke`, `sync-smoke`, `bridge-smoke`, `startup-smoke`,
  `cross-smoke`, `theme-smoke`) gate it without a device or a screen.
- **Headless relay daemon (`apps/peer`) — Phase 6.** A **ciphertext-only**
  store-and-forward relay, not a full replica: it holds opaque encrypted
  envelopes and can never read a note. `hypha-peer` CLI (`init` / `join` / `run`
  / `status` / `prune`), a `FileSecretStore`, durable SQLite opaque stores, a
  `daemon`-role first contact, a `systemd` unit and a multi-stage Docker image.
- **Tombstone and projection GC (Phase 8, §4l).** CRDT tombstones, removed
  edges and deleted notes' bodies were retained forever on every client — only
  the daemon's stores were ever pruned. Now a tiered reclaim that runs
  automatically in the app: **Tier 1** evicts a deleted note's body (Yjs
  snapshot, content row, FTS5 + vector index) past the trash retention period,
  slimming the row in place to a compact tombstone fact so LWW convergence still
  holds; **Tier 2** hard-deletes those facts once every recently-active peer has
  acknowledged them, using a per-peer acked frontier held back by a per-actor
  reorder window (the "committed-frontier witness", piggybacked inside the
  existing encrypted META batch — additive, no wire-version bump), with a local
  resurrection oracle rejecting a stale lower-HLC row that arrives after the
  fact is gone. A relay re-advertises its stored frontier so a peer's *own*
  tombstones become reclaimable in a star topology, and the oracle is bounded by
  a 90-day retention cap. Both tiers are kill-switchable at runtime.
- **Sync hardening (§4m).** HLC clock-skew convergence (a peer skewed +100s is
  absorbed via `observeRemote` instead of splitting the causal order); a
  cross-peer actor tiebreak so a tied `(wall, counter)` resolves to the same
  winner on both sides; and opt-in live-META push coalescing that collapses an
  N-write burst to at most two pushes without losing the final delta.
- **Vault passphrase rotation.** The passphrase now *wraps* the vault key
  instead of *being* it (key indirection), so it can be changed without
  re-encrypting the vault. An owner's rotation locks every other device out
  until it is re-invited, and the lockout is surfaced as something a person can
  act on rather than a decrypt failure. Invite wire v3 carries the vault key
  with the invite, so a re-invited device recovers in one step.

### Changed
- **The test suite is now typechecked.** Every other tree in the repo is; the
  tests were not, so a spec could call a method that no longer existed and only
  find out if that line happened to run. Turning it on found 62 type errors in
  one pass, four of which were tests quietly not testing what they claimed —
  including one that had been building a malformed link, and ten editor calls
  that were suppressing an update by passing an argument the editor stopped
  reading two major versions ago. All fixed; nothing in the app changed.
- **The editor's extension list has one definition**, `createEditorExtensions()`
  in `@hypha/editor-vue`. It used to be an array literal inside the renderer's
  `Editor.vue`, which meant a test could only approximate the editor people
  actually type into — and an approximation cannot catch a configuration the app
  gets wrong. Two specs had done exactly that: they registered the `hypha://`
  link protocol themselves while the app did not, so internal links were being
  stripped on load in front of a green suite. All four editor specs now build the
  app's real editor; the first run of the new one found a live defect (see
  Fixed).
- **Editor: Tiptap v2 → v3** (2.6.6 → 3.29.2). StarterKit's History extension was
  renamed `UndoRedo`, so the `history: false` disable became `undoRedo: false`
  (the rename was initially missed — see Fixed). StarterKit now also bundles
  `link` +
  `underline`, which are disabled here to keep the custom `hypha://` Link and
  Underline extensions (avoids the "duplicate extension names" warning). `editor.storage`
  is typed strictly in v3, so storage reads are bridged with `as unknown as
  Record<…>`. `setContent(html, false)` is now `setContent(html, { emitUpdate:
  false })`. `TextStyle` and `Table` moved to named exports. Refractor 4 → 5.
- **IPC: tRPC v10 → v11**. Upstream `electron-trpc` is tRPC-10-only and dormant,
  so both halves are vendored from scratch to speak tRPC 11 while keeping the
  upstream wire protocol (so the preload's `exposeElectronTRPC()` is unchanged):
  `src/renderer/src/platform/ipc-link.ts` (terminal link; v11 empties the link
  runtime so the transformer is read per-link) and `src/shared/electron-trpc-handler.ts`
  (`createIPCHandler` via v11 `callProcedure` / `getErrorShape` /
  `getTRPCErrorFromUnknown`, with full subscription lifecycle and per-`webContents`
  teardown). `@trpc/server` / `@trpc/client` ^11.18.0 added. The third piece,
  `exposeElectronTRPC`, was initially loaded from upstream through
  `createRequire`; it is now vendored into `electron-trpc-shim.ts` as well, so
  the preload has no runtime dependency outside `electron` (a hard requirement
  of the renderer sandbox — see Security).
- **Renderer sandbox: the preload is CommonJS (`out/preload/index.cjs`)**, not
  ESM. Electron loads a sandboxed preload as CJS only. If you add an import to
  the preload, it must resolve to `electron` or be bundled — a bare import of
  anything else breaks the bridge at load time, and the symptom (every
  `desktop.*` call failing with "Could not find electronTRPC global") points
  nowhere near the cause.
- **Sync is per vault.** `desktop.sync.*` procedures take an optional `ctx`; main
  keeps one coordinator session per vault context rather than one globally. See
  Fixed for what that repaired.

### Removed
- **A dead storage layer inherited from the fork.** `NNStorage` — an IndexedDB
  key-value store with its own password-crypto and PGP surface — was built on
  every launch, on desktop and iOS, and then dropped: the data engine never read
  the option it was passed in. It reached nothing and nothing reached it. Gone,
  along with the rejecting `NNCrypto` shim it called, the KV store behind it, the
  `IStorage` contract that described it, and the key store that existed only to
  feed it. Hypha's key-value data lives in the CRDT store, and its secrets live
  in the OS keychain.

  Nothing was ever written to those IndexedDB databases, but earlier builds
  created an empty one per vault. Removing a vault still deletes it, so they
  clear themselves as you go; a leftover is inert either way.
- **Everything else that was wired to nothing.** The same question asked of every
  remaining option the data engine is handed — "does anything ever read this?" —
  removed four more: a gzip compressor (built on every launch, on both
  platforms, with its own IPC channel to the main process), a server-events
  adapter and the dependency behind it (Hypha has no server), and two settings
  the engine ignored. None of it was reachable from the app; the one part that
  *was* reachable turned out to be the broken attachment backup under Fixed.

### Security
- **A second barrier around clipped web pages.** Clipping a page brings someone
  else's HTML into the app, and the app strips anything dangerous out of it
  before it is ever shown. That strip was the only thing standing between a
  booby-trapped page and your notes database. The app window now also refuses,
  at the browser level, to run *any* script that did not ship with Hypha — so a
  script that somehow survived the strip still cannot do anything. This changes
  nothing you can see. **iPhone gets the same barrier**, which matters more
  there: the phone can clip pages too, and until now the strip was the only
  layer on that side.

### Fixed
- **Opening a note re-downloaded the whole note, every time.** When Hypha asked
  another device (or your always-on relay) for a note's contents, it always
  asked for *everything* — even for a note it already had and had only come back
  to. On a long note with a long editing history that meant sending the whole
  thing again on every open, on every device, forever. It now asks only for what
  it is actually missing, and the relay keeps track of what it has already sent
  you rather than replaying a note's entire history. A device that has genuinely
  lost a note still gets the full copy: it says so, and is sent everything. You
  should see this as notes opening quicker over a slow connection, and as much
  less network traffic on a busy vault.
- **Two devices on the same network flooded it with discovery traffic.** Hypha
  announces itself on the local network once a second and answers announcements
  it hears, so that a device whose announcement can't reach you still gets found.
  Nothing stopped it from answering an *answer* — two devices talked each other
  into roughly 43,000 packets a second. On a Mac that quietly burned CPU; on an
  iPhone it jammed the app's main thread and could freeze it. Answers are now
  limited to one per device per second, which is enough for discovery and cannot
  run away.
- **A deleted reminder kept firing on your other devices.** Deleting a reminder
  removed it here and told no one. Every other device kept the reminder and kept
  notifying you at its scheduled time, with no way to stop it from the device you
  deleted it on — and no later sync could fix it, because the deletion was never
  recorded as one. Deletions now travel, and the reminder's link to its note goes
  with it. The same bug had one more edge: a reminder never displayed the note it
  was attached to, on any device.
- **Unpinning a shortcut only unpinned it here.** A shortcut removed from the
  sidebar on one device stayed in the sidebar on all the others, permanently.
  Pinning had the mirror problem in a milder form — a new shortcut did reach your
  other devices, but their sidebars did not show it until the app restarted.
  Both now update everywhere, as they happen.
- **An attachment whose file never arrived stayed broken forever.** Your devices
  send a note's *record* and its *file* separately, and the file was asked for
  only once, from a single device, at the moment the record arrived. If that
  device went offline mid-transfer, or the record came via one that didn't have
  the file, or your own device restarted in between, nothing ever asked again —
  the attachment listed correctly and never opened, on that device, permanently.
  Every device now asks for the files it is missing each time it connects to
  another one, so an interrupted transfer finishes itself. This also puts those
  files back into your backups (see below).
- **A "with attachments" backup never contained an attachment.** The engine
  writes the notes and names each attachment it references; copying the actual
  files is the app's job, and the app's half was a placeholder that reported
  "not stored on this device" for every one of them. So a `.hyphafull` backup
  held every attachment's *record* and none of its *data*, and restoring one put
  the records back and left every image and document unopenable — reported, both
  times, as a count in a log nobody reads. Backups and restores now move the
  files themselves, through the same path attachments already travel between
  your devices. Previously written full backups are unaffected by the fix: the
  files were never in them. Take a fresh one.
- **iOS: a joined vault's notes were invisible until you wrote a note yourself.**
  A merged peer batch reached SQLite and refreshed nothing — the notes list, the
  sidebar, the trash view, the open editor and the "last synced" stamp all
  reload off `syncItemMerged`/`syncCompleted`, and on mobile nothing published
  them. On the desktop those announcements live in the renderer's sync seam
  server, which every remote apply crosses on its way from Electron main; the
  mobile coordinator runs inside the WebView with the engine seams wired to it
  directly, so it crossed nothing. Both hosts now go through one shared module,
  so a remote note, a remote body edit and a remote tag assignment all appear as
  they arrive — and an editor open on the same note reloads instead of sitting
  on stale text.
- **iOS: no keyboard, in any field.** `Info.plist` specified a launch screen with
  an empty colour name, which is not a valid specification — so iOS ran the app
  in compatibility mode, and on iOS 27 an app in that mode is never given a
  keyboard session at all: tapping a field showed a caret and an accessory bar
  and no keys. (Native text fields in the same app were equally mute; Safari on
  the same device was fine. iOS 26 tolerated it.)
- **iOS: the app began below the notch, under a black bar.** The web view's
  scroll view was insetting the page by the safe area, which also zeroed the
  `env(safe-area-inset-*)` values the mobile shell pads itself with — so the
  padding written for the notch did nothing and the strip above the page showed
  the native view's background. The page now owns the whole screen and paints it,
  including the strips around the notch and the home indicator.
- **iOS: the app could freeze and go blank while a peer typed in the same note.**
  Persisting the database copies the entire thing out of the WASM heap and writes
  it to OPFS. Requests were not serialized, so a sustained write burst (every Yjs
  update from a peer writes a snapshot) started a new full-size copy every 250 ms
  before the previous one had finished, until the WebContent process was killed
  for memory — which looks, from the outside, exactly like a frozen app. Flushes
  now coalesce into a single trailing pass, read-only queries no longer schedule
  one at all (every list scroll and search keystroke was re-serializing the whole
  vault), the app flushes when it leaves the foreground instead of losing the
  last quarter-second of writes, and if the process is killed anyway the shell
  reloads the renderer rather than showing a dead view.
- **The restore file picker could not see backup files.** Both the save and the
  open dialog filtered for a file extension left over from the project this
  shell was forked from — one Hypha has never written. Choosing a backup to
  restore showed an empty folder. Fixed with the Phase 7 naming pass; backups
  are `.hypha` / `.hyphafull` throughout.
- **Two undo systems ran in every editor.** Hypha's undo is y-prosemirror's
  collaborative `UndoManager`, which reverts only your own edits and leaves a
  peer's alone. TipTap 3 renamed StarterKit's local undo option from `history` to
  `undoRedo`, and the upgrade dropped the disable rather than renaming it — so
  `prosemirror-history` kept a second, non-collaborative undo stack of every
  change to every open note. The keyboard was unaffected (the collaborative
  keymap registers last and wins Mod-z, now pinned by a test that fires a real
  Mod-z with a peer's edit applied), so this cost memory and left a latent
  `editor.commands.undo()` that would have undone the wrong thing; it is gone
  from the shipped bundle entirely. Found by giving the test suite the app's real
  extension list — see Changed.
  Main held a single global coordinator session, and `start` returned success the
  moment one existed. Since every vault window runs its own `startSync()`, the
  second vault got success back without a room being joined and without a seam
  port — its syncer then timed out and started no seam server at all. The
  converse was equally bad: locking or switching context in *any* window stopped
  whichever vault happened to own the global session, permanently. Sessions are
  now keyed by vault, and each call names the vault it means. Related: the seam
  port was handed to the main window regardless of which window asked, so a
  non-main vault window listened for a port it never received.
- **Closing the last window on macOS left the app running but inert.** The dock
  `activate` handler created a window and re-registered nothing, so sync could
  never start again (`getMainWindow()` stayed undefined), `hypha://` links went
  nowhere, cross-window refresh was dropped, and the tray's menu items pointed at
  a destroyed renderer. All window-bound wiring is now re-established on
  `activate`, and the registrations it calls were made genuinely idempotent — the
  tray in particular would otherwise have left one dead icon per dock-reopen.
- **A torn-off note window auto-locked on its own schedule and took the main
  window's database with it.** Note and pane windows armed the idle auto-lock
  timer despite a comment saying they did not; locking calls `db.close()`, and
  main shared one SQLite handle across every renderer, so the main window's next
  save failed with `Database not found for id: hypha-local` and every query after
  it failed until a manual reload. The handle is now ref-counted by the windows
  holding it (including a release when a window is destroyed without closing
  cleanly), and only the main shell window arms auto-lock.
- **A dead renderer hung the sync coordinator silently.** The main→renderer seam
  had no close handler and no per-call timeout, so when the seam-owning window
  went away every pending call stayed pending forever and the coordinator simply
  stopped. Pending calls now reject with a named `SyncSeamError` on close, and
  each call is bounded at 30 s for the other case — a renderer still alive but
  wedged, which emits no close event at all.
- **Auto-backup never tracked a fresh install's main-window size**, because only
  the session-restore path attached the bounds listeners.
- **Bulk wire length prefixes widened to u32 — a silent `u16` overflow corrupted
  every payload over 64 KiB. This changes the wire format; peers must share a
  build.** `lpBytes`, the length prefix on every bulk byte field (ciphertexts,
  attachment blobs, opaque carrier payloads), was `u16`, and the encoder *masked*
  rather than range-checked: a 70,000-byte META_STATE ciphertext wrote a length
  of `70000 & 0xffff` = 4464 and then appended all 70,000 bytes. The frame
  envelope's own `u32` header stayed correct, so the receiver handed a
  full-length payload to a decoder that consumed only the 4464 the inner prefix
  claimed and threw on the remainder. It surfaced as an iPhone reporting
  "trailing bytes in META_STATE", but it was never a mobile bug — the phone was
  simply the first peer to sync a vault whose META_STATE exceeded 64 KiB. **It
  was worse on desktop:** the coordinator bounds attachment blobs at 16 MiB, so
  every attachment above 64 KiB — in practice every image — was silently
  corrupting on the wire with no error on either side. Bulk fields now carry a
  `u32` prefix; short bounded identifiers (note ids, actor ids, hashes) keep
  `u16` behind a separate `lpShort`/`readLpShort` pair. Both widths now
  range-check in *both* directions, so an oversize field throws at encode time —
  silent truncation is not the failure mode again. A build mismatch between two
  peers fails loudly (an old `u16` prefix read as `u32` yields an absurd length →
  `truncated field`), never silently. Regression tests straddle the old ceiling
  (65,534 / 65,536 / 70,000 / 300,000) across META_STATE, ATTACHMENT, YJS_UPDATE
  and SYNC_REQUEST, plus a 200 KB frame pushed through `FrameReader` in
  1500-byte chunks.
- **An unauthenticated peer could reach handlers behind the HELLO gate.** Frame
  dispatch consulted "is this the first frame?" rather than an explicit
  `verified` flag, and `FrameReader` did not await its callback, so the decode
  loop did not serialize — `HELLO(bad credential) ‖ ATT_REQUEST` written as a
  single TCP write ran the `ATT_REQUEST` handler before the credential's
  *asynchronous* signature check failed. Dispatch now gates on `verified` and the
  reader awaits, so frames after a failed HELLO are never dispatched.
- **A malformed frame killed the process.** A decode error thrown inside a
  stream `data` listener had no catch; `FrameReader.push` now catches and drops
  the connection instead.
- **Wire-supplied attachment hashes are validated as `/^[0-9a-f]{64}$/`** at the
  sync-store boundary *and* again inside the blob storage layer, so a traversal
  path in an `ATT_REQUEST` or `ATTACHMENT` frame cannot escape `blobs/`. The
  daemon does not trust its caller either.
- **Five async seams that could interleave into corruption** (`applyMetaBatch`,
  the Yjs H8 path, `openDoc`, the dirty flag, the invite nonce) were closed;
  `Engine.transaction` now hands its callback an `EngineTransaction` so a
  transaction's repository is an argument rather than ambient state that a
  concurrent caller could swap underneath it.
- **A note opened before its peer was discovered stayed stale forever.**
  `openNoteForSync` pulled only from peers connected *at call time*, on every
  platform. Relatedly, `onLocalMetaChange` recorded a peer's frontier *before*
  sending, so a failed push over-claimed what that peer held for the life of the
  connection.
- **Sync errors are no longer silent.** The coordinator's error channel now
  names the decrypt failure and every host subscribes to it — an `EventEmitter`
  `"error"` with no listener is thrown, not swallowed.
- Settings and Changelog windows no longer fall back to the full shell boot.
  Those windows run a minimal boot, but their `encryption.refresh()` silently
  unlocks the vault via the keychain, flipping `isUnlocked` — which fired
  `presentShell()` inside the settings window and clobbered the `/settings`
  route. The `isUnlocked` watch now also guards against `isSettingsWindow` /
  `isChangelogWindow`.
- **Invites: minting no longer fails with "incomplete input".** The room secret
  is stored/encoded by the renderer as standard *padded* base64 via `btoa`
  (`platform/room-secret.ts`), but `encodeInviteUnsigned` decoded it with
  libsodium's *default* `from_base64` variant — `URLSAFE_NO_PADDING` — which
  rejects `btoa` output (the `=` padding / `+` / `/`) with "incomplete input", so
  every "Generate invite" threw and surfaced as red error text. Pinned the
  `ORIGINAL` (standard padded) variant for the roomSecret in
  `packages/crypto-own/src/encoding.ts` (both encode and decode) to match the
  renderer's `btoa`/`atob`, and declared `base64_variants` in the libsodium
  type stub. The signed bytes (the decoded 32-byte secret) are
  variant-independent, so this changes no signature or wire format and no
  keychain storage format — existing installs/secrets are unaffected. The
  contract tests (`invite.spec.ts`, `invite-url.spec.ts`, `p2p-frames.spec.ts`)
  generated the room secret with libsodium's own `to_base64` (matching the
  default), which masked the bug; they now use standard base64 to exercise the
  real production path.
- **Devices: a fresh device no longer silently becomes its own "owner".** Boot
  sync (`P2PSyncer.start`) called `getRoomCredentials` unconditionally, which
  auto-generates `ownerKey:<ctx>` + `roomSecret:<ctx>` on first call — so as
  soon as the vault was unlocked on first run, every fresh device minted an
  owner key and flipped to the "owner" role, hiding the "Join a room" UI (the
  `devices` section's pending block is `v-if="isPending"`). `start` now bails
  (returns `false`, P2P off) unless the context holds an owner private key
  (`hasOwnerKey`), keeping pending devices pending. This also protects members:
  `getRoomCredentials` is owner-only (it signs an *owner* credential), so a
  member reaching it would auto-generate a bogus owner key and corrupt the
  member into an owner on the next boot. Member→owner P2P sync remains the
  5c-4 follow-up. Note: an instance already corrupted by the prior behavior
  (spurious `ownerKey:local` + a stale owner row seeded in the `devices` CRDT)
  must be reset by wiping its userData — the fix prevents new corruption, it
  does not un-corrupt an existing instance.
- **P2P editor sync: edits no longer stop broadcasting after switching away
  from a note and back.** The broadcast trigger (`YjsSyncStore.onUpdate`) bound
  a `doc.on("update")` listener to the `Y.Doc` *instance* captured at subscribe
  time, and the editor destroys + recreates that `Y.Doc` on note switch
  (`YjsStore.closeDoc` → the next `openDoc` mints a fresh doc with a new Yjs
  `clientID`). The coordinator's `openNoteForSync` subscribed only once per
  note, so after a close/reopen the listener stayed bound to the destroyed doc
  — local edits on the live doc fired the store's flush listener but never
  reached the broadcast callback, so the peer silently received nothing
  (one-directional; macOS logs showed `[yjs-store] update` with a growing
  fragment but no `[sync] applied:yjs` on the other device). Fixed at the
  store level: `YjsStore` now keys local-edit subscriptions by `noteId`
  (`updateCbs`) and `openDoc`'s per-doc `update` listener re-dispatches each
  genuinely-local edit (origin ≠ `REMOTE_ORIGIN`, so remote applies + the
  cross-window `reloadDoc` merge are still not re-broadcast) to that set, so a
  subscription survives doc recreation by construction. The data-engine seam
  delegates to `YjsStore.onUpdate` instead of capturing a doc instance, and the
  coordinator's one-shot subscribe is now sufficient. Regression test in
  `sync-yjs-convergence.spec.ts` (close/reopen without re-subscribing → the
  peer still receives the next edit) times out against the old seam and
  passes with the fix.
- **Editor: switching to a note with no Yjs snapshot no longer leaves the
  previous note's body visible.** `bindYjsDoc` rendered the bound fragment into
  the editor only when it already had content (`fragment.length > 0`), skipping
  the render for an empty fragment — a workaround (`ae9558a`) for
  `_forceRerender`'s dispatch dropping the `ySyncPlugin`. That drop is now
  prevented by the `editor.state` shadow fix (the dispatch applies against the
  live, plugin-bearing state), so the skip is obsolete. Removing it makes the
  swap render the (empty) fragment unconditionally, clearing the prior note's
  content on note switch instead of leaving it visible until the caller's
  `setContent` overwrote it. The `yjs-live-binding.spec.ts` swap test
  (rebind to an empty doc → the prior content must not leak) now passes.
- **Sync: tag associations no longer ghost / duplicate across peers.**
  `meta_edges` rows are keyed by a deterministic PK that *encodes direction*
  (`${fromType}:${fromId}|${toType}:${toId}`), and the LWW upsert gate only
  dedups rows with the same PK. The read path commits to `tag→note` /
  `color→note` / `notebook→note` direction
  (`stores/notes.ts`, `stores/properties.ts`), but `bootstrap.ts` seeded the
  welcome-note tag as `note→tag` — the opposite direction. Two consequences:
  (a) the seeded "phase-3" tag silently failed to filter its welcome notes
  (the `from({tag},"note")` read never matched a `note→tag` row), and (b) if
  a user later removed the tag, `unlink({tag},{note})` wrote a `tag→note`
  remove under a *different* PK, so it could not tombstone the reversed add —
  the `note→tag` `op=add` row survived as a ghost that replicated via META sync
  and could reappear as a duplicate association. Fixed on three fronts:
  `bootstrap.ts` now writes `add({tag},{note})`; `CrdtRepository.normalizeEdgeRow`
  (`packages/crdt-store/src/repository.ts`, called from `upsertEdgeRow` — the
  single chokepoint for local + remote writes) canonicalizes any `note→tag`
  row to `tag→note` on write, so a reversed edge from an un-upgraded peer
  can't survive (directed `note→note` / `notebook→notebook` edges are
  intentionally left untouched); and a one-time kv-gated migration
  `flipReversedTagEdges` (`packages/crdt-store/src/migrations/flip-tag-edges.ts`,
  gated by `tag_edge_direction_flipped` in `packages/data-engine/src/db.ts`)
  flips pre-fix reversed rows already on disk, merging under the LWW gate
  with original hlc/actor preserved. Pinned by `sync-associations.spec.ts`
  (round-trip through the real facade contract, no-dup-on-reapply, color
  reassignment, notebook add/remove) and `edge-set.spec.ts` (normalization +
  flip). The `sync-meta-convergence.spec.ts` tag edge is aligned to the
  `tag→note` convention so the suite models the real direction.
- **Sync: a note synced to a peer is now searchable there without opening it.**
  The `text_index` (FTS5) and `vec_notes` (semantic) projections are Yjs-derived
  with no write trigger; the only indexer was the editor's `flushSave`, so a note
  that arrived via META sync was absent from the receiver's search index until
  the user opened + edited it there (and a tombstoned note wasn't removed from
  the receiver's index). This silently degraded search after every sync — a gap
  the roadmap's "search = projection rebuilt off Yjs update events" thesis
  covered locally but not on the receive side. `MetaSyncStoreImpl.applyMetaBatch`
  (`packages/data-engine/src/sync-seams.ts`) now reindexes notes touched by a
  remote META batch via a new `LookupFacade.reindexNote` (note row → index/remove;
  content row → reindex the owning note), best-effort so a projection failure or
  locked content never breaks apply. `noteIdOf` is shared from
  `@hypha/data-engine` (the renderer's duplicate is removed). Pinned headlessly
  by `sync-remote-reindex.spec.ts` (create-on-A → searchable-on-B with no editor
  open; trash-on-A → dropped from B's index; content update → reindex to the new
  term). Also added `sync-settings.spec.ts` (the `settings` CRDT table
  round-trips, previously untested), `sync-tombstone.spec.ts` (tombstone sync +
  LWW resurrection semantics: a stale lower-HLC live row doesn't resurrect, a
  fresh higher-HLC live row does — pinned as intended), and an encrypted-mode
  association round-trip in `sync-associations.spec.ts`.

### Security

The renderer trust boundary, hardened. Every item here assumes the realistic
threat: content that arrives from a synced peer or an imported archive is not
content this device wrote.

- **"Open externally" no longer hands a peer-chosen filename straight to the OS.**
  `shell.openPath` dispatches on the extension and nothing else, and both callers
  pass a name from off-device — a synced attachment's filename, or a `file:` link
  stored in synced note content. An attachment called `Invoice.pdf.exe` ran on
  click, on Windows, with nothing shown to the user. Known-inert document and
  media types still open directly; anything else now raises a confirmation with
  Cancel defaulted, worded specifically when the type is one we can identify as a
  program. The classification is an allowlist rather than a list of bad
  extensions, and normalises the usual disguises (trailing dots and spaces, which
  Windows ignores; case; right-to-left override characters that make `.exe`
  render as `.png`).
- **Release notes and changelogs are no longer rendered as raw HTML.** The
  markdown renderer preserved HTML by design, and both of its `v-html` sinks are
  fed from the network (the repository's `CHANGELOG.md` and the update feed's
  release notes). Input is now escaped first and the only tags in the output are
  ones the renderer writes itself; link targets are restricted to
  http/https/mailto, with anything else degrading to plain text. `>` blockquotes
  are supported now, which is what the HTML passthrough was really there for.
- **Backups and imports are confined to a directory the user actually picked.**
  Both APIs enforced containment against a root the *renderer* supplied on every
  call, which is not containment at all. Main now records what the native folder
  picker returned and checks against that, resolving symlinks so a link planted
  inside a chosen folder is not a way out of it. **Upgrade note:** a backup
  directory configured before this release is not in that record — the first
  backup will fail with a message asking you to choose the folder again in
  Settings → Backup, after which it resumes normally.
- **The renderer runs in the OS sandbox** (`sandbox: true`) with Node integration
  off. The Node flag granted nothing in practice — with context isolation on,
  `require`/`process`/`Buffer` are already undefined in the renderer — but it was
  a latent escalation waiting for someone to relax context isolation. Note that
  this does not contain a renderer compromise on its own: the tRPC bridge is
  exposed to the page by design, which is why the injection sources above were
  removed rather than merely filtered.
- **Links in a note can no longer name any scheme they like.** The `link` mark
  overrode TipTap's render step without calling the original, which dropped its
  URI check — so a link mark arriving from a peer rendered as a live anchor for
  `javascript:`, `data:`, `file:` or anything else. The check is back, and it is
  the only one that runs on the sync path: synced notes are loaded as structured
  data, not HTML, so nothing else inspects the address. `target` and `rel` are
  now decided by the app rather than by the note's content, which means an
  external link always carries `noopener noreferrer nofollow` even if the stored
  mark says otherwise. *Consequence:* the "Link to file" option in the link
  picker now renders an inert link. It never worked — the address it produced was
  missing the folder — and it will either be removed or reconnected through the
  guarded "open externally" path.
- **Internal `hypha://` links survive opening a note.** The protocol was never
  registered with the link mark, so every internal link was stripped the moment a
  note without a sync snapshot was opened — and because that stripped document is
  what gets saved and broadcast, the links were gone on every device, silently
  and permanently. Linking selected text to a note also did nothing at all. The
  protocol is now part of the mark itself rather than something each call site
  has to remember to configure.
- **SQL that names a file is refused.** The database layer advertised that a
  compromised renderer could not point SQLite at an arbitrary path, but enforced
  that only on the `open` call — `ATTACH DATABASE '/anywhere'` and `VACUUM INTO
  '/anywhere'` walked straight past it. Both are now rejected at statement
  preparation. The handle also runs with SQLite's defensive mode on, which
  refuses direct writes to full-text-index internals and to the schema table.

### Tooling / Dependencies
- **CI: every GitHub Action is pinned to a full commit SHA**, with the version in
  a trailing comment. A `@v5` tag is a moving pointer its owner can repoint at
  any commit; these jobs hold a token and build the binaries users download.
- **Dropped `npm install -g npm@latest`** from the release and packaging jobs.
  Node 24's bundled npm already matches the lockfile generator, and installing an
  unpinned "latest" into the toolchain that produces shipped binaries defeats the
  SHA pins above.
- **The root `typecheck` covers every workspace.** It was a hand-maintained list
  of 10 `--workspace=` flags that omitted `apps/mobile` (the active workstream)
  and the three Vue packages; it is now `npm run typecheck --workspaces
  --if-present`, so a new package is gated the day it is created. Coverage went
  from 10 workspaces to 15. `packages/{shared,theme-vue,ui-vue,editor-vue}` gained
  the `tsconfig.json` (and, for the two with `.vue` files, the `vue-tsc`) this
  needs — `packages/shared`'s `typecheck` script had silently checked *nothing*
  for its whole life, having no config to find.
- **The UDP LAN-discovery spec no longer broadcasts on every test run.** It bound
  a fixed, topic-derived port and put real packets on whatever network the
  machine was attached to; it is now `p2p-udp-beacon-live.spec.ts`, gated behind
  `HYPHA_LAN_LIVE=1` like the other live specs. The topic → beacon-port
  derivation — which the iOS native side re-implements, and where a silent
  disagreement means LAN discovery just never works — is pinned offline instead
  by a new `p2p-lan-ports.spec.ts`.
- Broad toolchain bump: typescript ^5.9.3, `@types/node` ^26, eslint ^10
  (+ `@eslint/js`, `globals`), vitest ^4, happy-dom ^20, `@electron/rebuild` ^4,
  vue ^3.5.40, kysely ^0.29, libsodium-wrappers-sumo ^0.8, `@lucide/vue` ^1.28,
  tailwind-merge ^3.6.
- `tsconfig`: dropped `baseUrl` and made all `paths` explicitly relative; added
  `typeRoots` + `types: ["node"]` to the `data-engine` / `p2p` / `sync` tsconfigs
  so the hoisted `@types/node` ^26 resolves reliably.
- `scripts/rebuild-electron.mjs` now fetches the Electron binary itself when
  missing (`path.txt` absent) — Electron 43+ ships its downloader as a `bin`
  with no postinstall, so a fresh `npm install` left the binary unfetched and
  `electron-vite dev` died with "Electron uninstall". Keeps `npm install &&
  npm run dev` self-contained.
- `scripts/rebuild-electron.mjs` (the `predev` hook) no longer rebuilds
  better-sqlite3 on every `npm run dev` — it probes the existing `.node`'s ABI
  and skips when it's already built for the current Electron. The probe loads
  the binding under the host Node: if it loads, it's a Node-ABI build (e.g.
  left there by `npm run test:contract`'s `pretest` `npm rebuild`, which
  overwrites the same `.node`) → rebuild for Electron; if it fails with a
  `NODE_MODULE_VERSION` mismatch, it's an Electron-ABI build, and a marker
  (electronVersion + arch) gates against an `electron` upgrade → skip. This
  keeps the dev/test ABI flip-flop safe (a naive marker would skip after tests
  and ship a Node binding Electron can't load). `HYPHA_FORCE_REBUILD=1` forces
  a rebuild; the actual rebuild stays `force: true` + `useCache: false`
  (deterministic for release).
- `electron-builder.yml`: `npmRebuild: false` is now retained intentionally
  (deterministic Electron-ABI pre-rebuild via the explicit rebuild script),
  not just as the old electron-builder v25 prune-bug workaround.
- `i18n-po.mjs` preserves the error cause chain (`{ cause: err }`).
