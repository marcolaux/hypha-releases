# Changelog

All notable changes to Hypha are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

**Entries are SHORT — one or two sentences.** What changed, and what it means
for someone using the app. No mechanism, no measurements, no reasoning about
why the old behaviour was wrong: those belong in the commit message, which is
where anyone asking "why" will look. Entries here are the release notes, and
the desktop *What's New* window shows them verbatim to people who just want to
know what is different. Versions 0.1.0–0.13.0 were written before that rule and
were shortened to it on 2026-08-27, almost entirely by truncation: of the 160
entries that got shorter, 155 are a strict prefix of what they said before. The
other five were compressed rather than cut, so they are the only places the
wording is not the author's own — checked, and none of them changed what the
entry claims. Every published correction and every "this is not an automatic
upgrade" warning was checked back in by hand afterwards.

## [Unreleased]

## [0.21.1] - 2026-09-06

### Fixed
- **A note you deleted can no longer come back as an "Untitled" copy of itself.**
  Trashing the note you had open left the editor bound to it, and a write from
  that pane could recreate the note — including one already emptied from the
  trash, which returned with no title and its old text. Trashing, permanently
  deleting and emptying the trash all hold now.
- **On the phone, trashing the note you are reading takes you back to the list**
  instead of leaving the editor on a blank "New note", and swiping back no longer
  lands on a note you just deleted.
- **Moving an archived note to the trash now updates every list at once** — All
  Notes, Archive, Trash and any other open window.

### Changed
- **Emptying the trash now reclaims the note on all your devices, not just the
  one you pressed it on.** Until now the other devices kept the note in their
  own trash, with its full text, indefinitely.

## [0.21.0] - 2026-09-05

### Added
- **Select a whole list with Cmd/Ctrl+A, and send a selection to the trash with
  Backspace or Delete.** Both work from the notes list, Archive and (select-all
  only) Trash, including when you got there by clicking a notebook, tag or
  colour in the sidebar and focus never left it. Deleting still asks first, and
  Delete does nothing in the Trash — emptying it keeps its own button.
- **The desktop titlebar shows the vault you are in**, between the version and
  the QR button. It updates when you switch vault, and on a vault you joined it
  updates again when the owner's name arrives over sync.
- **Drag a block by its grip.** Hovering any block — a paragraph, heading,
  quote, code block, table, image, rule or list row — shows a handle in the left
  margin; drag it to move that block anywhere in the note, including from one
  list into another, where the row takes on the destination list's kind instead
  of jumping out of it. A list row carries everything nested under it, and you
  can drop in the margin without moving back over the text.
- **Move a block with Cmd/Ctrl+Alt+Up/Down.** The keyboard version of the same
  move: the list item the caret is in — with everything nested under it — or the
  paragraph, heading, image or list it is in, one place up or down. It stops at the
  ends of a list rather than lifting the item out; Tab and Shift+Tab are still
  how you change level.

### Changed
- **The editor toolbar's move up / move down buttons are gone**, replaced by the
  drag grip above. The keyboard shortcut is unchanged.
- **There is one checkbox list instead of two.** The app had a second checklist
  beside the task list; once due dates moved into the item's own text the two
  were identical, so they are now one. Existing notes are converted as they
  open, on every device, and nothing is lost — a converted note is the same list
  with the same items, ticks and due dates. A customised toolbar keeps its
  button.
- **Text in the app's own interface no longer highlights when you drag across
  it.** Menus, lists, the sidebar, settings and dialogs behave like an app
  rather than a web page. Note content, anything you type into, and code and
  file previews still select and copy as before. Phone unchanged.
- **Enter now confirms a confirmation dialog**, and the confirm button is what
  opens focused. The exception is the handful of actions that cannot be undone
  — emptying the trash, deleting from it, removing a vault, deleting an
  attachment, changing the passphrase, restoring stock themes — where Cancel
  still opens focused and Enter will not perform the action. Escape always
  cancels.
- **The omnibar no longer slides under the version and QR button** when you
  make the window narrow. It gets shorter instead.
- **Desktop Settings shows one vault at a time.** Instead of listing every
  vault's sections one after another, it opens on the vault you pressed Cmd+,
  in and shows that vault's settings plus the device-wide ones — with a vault
  picker at the top of the sidebar to change which. The phone has always worked
  this way.
- **The desktop editor toolbar now follows the phone's order.** Undo/redo
  first, then block structure, inline formatting, block containers, and
  everything that inserts — and it gained the five tools the phone had and it
  did not: simple checklist, task due date, web link, audio/video and insert
  date. Nothing was removed. If you have customised your toolbar you keep your
  own layout; Settings → reset picks up the new one.
- **The two link buttons are told apart.** Linking to another note now draws a
  page rather than a second chain, and no longer appears twice.

### Fixed
- **Highlighted text is readable again.** Highlighting in a dark theme left
  white text on a bright yellow band; the text on a highlight now takes its
  colour from the highlight, so every swatch — and any colour you pick yourself
  — meets the contrast standard.
- **Adding an embed puts the cursor straight in the address field**, an embed
  now fills the width of the note instead of stopping a little short, and its
  resize corners sit on the edge where you can actually grab them.
- **Embedded players actually run now.** An embedded page was walled off from
  its own cookies and storage, so YouTube, Vimeo, Spotify and anything else that
  keeps state loaded as a black rectangle — and YouTube additionally answered
  *Error 153* because the frame sent no origin. Embeds still cannot open
  windows, navigate away from the app, or reach anything in it, they are still
  told nothing about which note they are in, and nothing is fetched until you
  turn embeds on.
- **YouTube, Vimeo and Spotify links now play inside the note.** Pasting a
  video's page address used to give a blank box — those sites refuse to be put
  in a frame on that address. The embed now points at the one they publish for
  it, while the note still remembers the page you chose. An address those sites
  will not show at all — a home page, a channel, a profile — is now declined by
  the address field, which says so, instead of becoming an empty rectangle.
- **Undo works on checklists again.** Making a checklist — Cmd/Ctrl+L, typing
  `[] `, pasting one, or converting a list — was invisible to Undo, which
  skipped past it and undid an earlier edit instead. Every way of making one is
  now a normal undo step.
- **Clicking the corner of an image no longer counts as editing the note.** A
  click that moved nothing used to resize the image to the size it already was,
  which marked the note edited and moved it up a list sorted by that. Only a
  real drag changes anything now.

### Added
- **Put a web page in a note.** The toolbar's *Embed* button, `/embed` and the
  command palette now insert one — type or paste an address and the page
  appears in the note. Drag a corner to resize it, double-click a corner to put
  it back. It is on the phone's format bar too.
- **Settings → Global → Privacy → *Load embedded web pages in notes*.** Off by
  default: an embedded page shows a placeholder naming the site with a "Load
  page" button, and nothing is requested until you load it. Separate from the
  external-images setting, because an embedded page is a whole site's code
  running on your device every time you open the note.
- **Import a Standard Notes backup folder.** Settings → Import reads the
  encrypted backups the Standard Notes app writes on a schedule — pick the
  folder, choose which backup when there is more than one, and enter your
  account passphrase. Notes, nested tags, attached files, pinned and archived
  states, note links and the original dates all come across, and anything that
  was in the trash stays in the trash.
- **`Cmd/Ctrl+L` for checkboxes.** Press it on a line to turn it into a
  checklist item; press it again inside one to tick and untick it. It works in
  both kinds of checklist.
- **Tables can be wider than the editor.** *Table ▸ Wider than the editor* (in
  the right-click menu, or the toolbar's table button) lets one table use the
  full width of the tab and scroll sideways, its header row staying in view as
  it does. Column widths are saved with the note either way.
- **The relay daemon can remove a vault: `hypha-peer leave <context>`.** The
  inverse of `join` — it drops that vault's secrets, its registry entry and its
  stored ciphertext, and leaves the others alone. It does not revoke the
  daemon's access; only the vault's owner can do that.
- **Web clips get a tag.** Every page you clip is tagged `webclip`, and the tag
  is set in Settings → Notes (leave it empty for none). The same tag is applied
  to a page clipped from the phone's share sheet.
- **Clicking a task takes you to that task.** Task rows in the notes list, and
  the overdue and per-day rows in a daily note's footer, now open the note
  scrolled to the line you clicked, with it briefly highlighted. A
  *Copy link to block* link does the same.

### Fixed
- **An over-wide table no longer paints across the page.** Dragging a column
  past the width of the text column now scrolls the table inside it, instead of
  drawing over whatever sits beside the editor.
- **The table row/column/header controls are reachable again.** Right-clicking
  inside a table now offers them, whatever your toolbar looks like — and a
  toolbar layout that arrived from another client gets the table button back.
- **Clicking beside the text no longer jumps the cursor to the end.** Only a
  click below the last line does that now — a click level with the middle of a
  long note used to throw you to the bottom of it.
- **The open note's footer now follows a notebook, tag or colour assigned from
  anywhere else.** Dragging a note from the list onto a notebook — or assigning
  from the row's right-click menu, the multi-selection menu, or the sidebar's
  colour rows — left the chips in the open editor showing the old answer until
  you switched tabs and back.
- **"Link to note" from the toolbar opens a popover you can see.** It was being
  laid out inside the 36px toolbar strip, which clipped it away entirely.
- **"Link to note" with text selected now links that text.** It replaced the
  selection with an `@` instead.
- **"Synced N minutes ago" now moves while you are the one typing.** Paired
  with a relay peer — which has nothing to send back — the sidebar only ever
  re-read that time when a peer sent *us* something, so it froze at the moment
  you connected and counted up from there while every save was going out fine.
  The `• unsynced` marker was stuck the same way.
- **Settings → Encryption showed "1 minute" for auto-lock on a vault that was
  never locking.** The stored default matched none of the offered timeouts, so
  the dropdown fell back to its first entry. It reads *Never* now, which is what
  it was actually doing.

## [0.20.2] - 2026-09-04

### Fixed
- **The app can update itself again.** "Install and restart" did nothing — the
  download told the app it had succeeded while never handing the file to the
  installer, so there was nothing to install. Updates are now fetched quietly in
  the background and the titlebar's *Restart to update* actually restarts into
  the new version.
- **What's New no longer says you are up to date while showing you a newer
  version's notes.** That window never checked; it only ever repeated its
  starting state. It checks now, says "Checking…" until it knows, and offers the
  update.
- **A failed update check no longer reports "Up to date".** It keeps the last
  answer, but says so — "Couldn't check for updates — last seen: up to date" —
  instead of making a claim it could not verify.
- **The release notes window stops jumping in front of you during a download.**
  It was re-raising itself on every progress tick. It now opens once per
  version.

## [0.20.1] - 2026-09-03

### Fixed
- **The app no longer locks itself after 30 minutes you never asked for, or
  jumps in front of what you are doing.** The auto-lock timeout in Settings →
  Encryption was ignored — including *Never* — and a lock reloaded the window,
  which brought it to the front.
- **Settings no longer asks for your passphrase.** With Touch ID armed, opening
  Settings landed on the unlock screen instead of the settings, and the switch
  that turns Touch ID off was disabled in the one place it is offered. Settings
  now opens as itself, with an *Unlock* button where it needs the key.

### Added
- **A *Lock vault now* command.** In the omnibar's command list (`>`), for the
  moment you decide to walk away — it does exactly what the idle lock does.

### Changed
- **Auto-lock is off unless you turn it on, and it now unloads your notes from
  memory.** When it fires, every window on that vault locks — torn-off notes
  included — and their pages are torn down, so the decrypted content is gone
  rather than merely hidden. Getting back in always takes a gesture: your
  passphrase, or a one-click keychain unlock (Touch ID where you have armed
  it). Activity in any window of the vault keeps it open, reading included.
- **On the phone, auto-lock now notices time you spent away.** It could only
  count seconds while you were looking at it, and coming back from hours in
  your pocket started the countdown over — so it never locked when it mattered.
- **A scanned page's text now appears under it, and you can correct it.** Scans
  were already searchable, but the recognised text was invisible — so a word the
  scanner misread was wrong in the note with no way to see it or fix it. It sits
  under each page as ordinary text now, one page at a time.

## [0.20.0] - 2026-09-02

### Added
- **Print a note, or export it as a PDF, from the File menu.** They act on the
  note you are looking at, and Print is Cmd/Ctrl+P.
- **Find follows the usual keys.** Cmd/Ctrl+G jumps to the next match and
  Cmd/Ctrl+Shift+G to the previous one from anywhere in the note, and pressing
  Cmd/Ctrl+F again puts the caret back in the find field with the query selected.
- **Pin any notebook, tag, colour or note to the phone's home screen.** Long-press
  it and choose *Add to tiles*; it sits beside the built-in tiles, with its count
  (a note shows when you last edited it), and long-press removes it again. The
  pins sync, so the same tiles appear on every device — and a pin whose item was
  deleted simply disappears.
- **Due dates now work on the phone.** Put the caret in a checklist item and
  the formatting bar offers a due date, the same one the desktop has. The
  Tasks view can also list each note's unfinished tasks under the note itself,
  the overdue ones first and marked in red.
- **See what changed while you were away.** Home has an Activity section
  listing the notes your other devices edited since you last looked, newest
  first — open one to read it, or mark everything seen. On the phone the same
  list sits in the sidebar, under the tiles. It notices changes even to a note
  you had open at the time.
- **Ask for Touch ID before unlocking.** On a Mac, turn it on under Settings →
  Encryption once you store the key in the keychain. Your passphrase keeps
  working, and after a passphrase change you are asked for it once.
- **Record a voice note on your phone, and hypha writes it down.** Tap the
  microphone in the formatting bar, talk, tap Stop: the recording goes into the
  note with the transcript underneath it, as ordinary text you can correct. The
  transcription happens entirely on your phone — the audio is never sent
  anywhere. If your phone has no speech model for your language, you get the
  recording and hypha says it could not transcribe it.
- **Scan a document on your phone, and search it later.** Tap the scanner in the
  formatting bar to photograph a receipt, a letter or a page. hypha reads the
  text off it and stores that text with the picture, so searching for a word on
  the receipt finds the note — on your laptop too, not just the phone that took
  it. Search results say when the match was inside a scan rather than in what
  you typed.
- **A Home screen, and "on this day".** hypha now opens on Home: today's note,
  what is due, how many notes still have open tasks, and what you edited last.
  Above them, the daily notes you wrote on this same date in past years — one
  click away, and also shown at the top of today in the daily stream. **This
  changes what a launch does:** unless you have chosen otherwise in Settings, a
  window with nothing restored now opens on Home instead of All Notes.
- **Export a note as PDF, or print it.** Both are in the note's right-click
  menu; images in the note are embedded in the file, so it still shows them
  years later with no network.
- **hypha suggests tags while you write.** Click the tag box under a note and,
  if the note has no tags yet, hypha offers the tags from notes most like this
  one — click one to add it. It reads only your own notes, on your own device,
  and you can turn it off in Settings → Notes.
- **A due date is a link to that day's daily note.** Set one from the toolbar,
  the slash menu, the right-click menu or the command palette — the caret in
  one task or several at once — and the date appears inside the task as an
  ordinary link, so it travels with the note to every device. Today's daily
  note shows an Overdue section above its task list, and the Tasks view can
  list each note's open tasks under the note itself, overdue first.
- **Quick capture from anywhere.** Press Ctrl/Cmd+Shift+H — or pick Quick
  Capture in the tray — for a small box that stays on top: Enter adds what you
  typed to today's note, Cmd/Ctrl+Enter makes a new note from it.
- **Templates can fill in the date for you.** Write `{{date}}`, `{{time}}`,
  `{{datetime}}`, `{{weekday}}`, `{{title}}` or `{{date:DD/MM/YYYY}}` in a
  template and every note made from it gets the real value, in the date and
  time formats you chose in Settings. Anything else in braces is left exactly
  as you typed it, so a template about another template language still works.
- **Move through your notes with the keyboard.** The note list, Archive and
  Trash now take the arrow keys: up and down walk the rows without opening
  anything, Enter opens the one you land on, Space adds it to a selection,
  Shift with an arrow extends that selection, and Esc clears it.
- **Clip a web page from your browser.** Settings → Notes now shows a
  bookmarklet you can save to your browser's bookmarks bar; clicking it on any
  page opens hypha's clip dialog with that page already filled in.
- **The References section shows unlinked mentions.** Notes whose text
  contains the open note's title — but don't link to it — appear under the
  backlinks, so a connection you wrote in passing can be found and made real.
- **Callouts are real blocks.** A note, tip, info, warning or danger callout
  — with its own colour, an editable title and a fold — can be inserted from
  the slash menu, and an imported Obsidian `> [!note]` now arrives as one,
  keeping its type, title and folded state instead of turning into a plain
  quote. Exporting to Markdown writes the same syntax back.
- **Pasted Markdown becomes formatting.** Copy plain text with headings,
  lists, tasks, quotes, fences or tables — from Obsidian or anywhere — and
  pasting it into a note creates the real structure; a paste inside a code
  block stays literal. And the selection menu gains *Copy as Markdown*, which
  keeps note links working when pasted back into hypha.
- **Code blocks are syntax-highlighted.** Pick a language on a code block and
  keywords, strings, numbers and comments take colours from your theme — on
  the desktop and the phone, for all sixteen listed languages and their usual
  aliases.
- **A first start opens with hypha introducing itself** — the mark writes
  itself, then five short slides on what it does for you, each with a small
  animated scene, and the two permissions it can use (notifications for
  reminders, location for the weather in daily notes), each explained before
  it is asked for. It returns, for the new permission only, when a later
  version adds one.
- **After the first vault is created, a two-step tour points out the sync
  status and the invite** that opens the vault on another device or shares
  it with someone. Shown once per device.
- **Notes can be exported as Markdown** — the whole vault from *Backup &
  export*, or a single note from its menu, each note landing as a folder with
  its attachments beside it and the notes it links to coming along.
- **An Obsidian vault or any folder of Markdown notes can be imported** — wiki
  links between imported notes become Hypha note links, and referenced files
  become encrypted attachments.
- **A new device can restore a backup before it has a vault.** The first screen
  offers *Restore a backup* beside *Create* and *Join*: pick your backup folder
  (or a single `.hypha` file), enter the passphrase the backup was taken with,
  and the vault opens with your notes and attachments. If another device still
  has the vault, join it from there instead — a restored vault is a fresh copy.

### Changed
- **Backup is two settings sections now.** *Backup & export* sits under each
  vault and acts on that vault — back up now, restore, export to Markdown;
  *Backups* stays under Global for the folder, the schedule and how many to keep,
  which are the same for every vault on this device.
- **Tooltips are hypha's own now** — prompt, themed and out of the way, instead
  of the operating system's late grey bubble. The toolbar and the tab strip this
  time round.
- **Buttons respond to being held.** They dim while pressed, and the dimming
  fades rather than snapping.
- **Home opens notes beside itself.** Home is now a panel on the left with the
  editor on its right, like every other list in the app — clicking a recent
  note or an activity row opens it there instead of doing nothing.
- **Home's reminder tile counts what is coming.** It said *Due today* and
  counted only what fires before midnight, which on most days was nothing; it
  now says *Active reminders* and counts every reminder still due to go off.
- **Daily notes no longer carry a `#daily` tag.** The day itself is what makes
  a daily note one, so the tag is gone from new days and hidden on the ones you
  already have. Any other tag on a daily note still shows.
- **The notes list header is one row.** Sort, direction and grouping moved into
  a single ⋯ menu, the count says what it counts, and the Tasks view's
  *Completed* and *Individual tasks* switches are chips in that same row — the
  Tasks list used to be three rows of controls deep.
- **The list remembers how you sorted it.** Sort key, direction and grouping
  now survive a restart instead of resetting to newest-first each launch.
- **A pinned shortcut's menu is the menu of the thing it opens.** Rename,
  change icon, change colour — whatever the notebook, tag, colour or note
  would offer on its own row, the shortcut offers too, on both the desktop
  and the phone.
- **Reminders open in a tab, like notes.** Clicking a reminder in the list
  opens it beside the list and you edit it right there — no separate edit
  window. The mode and repeat controls are segments now, the same look as the
  phone's. The New button still opens its own dialog.
- **The Tasks filter's options got their own rows.** "Completed" and "List
  individual tasks" sat crammed into the filter pill (and overflowed it);
  each is now a row of its own right under the filter, the same look as the
  task rows in the list. The options left the phone's overflow menu too —
  they are in the list itself, where you can read the whole label.
- **A notes-only backup you take yourself goes where the scheduled ones go** —
  `<backup directory>/<vault>/notes/` — and counts toward the same "keep last"
  limit. With no directory set it still asks where to save.
- **The "Back up now" format picker starts on "notes only"**, and on iPhone the
  backup folder shows its folder name rather than a system path.
- **The vault sits in a fixed bar at the bottom of the home screen**, the same
  one Settings has, and it opens the same drawer — which now also adds a vault
  and removes one, from either screen. The last-sync line under it is gone; the
  sync dot in the bar above still shows that.
- **Tapping the sync dot goes straight to the invite QR** — a role, an expiry
  and the code, with nothing else in the way. Devices, peers and the last sync
  time are in Settings → Sync.
- **A daily note counts a task for a day when the task itself says so** — a
  link to that day's note in the task's text, or the task living in that day's
  note. Merely mentioning a date as plain text, or being created that day, no
  longer counts; editing the task makes the auto-linker link the date again.
- **Reorder the tiles on your phone's home screen.** Long-press a tile and
  choose *Sort tiles*, then drag the tiles where you want them — built-in and
  pinned tiles share one order, and it syncs to your other devices. Pinning
  something now scrolls the grid to the new tile, which appears with a small
  animation.

### Fixed
- **Switching vault from Settings stays in Settings.** On the phone it threw you
  back to the home screen mid-task; the vault had switched correctly, you just
  lost your place.
- **"Back up now" and "Restore" act on the vault they are listed under.** They
  used to sit under *Global* and follow whichever vault the Settings window was
  last pointed at, with nothing on screen naming it — a restore could adopt
  another vault's identity that way.
- **A backup schedule with no folder says it will not run.** Choosing a cadence
  before choosing a folder left a setting that quietly did nothing.
- **Escape closes one thing at a time.** A dialog opened over a popover used to
  take both away with a single press.
- **A confirmation dialog starts on a button, and Tab stays inside it.** Deleting
  something opens on *Cancel*, so an Enter that arrives a beat late no longer
  presses "Delete permanently", and closing puts focus back where it was.
- **Tabs say which note they hold.** Hovering a tab showed instructions for
  dragging it instead of the note's name.
- **A submenu no longer disappears on the way to it.** Moving diagonally from
  *Tags* or *Notebooks* to the panel it opened crossed the row underneath and
  closed it.
- **The notes list's date headers are solid.** Notes used to scroll visibly
  through them.
- **The link menu no longer sits see-through over the paragraph underneath.**
- **Tabs switch the moment you press them**, and a tab reached with Cmd+1-9 or
  Ctrl+Tab scrolls into view instead of changing the editor with nothing visibly
  happening in the strip.
- **A tab's close button can be reached with the keyboard.** It stayed invisible
  when focused.
- **Dragging across tabs, menu rows and list headers no longer highlights their
  text**, and those surfaces use the ordinary arrow cursor.
- **The indexing badge and the right-hand panel hold still when your system asks
  for reduced motion.**
- **The note's right-click menu shows words, not key names.** Its two PDF rows
  read `contextMenu.exportPdf` and `contextMenu.printNote`.
- **Leaving a window open past midnight no longer strands it on yesterday.**
  Home's *Today* tile opened yesterday's note and the date picker kept ringing
  yesterday until the app was restarted.
- **Clicking an "on this day" chip on Home opens that day.** It did nothing.
- **A search that matches nothing says so.** The results panel used to vanish, as
  if the field had been cleared.
- **The detach-pane shortcut no longer opens the command palette** when there is
  nothing in the pane to detach.
- **An interrupted panel drag no longer wedges the window.** If the system took
  the drag, the sidebar stopped animating for the rest of the session and the
  split handle kept resizing on the next mouse move.
- **The sidebar and notes-list slide is skipped when your system asks for reduced
  motion.** It is an inline animation, so the app's reduced-motion rules could
  never reach it.
- **A slow drag and a quick flick are no longer the same gesture on the phone.**
  A fast flick that barely moved used to spring back — panels, sheets and the
  half/full drawer now go where you threw them, and a swipe that is nearly there
  finishes faster instead of always taking the same quarter second.
- **A list row, a menu row or a search result no longer flashes every time you
  scroll past it.** The highlight waits for a finger that has actually stopped,
  the way iOS does.
- **Sheets, menus and the formatting bar keep clear of the notch when you turn
  the phone sideways.** In landscape the camera housing used to sit over the
  start of a menu row's label, and over undo and redo.
- **The phone's formatting bar no longer appears under menus that have nothing to
  do with the editor.** A long-press on a note, a notebook or a tag slid a
  formatting strip in along the bottom of the screen behind the menu.
- **A phone call or a notification pulled down mid-swipe no longer navigates.** A
  gesture the system takes away is dropped instead of being treated as if you had
  let go.
- **A slow swipe on a list row no longer leaves it stuck half open.** Dragging a
  row a few pixels and holding used to raise its menu over a row frozen sideways,
  and it stayed there after the menu closed.
- **The Dock icon and the tray work again after you have used quick capture.**
  Once the capture box had been opened, closing the last window left the app
  running with no way back into it — the Dock icon, the tray's *Show* and its
  *New Note* all did nothing.
- **Cmd+W does something in every window.** It closes the What's New window and
  hides the quick-capture box instead of being swallowed.
- **Cmd+S no longer hides the sidebar.** The sidebar and focus-mode toggles moved
  to Cmd+Alt+S and Cmd+Alt+. — which is what you want from a save reflex in an
  app that saves as you type.
- **A window last used on a monitor you have unplugged opens back on screen.**
- **A window closed in full screen reopens in full screen.**
- **Reminder banners with details turned off say "Hypha".** They were titled
  "hypha-desktop".
- **A hypha:// link opens the note.** With the Settings, What's New or
  quick-capture window in front, the link used to raise that window and go
  nowhere.
- **Opening Settings twice quickly no longer breaks the menu.**
- **Outline lists keep what you type in them.** Picking *Outline list* used to
  produce an empty block you could not type into, and an outline list already in
  a note lost its rows when the note was saved or reopened.
- **Copying a tag chip pastes a working tag.** A copied `#tag` used to paste as a
  dead chip that had lost the tag it pointed at.
- **The note picker highlights a row you can actually pick.** Typing another
  character after arrowing down used to leave no row highlighted and Enter doing
  nothing. Enter also no longer fires while you are confirming an input-method
  candidate.
- **Find's regex and case-sensitive switches now do something.** Both buttons lit
  up when pressed but the search stayed a plain literal one.
- **The slash, tag and note menus behave the same way.** Pressing a row no longer
  drops the cursor out of the note or dips the phone's keyboard, clicking a row
  runs that row rather than whichever one was highlighted, and arrowing down a
  long list scrolls it instead of walking the highlight out of sight.
- **The daily stream's footer stays closed until you open it.** A day's tags and
  its *Add tag* box were showing on every day of the stream whether or not you
  had expanded that day's details, jammed against the row above them.
- **A day's footer is as wide as the day's writing.** Expanding a day's details
  no longer throws its sections the full width of the pane.
- **The empty space under the day you opened is somewhere to write.** It used
  to sit below the day's closing rule doing nothing; it is now part of the
  day's text area, so clicking it puts the caret at the end of the day.
- **Popovers stay put above the keyboard.** The note picker, the date picker
  and the link popover now place themselves in the space the on-screen
  keyboard leaves. The link popover no longer vanishes the instant the
  keyboard rises — it moves aside and stays open until you scroll the page
  yourself.
- **Renaming a colour works on the phone.** The colour list's Rename command
  used to do nothing; now the name opens for editing right in the list — and
  whatever you rename in the sidebar scrolls into view first, so it isn't
  hidden behind the keyboard.
- **Removing a notebook or tag from a note now updates that collection's open
  list.** The note used to stay listed until you picked the collection again.
- **The sidebar, lists, tab bar and title bar are easier to read in dark mode
  with window transparency on.** They sat lighter than the window behind them
  instead of darker, which washed out their text.
- **A hypha:// link clicked while the app's window is closed no longer fails
  silently** — it is remembered and opens when the window is back.
- **PDF export and Print now work on notes with large images.** Documents over
  a couple of megabytes used to be refused without a word.
- **Removing a vault's key from the keychain no longer leaves Touch ID armed
  over nothing.** A removed account kept prompting, and the settings toggle
  kept saying the key was stored.
- **The first quick capture of a session is no longer lost** when pressing the
  shortcut had to open the app's window first: the text is held and delivered
  once the window is ready.
- **A task pasted within the same note no longer hides the tasks after it.**
  The pasted copy kept the original's identity, which broke the note's task
  rows from then on.
- **With Touch ID turned on, the keychain option no longer shows as off**, and
  a passphrase changed on another device now really does remove this machine's
  stored key.
- **A vault that crashes no longer keeps its due dates readable on disk.** The
  task list's dates stayed in the file until the next proper lock; they are now
  wiped at startup, before the vault can even be opened, and rebuilt on unlock.
- **Search keeps working on vaults without a passphrase after the index
  upgrade.** The one-time rebuild only ran when a vault unlocked with a
  passphrase, so every other vault's notes stopped appearing in search until
  each one was edited again.
- **On a phone, the find bar fits the screen, the insert-date panel stays
  above the keyboard, and every icon-only control has a name** for a screen
  reader — including the attachment preview's zoom buttons and the colour
  editor's swatches, which also stopped stretching into ellipses.
- **The German interface says *Tresor* and *Schlagwort* throughout** instead
  of mixing them with "Vault" and "Tag", the unpin action no longer reads as
  "file away in a binder", and the owner role is an *Eigentümer*.
- **Copy that reaches a phone no longer tells you to click** or to use the
  "main window": hints, the find bar and the insert-date picker are neutral,
  with keyboard shortcuts re-added only where a keyboard exists.
- **A note opened from Archive, Trash, Reminders or Web Notes has a back
  button that names that list**, the notes list shows its count like every
  other list, and an alert's button says *OK* instead of *Confirm*.
- **On a phone, selected text can be made into a link, tables can gain and
  lose rows and columns, and text can be aligned** — all from the format bar,
  which no longer assumes a right-click or a Tab key.
- **A long-press opens the menus that used to need a right-click** — a past
  day's in the daily timeline, backlink cards, and the daily note's task
  list.
- **The slash, @ and # suggestion menus now open above the keyboard**
  instead of under it, behind the format bar.
- **On a phone, a tapped image reveals its "Save to vault" button, the
  colour you applied in a sheet shows its checkmark, and the note-link
  picker's rows respond to taps** — which they previously did not.
- **A trashed note can be read on the phone before you restore or delete
  it.** The menu on a trash row now offers *Open*, which shows the note
  read-only; a trashed file shows its name, type and size instead, and a
  notebook offers no *Open*.
- **The pin and shortcut markers are now the same colour everywhere** —
  amber in light mode and the theme's yellow in dark, on both the desktop
  and the phone, where they previously ignored dark mode entirely.
- **The floating search and new buttons no longer sit on top of an open
  drawer**, and no longer overlap the vault bar on the home screen.
- **Backup settings say when a backup is not fully sealed.** A vault that has
  only been opened from the keychain since August's sealed-backup format still
  wrote backups with tag, notebook, reminder and attachment names readable, and
  nothing said so. The section now says it, and says what fixes it: unlock with
  your passphrase once.
- **"Last backup" now updates after every backup** — with attachments,
  scheduled, or notes-only — and no longer after a save you cancelled.
- **A backup saved through the save panel is readable only by your account**,
  like every other file hypha writes beside a vault.
- **Swiping a note on the phone now asks before it deletes, and says what it
  does** — "Move to trash" in the notes list and Archive, "Delete permanently"
  in Trash, the same words the long-press menu uses.
- **An invite link can be selected by hand on a phone** — the Select/Copy bar
  appears on the code, the fallback for when the copy button fails.
- **The phone's command list no longer offers commands that do nothing there** —
  new window, sidebar, list, table of contents and focus mode are gone from the
  omnibar, "Open in new window" is gone from attachments, and Reload no longer
  appears on the vault unlock screen.
- **Settings sections the phone had on the wrong side have moved** — Search is
  per device (it downloads a model), Search index per vault, matching the
  desktop.
- **Web Notes on the phone no longer asks you to log in** — publishing writes to
  your own S3 bucket, so there is no account, and a local-only user who has
  published can reach their web notes from the phone.
- **A note can be duplicated and a tag can gain a sub-tag from the phone's own
  menus** — a note could previously only be duplicated from the multi-selection
  menu, and a sub-tag only created from the tag row's hover button.
- **Shortcuts on the phone show the open-task dot** — a notebook, tag or pinned
  note in the shortcut row is dotted when it holds unfinished tasks, same as in
  the tree.
- **Settings toggles and the tree's expand chevron are easier to hit on a
  phone** — both now meet the same touch size as the controls around them.
- **The tray icon shows the hypha mark instead of an empty placeholder.** It
  adapts to the menu bar's light and dark mode, and stays crisp on Retina
  displays.
- **Dark themes no longer paint a huge tiled hypha mark across the app's
  background.** The intro's own faint mark also shows the right ink in dark
  themes now.
- **On the phone, the small title fades into the nav bar as a screen's large
  title scrolls underneath it** — it never appeared before.
- **The quick-capture window no longer shows the first-run welcome deck.** A
  fresh install's capture box arrived under the whole intro.
- **Importing from another account's vault works again when its key is in the
  keychain** — with Touch ID armed it claimed the vault was locked instead of
  asking.

## [0.19.0] - 2026-08-29

### Added
- **Daily notes record the weather.** A new daily note keeps its day's weather —
  the sky and temperature when it was written, the day's high and low, and rain
  or snow — shown in the day's header. It follows your device's location once
  you allow that under Settings → Notes (*Use my location*, at reduced
  accuracy), or a place you type there; the switch beside them turns it off.
  Only a coarse position is sent, to Open-Meteo, and nothing is written into the
  note but the weather itself.
- **Every day in the daily stream has a ⋯ menu** — the same actions as a note in
  the list, from the day's own header; a day with no note offers to create one.
  On the desktop, right-clicking the header opens it too.
- **The phone's pinned tiles and activity feed now appear at startup without
  waiting for a sync.** The home screen loads before the vault is open, and
  its first read used to answer "nothing" — with an error in the console —
  until a later sync happened to run it again, which a vault on its own never
  does.

### ⚠ Existing installs must start fresh

The vault model changed and **profiles from 0.18 and earlier are not migrated**.
Before launching this version: export anything you want to keep (Settings →
Backup), then delete the app's data and set up again — create a vault on one
device and join it from the others.

- macOS: `~/Library/Application Support/hypha`
- Windows: `%APPDATA%\hypha`
- Linux: `~/.config/hypha`
- iOS: delete and reinstall the app
- Relay daemon: remove its `--data-dir` and run `hypha-peer init` + `join` again

### Fixed
- **In daily notes, the day you are writing in no longer changes as you
  scroll.** Scrolling used to hand the caret, the toolbar and the timeline's
  selection to whichever day passed a line near the top — differently going up
  and down. Now the active day changes only when you click or tap into a day,
  cross a day with the arrow keys, or pick a date; scrolling just scrolls.
- **A daily note moved to the trash leaves the daily stream at once.** Its day
  goes back to "Write something for this day…", nothing typed there brings the
  old text back, and its weather line goes with it. Restoring it from the trash
  brings the day back.
- **In daily notes, the day header is no longer a solid band across the page.**
  With transparency on, every day's date painted the pane's colour a second
  time; now only the date holding at the top covers the text scrolling under
  it, and with a lighter touch.
- **On the phone, tapping a tag or notebook you already have open shows its
  list again.** Going home and tapping the same tag a second time used to do
  nothing; the same held for a note's notebook and tag chips.
- **On the phone, going back from an attachment returns to where you opened
  it** — the daily stream on the same day, a search, or the note — instead of
  the notes list. A file opened from a note's Files footer now opens in place.
- **On the phone, the home screen and the navigation bar are one colour.** The
  bar used to sit a shade off the screen below it, in every theme.
- **On the phone, the reminder editor no longer loses its form when the
  keyboard comes up.** The title and description fields stay on screen and can
  be typed into; Save and Cancel stay put.
- **The reminder editor's Mode and Priority are icon toggles, side by side.**
  Once / repeat / permanent and silent / vibrate / urgent each sit on one row
  as glyphs, and read out by name with VoiceOver.
- **Resizing a picture on the phone works under a thumb.** While a picture is
  selected its corner handles are large enough to grab, a grab no longer turns
  into a scroll, and dragging a left-hand corner no longer swipes back to the
  list.
- **Daily notes are named for their day everywhere** — the tab, the phone's
  title bar and the omnibar now say "Saturday, 29 August" instead of "Untitled"
  or the raw date. A daily note you have renamed keeps its name.
- **The preview line under a note's title in the list no longer reads "No
  additional text" after a restart.** It showed the first words of a note only
  once you had edited it in this session; now it is kept between launches, in
  the Archive list too.
- **Joining a vault can no longer overwrite a vault this device already has.**
  An invite naming a vault id this device holds for a different owner is refused
  with an explanation, instead of replacing that vault's keys.
- **"Add a vault" now asks whether the new vault should get the example notes.**
  The first vault on a device always has them; a vault added later starts empty
  unless you tick the box. A joined vault never gets them.

### Changed
- **There is no longer a special "local" vault.** Every vault — the first one on
  a device and every one added later — is created, listed, named, switched to
  and removed the same way. The vault switcher, the Settings groups, the
  launch-vault picker and the import target all read one list.
- **A first start creates a vault with its own identity**, the same way "Add a
  vault" does.
- **`hypha-peer migrate` is gone** along with the pre-multi-vault layout it
  converted.
- **The daily stream's scroll cost is now measured and gated** in the test
  suite: how many days are kept live, and how often that is recalculated while
  you scroll.

## [0.18.0] - 2026-08-29

### Fixed
- **A file added on the phone over cellular is now uploaded once**, to the
  relay, and the laptop gets it from there. It was uploaded three times.
- **A device that asks the relay for an attachment while it is still arriving
  now receives it as soon as it has landed**, instead of at its next reconnect.
- **Removing a device now disconnects it right away** on every device that
  learns of the removal, instead of at its next reconnect.
- **A large attachment one device cannot send is still fetched from another
  device that can.** One "too large" answer used to stop the request for every
  device until the app was relaunched.
- **With two vaults open on the desktop, each window now lists only its own
  vault's devices**, and a sync failure in one vault no longer flags the other.
- **The relay refuses to join a second owner's vault under a context it already
  serves.** Two people's default vaults share the name `local`; the second join
  used to silently replace the first vault's keys and serve its data to the
  wrong devices.
- **An attachment two devices both hold — the relay and a laptop, say — is now
  fetched from one of them at a time.** Both used to answer, and the second
  transfer wrote into the first one's half-finished file.
- **A device that joins a vault while the always-on relay or another member is
  reachable now syncs with them once the owner has admitted it.** Before, the
  two kept refusing each other until the app — or the relay — was restarted.
- **Notes written on one device while it could only reach the laptop now reach
  the always-on relay — and every device behind it.** They could be skipped
  silently on the laptop's next connect to the relay. Rows older than a relay's
  first join that had not reached it before this fix can still be skipped.
- **Deleting an attachment from a note now updates the Settings → Attachments list
  on the desktop.** A file you trashed from a note — and a trash you emptied —
  kept showing in the open Settings window until it was closed.
- **The desktop now asks whether to delete a file you took out of a note when no
  other note uses it**, like the phone already did. And a removal made on one
  device no longer prompts every other device once the note syncs.
- **Daily notes: the day header no longer sits on the stream as a solid slab.**
  It is now the same frosted surface as the pane around it.
- **Phone: opening a file from a note no longer puts its name and controls under
  the top bar.**
- **Phone: swiping back from a file opened out of a note returns to that note**
  instead of the notes list.

### Added
- **Settings → Sync: "Over cellular, send attachments only to the relay"** (on
  by default; shown on the phone). Turn it off to send to every device
  directly. Without a relay, attachments are always sent.

### Changed
- **The test harness now runs a laptop and a phone that reach each other
  directly and through the relay at the same time** — the configuration the
  2026-08-28 review found untested.

## [0.17.1] - 2026-08-28

### Added
- **Your always-on peer now keeps your attachments, not just your notes.** Add a
  file on one device and it reaches the peer straight away, so another device
  can fetch it later even if the first one is switched off. Before, a file only
  reached the peer if some device happened to ask for it while the device
  holding it was still online — so a note could arrive without its attachment.
  How long the peer keeps them is still its `prune` settings' decision.
- **An interrupted attachment transfer picks up where it stopped.** A large file
  that failed part-way used to start again from the beginning every time; now
  only the missing part is sent — verified on an iPhone by cutting Wi-Fi
  mid-transfer, which skipped a quarter of a 60 MB file on reconnect. Both
  devices need this version; against an older one, or through a relay that is
  only forwarding, it still restarts. A transfer *to* an always-on relay always
  restarts.
- **Settings → Storage: reclaim the space deleted notes leave behind.** It
  shows the vault's size and how much of it is reclaimable, and offers to
  compact when there is enough to be worth it. Nothing is deleted — notes,
  edits and history are all kept.
- **`hypha-peer prune --vacuum` gives the pruned space back to the disk.**
  Without it a prune only frees pages inside the daemon's database and the file
  keeps its size. Run it with the daemon stopped.

### Changed
- **A development build keeps its own data, separate from the installed app.**
  `npm run dev` used the same profile as the release build, so a test vault or
  a half-finished migration ran against the real notes; it now uses a `-dev`
  profile of its own, and the two can be open at the same time.
- **The release notes for 0.1.0–0.13.0 are shorter.** They were written before
  this file's one-or-two-sentence rule and ship inside both apps; trimming them
  to it took about 105 KB out of every build. No version was removed and no
  warning was dropped.

### Fixed
- **A file the always-on peer could not take is offered again later.** The peer
  now tells a device whether it kept a file. Before, a device treated "sent" as
  "kept", so a file pushed to a peer whose disk was full was never offered
  again — and a file the peer already had was sent in full a second time.
- **The mobile settings smoke counts the Storage section.** It was still
  expecting the twelve sections that existed before Storage was added, so the
  gate failed on a list that was correct.
- **The relay daemon no longer re-derives its passphrase key on every secret it
  writes.** `hypha-peer join`, and the vault migration that renames every
  secret, paid a full key derivation per write — about 74 ms each. It is now
  derived once when the store opens.
- **The relay daemon reclaims the disk space of interrupted attachment
  transfers.** A peer that dropped mid-transfer left its partial file behind for
  good, and after four of them that peer could no longer send the daemon any
  attachment at all.
- **The relay image runs on x86 servers.** Every previous one was built for
  Apple Silicon only, so pulling it onto an ordinary VPS failed outright. It is
  now published for both amd64 and arm64.
- **A trashed file is visible in Trash on iPhone.** Only trashed notes were
  listed, so a deleted file could not be seen, restored or deleted on its own
  until the seven-day sweep made it permanent.
- **`hypha-peer prune` no longer overstates what it freed.** It reported space
  inside its own database as if the filesystem had it back; disk and database
  are now reported separately.
- **A note shows when a file it references has been deleted.** The chip, image
  or player is marked deleted instead of offering to open something that is no
  longer there, and one still in the Trash can be restored from the note.
- **The iPhone says so when it cannot delete a file's data.** The failure was
  silent, and nothing retries it, so the space stayed used with no way to tell.

## [0.17.0] - 2026-08-27

### Added
- **A light and a dark app icon, plus a tinted one.** iOS picks whichever suits
  your Home Screen, so the icon now lightens on a light Home Screen instead of
  staying near-black, and tinted mode gets artwork made for it rather than one
  the system guesses at.
- **Choose what a vault opens on: the home screen, or a specific note.** Two new
  options in Settings → Notes → "Opens on". A note is chosen by searching for it
  rather than from a list, so it works in a vault of any size.

### Changed
- **The widgets wear the Hypha mark.** The Daily Note and New Note widgets
  carry the app's own calendar and note glyphs instead of generic system
  symbols, and the glyphs are larger — they were sitting small in their
  circle on the Lock Screen.
- **The iPhone home screen leads with tiles.** All Notes, Daily Notes, Tasks,
  Web Notes, Archive and Reminders are now a two-column grid of cards at the top
  of the screen, each with a coloured icon and a live count, instead of six
  identical rows. The Daily Notes tile is a calendar face — today's day over
  the month, with the weekday under it. The colours come from whichever theme
  you are using.
- **A new vault opens on the home screen.** Previously it opened on the notes
  list, with no sign that there was anything to the left of it. Once you have
  opened something, it goes back to where you left off as before.

### Tooling
- **Desktop releases are built and signed locally again.** A tag no longer
  starts a GitHub Actions build, so a release carries macOS and iOS; the Windows
  and Linux legs stay in the workflow, but no release has been built through
  them yet, so there is still no Windows or Linux download.

## [0.16.0] - 2026-08-26

### Added
- **One relay daemon can now serve several vaults.** Join as many invites as you
  like into a single `hypha-peer` data dir; each vault keeps its own identity and
  its own storage, and one service runs them all.
- **Notebooks and tags show when something inside them is unfinished.** A small
  dot at the right of a sidebar row means a note in that notebook or tag — or in
  anything nested under it — still has an unticked task.
- **The sidebar remembers which notebooks and tags you left open.** Unfolding a
  notebook with sub-notebooks, or a tag with sub-tags, now survives a reload
  instead of collapsing back to the top level every time.
- **Daily Notes opens ready to write.** On a Mac the cursor starts in today, and
  the day you opened is given room on screen rather than sitting as one thin
  line above the next day. On a phone the keyboard stays down until you tap.

### Changed
- **A relay daemon's storage moved into a folder per vault.** An existing data
  dir is converted the first time the new version starts; back it up first,
  because there is no way back to the old layout.
- **The text colour and highlight buttons are a brush and a marker.** The
  editor toolbar had two identical pen icons, one of which opened no colours;
  that one is gone, and text colour now uses a brush instead of a letter "T".
  On a phone both are available for the first time, each with its own swatches.
- **The daily stream sits closer to the screen edge on a phone.** It had a
  wider margin than an ordinary note; it is now slightly narrower than one.
- **The sidebar no longer marks favourites twice.** The star on a notebook, tag
  or colour row appears on hover instead of staying lit once the item is
  favourited, and on iPhone it is gone from the rows entirely; the Shortcuts
  section already lists everything you have favourited. Adding and removing a
  favourite works exactly as before, from the row itself on a Mac and from the
  row's long-press menu on a phone.

### Fixed
- **The relay daemon no longer asks for a passphrase before checking there is
  anything to unlock.** On a machine that has never run `init`, `vaults`,
  `status`, `run`, `prune` and `migrate` prompted first and only then reported
  that no store exists.
- **A relay daemon with no way to read its passphrase now fails instead of
  exiting quietly.** Started with no terminal and no `HYPHA_PEER_SECRETS_PASSPHRASE`
  — a misconfigured service file — it reported success while relaying nothing, so
  nothing restarted it.
- **A relay daemon joined to a shared vault now actually relays it.** It was
  refusing every device unless the vault happened to be the default one, so the
  relay sat in the room and nothing ever synced through it.
- **Daily Notes opened in a different place every time.** The stream now lands
  on the day you asked for, every time, and holds it there while the days above
  finish loading.
- **Clicking Daily Notes did not always show today.** From the sidebar it could
  reopen whichever day you last browsed, and after closing the daily tab it did
  nothing at all. It now opens today from either shell, however many times you
  click it.
- **Clicking an empty day did not put the cursor in it.** The "write something
  for this day" row, the space around it, and a day still loading are all
  places you can click to start writing.
- **Tapping a day moved the page under you.** The day you tapped now stays
  exactly where it was while its editor appears.
- **Scrolling up and down disagreed about which day you were in.** The
  highlighted day and the cursor now follow the scroll the same way in both
  directions instead of sticking on the day you started from.
- **Links between notes showed as "Untitled".** A linked note's title is
  encrypted like everything else, and the code that loads links — both the
  notes you link to and the ones linking back — never decrypted it, so every
  link chip fell back to "Untitled" in any encrypted vault.
- **The open-task dot is quieter, and it now shows in Shortcuts.** It is a
  little smaller and takes the same green a note's task progress bar uses,
  softened — one colour for one fact instead of two. Shortcut rows never had
  the dot at all, so a notebook could be marked in the list below and unmarked
  in Shortcuts; notebooks, tags and favourite notes up there now carry it too.
- **Sub-notebooks were unreachable in the sidebar.** A notebook containing
  other notebooks showed no way to open it, so everything inside stayed hidden
  — while still being counted, which is why the notebook heading read higher
  than the list. A newly made sub-notebook appeared only until the next
  restart. Notebooks that contain others now show the expand arrow again,
  whether or not they have been opened before.
- **A notebook could go missing from the sidebar while still being counted.**
  Putting a notebook in the trash left any notebook inside it with nowhere to
  appear: the sidebar counted it but had no row to show it under, so the
  notebook heading read one higher than the list. Those notebooks now move up
  to the top level, where you can see and move them — and restoring the
  original notebook puts them back inside it.
- **A link to a note in the trash now says so.** The link stays — restoring the
  note brings it back intact — and the chip carries a small trash icon and a
  struck-through title instead of looking like a link to a note that is still
  there.
- **Deleting a note for good left its links behind.** Emptying a note out of
  the trash removed the note but not the links pointing at it, so the notes
  that linked to it kept a chip leading nowhere — and re-opening one of those
  notes put the link back. Both halves are fixed: the links go with the note,
  and a link in the text of a note is no longer revived when its target no
  longer exists.
- **Your phone reconnects in about 9 seconds after you unlock it, instead of
  about 36.** While the screen is off the phone gives up its network connection
  entirely, and it used to get back by announcing itself and waiting to be
  found. It now also calls the devices it has actually talked to before,
  directly, at the same time as it announces — so a note you write on your Mac
  reaches your phone about half a minute sooner after you pick it up. Measured
  on an iPhone over mobile data: 36.2 seconds before, 9.5 after.
- **Two devices on the same network kept dialling each other over the internet
  as well.** When your phone and your Mac can already see each other locally,
  the second connection is redundant and was being closed and remade about
  every 45 seconds, all day — measured at roughly 79 needless connections an
  hour on each device. hypha now waits longer each time before trying again,
  up to ten minutes, while still reconnecting immediately if the local link
  really does go away.
- **Importing from Standard Notes created no notes.** Import opened its own
  connection to the vault, which is locked by definition — and since the
  at-rest work a write into a locked vault is refused rather than quietly
  stored unencrypted, so every note failed and the summary said it imported
  zero. Import now writes through the vault this window already has open, or
  unlocks the chosen one with this device's key, and says which vault to unlock
  when it cannot.
- **The desktop app would not start.** A change from the security work reached
  the sync package through its main entry point, which pulls in code that only
  runs on a server — in the app window that turns into an error before anything
  is drawn. The app now imports only the piece it needs, and a test walks the
  window's whole import graph so this cannot come back unnoticed.

### Security
- **The passphrase leaves fewer targets behind.** How expensive it is to turn
  the passphrase into a key is now stored beside the vault's salt (so it can be
  raised for new vaults without touching old ones), an invite link can be
  issued without the material that made every link a passphrase-guessing
  target, and a backup can be written device-bound with its credential sealed
  inside. All three are built and verified; the stronger cost, the new link
  form and the device-bound option are not yet switched on in the app.
- **Sync no longer takes another device's word for it.** Data arriving from a
  peer is checked against the expected shape before it is stored, a device
  whose clock is more than an hour ahead is held until real time catches up
  instead of overriding everyone's edits, an attachment is only deleted when
  the deletion itself has synced, and device credentials now expire after
  thirty days and are renewed automatically whenever the device meets one of
  the vault owner's devices. A renewed credential is saved on the device, and
  a used invite can no longer be un-used by another device's sync.
- **A locked vault leaves no readable copy of your notes behind.** The search
  index and the semantic index are now emptied when the app starts as well as
  when the vault locks, so a crash or a force-quit no longer leaves them full;
  the search index rebuilds itself after you unlock. Notes that were in the
  trash when you first set a passphrase are now encrypted too, note-history
  entries no longer store a plain fingerprint of their text, the app refuses to
  open a vault file that turned out not to be encrypted, and nothing can be
  saved in plain text while the vault is locked. Sealed values are now bound to
  the note they belong to on every device.
- **Sync discovery no longer reveals the vault to bystanders.** The LAN beacon
  announces a hashed alias of the vault's sync topic instead of the topic
  itself, and a device joining with an invite hands that invite only to the
  vault owner's device, never to whoever connects first. A device on this
  version and one on an older version will not find each other over the LAN
  until both update; sync over the internet is unaffected.
- **A note from another device is treated as untrusted.** Images hosted on
  someone else's server are no longer fetched when a note opens — they show a
  placeholder naming the host and a "Load image" button — unless you turn on
  the new Settings → Global → Privacy → *Load external images in notes*. An
  embedded web page in a note can no longer open windows or be granted
  permissions such as location or camera, and a link that points at a network
  share is refused rather than opened.
- **Opening a local file from a link in a note now asks first**, whatever the
  file type. Attachments you open from the app itself are unaffected.
- **Developer tools are no longer in the menu of a shipped build.**
- **The desktop app can no longer be used as a general-purpose Node runtime.**
  The shipped build now refuses `ELECTRON_RUN_AS_NODE`, `NODE_OPTIONS` and
  `--inspect`, verifies its own bundle before starting, and on Windows an
  uninstall keeps your vault on disk.
- **The macOS build is packaged with the Electron it was tested with.** The
  0.15.0 build had shipped with a newer Electron than its database engine was
  built for, so opening a vault failed; the version is now pinned and checked.
- **On iOS, the app's own diagnostic output is written to the system log only
  while Logging is turned on.** It used to be written regardless of the toggle.
- Files hypha keeps beside the vault (`picked-dirs.json`, `app-state.json`, and
  attachment blobs stored before 0.11.0) are now readable only by your account.
- **Backups and exports are written readable only by your account**, including
  files a previous backup left behind. Publishing to S3 now refuses anything but
  the four request types it uses and stops reading an oversized reply instead of
  buffering it; a passphrase-protected published page no longer shows the note's
  title before the passphrase is entered; the What's New check no longer sends a
  `GITHUB_TOKEN` from the environment; and note ids are drawn from the system's
  cryptographic random source.
- An internal security audit is published as `docs/SECURITY-AUDIT-2026-08-25.md`,
  and SECURITY.md now says what it found and what is still open.

### Tooling
- **The published relay compose file now pulls `latest`.** It pinned `0.13.0`
  and nothing bumped it, so anyone following the install instructions got an
  image several releases behind. Images also carry the version as a label, since
  the tag no longer says which one you have.
- **`npm run peer` builds and runs the relay daemon from a checkout.** It also
  puts the native SQLite addon back on the Node ABI, which `npm run dev` flips
  to Electron's — without that the daemon fails to start after a desktop session.

## [0.15.0] - 2026-08-25

### Changed
- **Semantic Vector Search is now one setting for the whole app**, not one per
  vault. It has moved to Settings → Global → Search, adding a vault no longer
  asks again, and your existing answer carries over — if you enabled it
  anywhere, it stays on. Rebuilding and purging a search index stays per vault,
  under that vault's new "Search index" section.

### Fixed
- **A tab or note dragged onto another vault's window is refused.** The window
  you are dragging over says so while you hover it, and the tab flashes if you
  drop anyway. It used to be accepted: the tab vanished from the vault that
  owned the note and the other window opened one it could not read.
- **Windows you closed stay closed.** Reopening a vault used to bring back every
  detached window you had ever opened in it, more of them each time.
- **Restarting reopens the vaults you had open, not every vault you visited.**
  Switching vault inside a window left the old one marked open, so a single
  window that had toured four vaults reopened as four windows.
- **Edits made in one window now show up in the other.** With the same vault
  open in two windows, typing in one — including in the daily-note stream —
  appears in the other within about a second, without touching your cursor.
- **A note created in one window appears in the other's list.** It used to stay
  invisible there until the app was restarted, and a day written into in one
  window's daily-note stream stayed an empty day in the other's.

## [0.14.1] - 2026-08-25

### Added
- **Sharing into Hypha can choose the vault.** With more than one vault on the
  phone, the share sheet asks which one first; with one, nothing changes.
- **A notification when a share needs you.** Choosing "an existing note…"
  posts a banner — tapping it opens Hypha at the note picker. Hypha asks for
  notification permission after the first share lands.
- **A shared link is clipped wherever it goes** — into today's daily note or
  an existing note as an article with its source line, not as a bare link.

### Changed
- **Scrolling the daily-note stream puts the cursor in the day you land on**, so
  it is ready to type in, and that day's date is the bright one. Picking a date
  yourself keeps it highlighted and focused until you scroll it off screen.
- **The share sheet is a real sheet**, in English and German: what is being
  shared, the vault, the three destinations, and an "Added" confirmation. A
  URL share with a single vault still clips silently.
- **A waiting share can be discarded** from the in-app sheet; Cancel still
  keeps it for next time.
- **A single-note window can show the daily-note stream.** Drag the daily tab
  onto one and it renders there. Opening one daily note in its own window still
  shows just that day.

### Fixed
- **Cmd+D no longer leaves the daily-note tab flipping between two dates.** The
  tab could get stuck jumping back and forth and would reappear every time you
  closed it.
- **Dragging a note window's last tab back to the main window works.** It used
  to close the main window instead, leaving the note window alone in focus mode
  with no tabs.
- **Today's date is never dimmed** in the daily-note stream, whichever day you
  have scrolled to — and it is still marked as today after midnight, without
  reopening the app.
- **A vault you join shows its real name**, not its identifier. The name arrives
  with the first sync and the sidebar and Settings update without a restart.
- **"Go to today" goes to today** in the daily-note timeline, even if the app has
  been open since before midnight.
- **The daily-note tab can be dragged out into its own window**, or onto another
  window, like any other tab. It was the one tab a drag did nothing to.
- **Closing the daily-note tab clears the day from the pane.** On a day with no
  daily note yet, the stream stayed on screen after its tab was gone.
- **Dragging a note out of its own window can no longer lose it.** Releasing the
  tab just short of another window closed the window and left the note open
  nowhere; it now stays where it was.

## [0.14.0] - 2026-08-25

### Added
- **Share into Hypha from any app.** A link becomes a web-clipped note on its
  own; anything else asks — right there in the app you are sharing from —
  whether it goes to today's daily note, an existing note or a new one. iOS does
  not let a share sheet open Hypha, so the share is waiting for you the next
  time you open it. Choosing an existing note is the one case that needs you to
  switch over, because picking it means reading your notes.
- **Two Lock Screen widgets on iPhone** — a calendar button that opens today's
  daily note, creating it if the day has none, and a plus button that starts a
  new one. Both also work as Home Screen tiles.
- **Each vault can choose what it opens on** — where you left off, a view, a
  notebook, a tag or a colour. Settings → Notes. The choice travels with the
  vault, so your other devices follow it.
- **On iPhone you can pin which vault opens when the app starts.** Settings →
  Open on Launch. It still defaults to the vault you used last, and it stays on
  this phone rather than syncing.

### Fixed
- **Long-pressing the + button now opens its menu on every screen**, not only
  the notes list. "Clip web page" is reachable from anywhere as a result.
- **The daily-note stream no longer jumps when you scroll up into older days.**

### Changed
- **Date headings in the daily-note stream are dimmed except the day you are
  reading.** The day becomes the bright one as it reaches the upper quarter of
  the screen, and its heading now reads as a date tile with the weekday beside
  it.
- **Search across all your notes is now ⇧⌘F** (Ctrl+Shift+F on Windows and
  Linux). It used to be ⌥⌘F.
- **⌥⌘F now opens find and replace inside the note you are in.** The replace
  row is already open, so you can type both halves straight away.

### Fixed
- **A long press in the notes list no longer selects text.** It opened the
  drawer and started a selection at the same time — sometimes highlighting the
  whole screen, or the drawer's own text.
- **Going back from a linked note returns you to the note you came from**, even
  when you had been out to the notes list in between. It used to drop you in the
  list instead.
- **Tapping a date in Daily Notes now opens that day at the top of the screen**,
  instead of a bar's height too high with its first lines behind the date.
- **The date at the top of a day no longer flickers between two sizes** while
  you scroll past it.
- **On Windows and Linux, the minimise/maximise/close buttons follow your
  theme.** They were drawn in white whatever the theme, so on a light theme they
  were white on a light background.

## [0.13.3] - 2026-08-24

### Changed
- **The bar at the top of every screen is solid now, and the strip behind the
  notch is part of it.** It used to be invisible until you scrolled, so that
  strip read as a grey band sitting above the bar.
- **The back button is a chevron on its own**, in the bar's own colour. It used
  to print the name of the screen behind it, in the accent, which read as the
  bar's main action rather than its way out.
- **The screen's name sits on the left of the bar**, lined up with the heading
  below it, instead of centred.
- **Collections leads with the app logo** instead of a "Collections" heading,
  and the arrow across to your notes is gone — swipe across instead.
- **Daily notes read as one page.** Each day's date is large on arrival, then
  shrinks and holds at the top while you read that day. Days you have not
  written in are a single line instead of a block, so about twice as many fit on
  screen.
- **A day's notebooks, tags, links and files are one row.** Tap it for the full
  set. They used to be four sections per day, mostly saying "None".
- **The daily notes editor runs the full width of the screen**, and the search
  and new-note buttons sit closer to the corners.
- **Daily notes is its own tab on the desktop**, named for the view instead of
  showing a date. Browsing a week of days leaves one tab rather than seven, and
  a day you have never written in now has a tab like any other — it used to open
  with nothing selected in the tab strip and no way back to it.
- **A day in the desktop daily-notes stream lines up with its own writing.** The
  date, the line on a day you have not written in, and the day's summary row ran
  the full width of the pane — and right to the edge of a narrowed tab, where a
  single note keeps its margin.

### Fixed
- **The Join button was behind the keyboard** when unlocking or joining a vault.
- **The formatting toolbar never appeared in daily notes.**
- **A vault on a dark theme was unreadable while another vault was open on a
  light one.** Windows whose themes clash now both trade the translucent glass
  for a solid background until they match again, and Settings → Appearance
  says so.
- **Pin, star and shortcut icons were the wrong shade** in a vault whose theme
  differed from the other open vault's.

### Tooling
- **The mobile sidebar smoke checks the header rather than the old headline**,
  and now catches an app logo that fails to load or picks the wrong light/dark
  variant — both of which used to render as nothing, silently.
- **A probe measures the daily-notes stream against the editor's column** in a
  running desktop window, so "the date lines up with the writing" is a number
  rather than a look.
- **A probe records which scroll wins when a daily note opens.** It asserts
  nothing and is not a gate — it exists for an open report that the stream
  sometimes lands at the end of a date instead of the start.
- **A probe drives the daily notes tab in a real desktop window** — opening it,
  quitting, relaunching, and checking the tab strip comes back whole.

## [0.13.1] - 2026-08-24

### Added
- **Daily notes are one continuous page you scroll through, not one note at a
  time.** Opening a day used to mean landing on that single note; getting to
  yesterday meant going back to the date list and picking again. Now the editor
  holds every day in order — scroll up for the days before, down for the days
  after — and picking a date in the list scrolls to it rather than opening
  another tab. Days you have not written in are there too, so a week you skipped
  is a short scroll rather than a gap you have to navigate around; writing in
  one creates that day's note exactly as before, on the first thing you type.
  The arrow keys cross between days: press up at the top of a day and the caret
  continues at the end of the previous one.

  Days you scroll away from are **unloaded**, not merely hidden, and days you
  have not written in cost nothing until you write in them. That is what keeps a
  page holding a year of days from growing without limit — and on the phone it
  is the difference between the app working and iOS shutting it down for using
  too much memory.
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
- **The iPhone app looks and moves like an iPhone app.** The chrome has been
  rebuilt against the design iOS uses now, and the change is most obvious in
  four places.

  The bar at the top of every screen no longer sits above your notes — it floats
  over them. Notes scroll underneath it and under the status bar, and the bar
  itself is clear until something passes behind it, at which point it frosts
  over and takes the screen's name into its middle. Screens with a big title
  (Collections, Settings) now print that title in the page rather than in the
  bar, so it scrolls away like the rest of the content.

  **A new note is always one thumb away.** The `+` used to exist on two screens
  out of thirteen; it is now a floating button in the bottom-right corner of
  every screen, and it knows where you are — on Reminders it makes a reminder,
  under the Tasks filter it makes a task. Press and hold it for the other ways
  to start something, including clipping a web page.

  **Search has its own button**, bottom-left, where your thumb already is. It
  used to be the screen's title, which worked and nobody found. It opens as a
  drawer that rises from the bottom with the search field resting on top of the
  keyboard and the results filling the space above it — so the thing you type
  into and the thing you tap are both within reach, instead of at opposite ends
  of the screen.

  **Swiping between screens now starts at the edges only.** Sliding between the
  sidebar, your list and the open note used to be possible from anywhere, which
  meant it competed with everything else a horizontal drag might mean — pulling
  a row aside for its Archive and Delete buttons, placing the cursor in a
  sentence, scrolling a wide table. Navigation now lives in a strip at the left
  edge (back) and the right edge (forward), which is where iOS puts its own back
  gesture, and everything else on the screen belongs to what is on it.

  Alongside those: one animation curve instead of three, with the outgoing
  screen sliding back and dimming behind the incoming one the way iOS does;
  larger, more consistent corners on sheets and menus, defined by a hairline
  rather than a shadow (which read as a smudge on the light themes); the iOS
  type scale; and a buzz on the new-note button, which never had one. If you
  turn on **Reduce Transparency** in iOS Settings the frosting is replaced by
  solid colour throughout, and **Reduce Motion** drops the sliding.

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
- **The iPhone app was letterboxing itself, and painting two different
  backgrounds.** Reported off a device: the notch area did not look like part of
  the navigation bar, and there was a thin grey band across the bottom of every
  screen. Both were the same mistake seen from two ends. The app reserved a
  strip at the bottom for the home indicator and filled it with its own
  background — where a native app simply lets content run underneath — and note
  rows and the note editor painted a slightly *different* background from that
  strip, so the seam had a visible edge. Content now reaches the bottom of the
  screen, the last row is spaced clear of the home indicator instead of stopping
  short of it, and every surface uses one colour. Measured before and after on
  an iPhone 17 Pro: the strip and the rows were (22,24,29) against (15,17,21),
  and are now identical.
- **The iPhone UI test suite could pass against an app that had not started.**
  The documented command asked Xcode to skip code signing, which costs the app
  its Keychain entitlement — so it stopped at a "Startup failed" box, and the
  test that checks the page reaches the top of the screen passed anyway, because
  it compares two dark pixels and an error screen is dark. The flag is gone and
  the reason is written beside the command. While confirming that, a second
  thing came out: those tests only ever see the vault-unlock screen, because a
  fresh install has no vault — one of them had claimed for its whole life to be
  tapping the notes list. They still check what they were written to check; the
  description was wrong, and now says so.
- **The 0.13.0 desktop app would not start.** It opened a grey error box
  ("Cannot find package 'libsodium-wrappers-sumo'") and went no further. One of
  the encryption components the app is built on was never listed among the
  things the installer had to include — it reaches the app indirectly, through
  another part of the project, and everything that runs Hypha from source shares
  a single pool of components, so it resolved correctly every time it was built
  or tested and was simply absent from what got packaged. It is declared now.

  Two things came out of looking for others like it. Twenty-six more components
  used by build and test tooling turned out to be undeclared in the same way,
  working only because something else in the project happened to pull them in —
  all now declared. And **every release from here on launches the packaged app
  before it can be uploaded**, which nothing had ever done: the checks that ran
  before a release tested the code, never the finished application. That check
  was written against the broken 0.13.0 build itself, so it is known to catch
  this rather than assumed to.
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
  `@` or `[[` in a note, keep typing a title nothing matches, and the picker
  now offers "Create “…”" as its last row.
- **Tags can have icons, like notebooks do.** Right-click a tag in the sidebar
  → "Set icon…", pick from the full icon set, and the `#` becomes whatever you
  chose; "Remove icon" puts the `#` back.
- **Colours can be recoloured.** Right-click a colour in the sidebar and there
  is now a "Change color…" entry alongside Rename — the same picker used when
  you create one, opened on the colour you clicked, with the preset swatches
  and a hex field. Until now a colour's swatch was fixed at the moment it was
  created: the menu could rename it and delete it, and that was all.
- **Archive and Trash select like every other list.** Shift-click a range,
  cmd-click to add and remove individual rows — the same as the notes list.
- **Hypha now asks before leaving a file behind.** Take a picture or a document
  out of a note, and if no other note is using it you get a dialog offering to
  delete it too, with a preview of what you are about to lose.
- **A setting for downloading attachments over cellular, on by default.** Your
  phone has always pulled the full attachment for every file in the vault the
  moment it heard about it, whatever network it was on.
- **Search on the phone, from any screen.** Tap the title at the top of any
  screen and it becomes a search field. It searches the *text inside* your
  notes, not just their titles — which the phone could not do at all before,
  and which the desktop has always had in its title bar.
- **You can see where a drag will land.** Drag anything over a note — a word, a
  picture, a file from Finder — and an accent-coloured line shows the exact
  spot it will be inserted, following the theme in light and dark. The editor
  had no such indicator at all: it was switched off years ago on the grounds
  that the list-drag extension drew its own, and that extension has never drawn
  anything.
- **Double-click a picture to open it.** It opens as a preview beside the note,
  in a pane split off to the right, so the picture and the note it belongs to
  are on screen together.
- **Pictures can be resized.** Hover a picture in a note and drag any of its
  four corners: the width follows the pointer, the proportions are kept, and it
  will not grow wider than the column it sits in.
### Changed
- **Three test gates were failing and had stopped being read.** One pinned the
  editor's drop indicator as *disabled* — the state a comment claimed was
  deliberate and which actually left notes with no drop marker at all, fixed in
  this same release; the gate was holding the old broken shape in place.
- **Settings tells you what happened, where you can see it.** Backing up,
  importing, restoring, rebuilding the search index, purging vector storage,
  saving a publishing target, changing your passphrase, filing older
  attachments — all of these used to answer in a small line at the bottom of
  the section.
- **The picture in a note's list row moved to the right.** It used to sit on
  the left under the title, which made every row with a picture taller than the
  rows around it and shifted the text of those rows sideways. It now sits on
  the trailing edge beside the title and the preview text — the same place it
  has always been on the phone — so more notes fit on screen and the rows line
  up.
- **Archive and Trash open a note beside the list instead of pushing the list
  around.** Clicking a row used to unfold its text underneath it like an
  accordion, so opening a second note shoved the first one's rows down the
  screen and a long note buried everything below it.
- **The search box under each list is gone; the title above it does the job.**
  Notes, Archive, Trash, Reminders and Web Notes each carried their own search
  box that only filtered the rows already on screen, matching titles but never
  the text inside a note.
- **Split-pane and detached-window commands no longer appear on the phone.**
  Five commands — split right, split down, close pane, cycle pane, detach pane
  — were only ever hidden there because the phone had no command palette to run
  them from. Now that it does, they are hidden properly: a phone has no split
  panes and no second window, and running one would have left an editor pane
  you could neither see nor close.
- **Faint text is readable now, on every theme.** Placeholder text — including
  the passphrase fields on the very first screen — was far below the
  accessibility standard on all ten built-in themes, in the worst case almost
  invisible.
- **Backups no longer hand out your tag, notebook and reminder names in the
  clear.** A backup was only ever encrypting your *notes*.
- **The note map is no longer written for whoever built it.** The one cramped
  toolbar row is now a panel down the left, laid out like the app's settings:
  headings, and a sentence under each control saying what it actually does.
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
  itself out inside a box the keyboard was sitting on top of. Every other
  dialog carries that mark; this one, added in this release, did not.
- **A setting's name and its explanation ran together as one line.** In
  Appearance, "Stock themes" and the sentence explaining what resetting them
  does rendered as a single run-on line with no break between them — the label
  and its description were two inline boxes in a plain container, where every
  other row in Settings stacks them.
- **Some panels had no spacing between their sections.** A layout helper built
  its gap size by string interpolation, which Tailwind cannot see when it scans
  the source, so four of the nine possible spacings silently compiled to
  nothing at all. Sync settings, Language settings and the note map's new
  options panel all had sections sitting flush against each other — which looks
  like a deliberately tight design rather than a missing stylesheet rule, and
  so had gone unnoticed.
- **The note map redrew itself differently every time you opened it.** The same
  vault, unchanged, produced a different picture on each open: clusters swapped
  colours, cluster numbers moved around, and nudging the K or density slider
  re-rolled the whole thing again.
- **Pasting text with an `@` in it hijacked the note-link picker, and could
  swallow the paste.** Paste a paragraph that happens to contain an `@` and the
  picker opened over it, treating everything from that `@` to the end of what
  you pasted as one long search.
- **Note links no longer break code open.** Typing `@` inside a code block, or
  inside an inline `code` span, opened the note picker — and picking a note
  from inside a `code` span split the span in two and left the title sitting
  outside it, unlinked. Neither the picker nor the link is offered inside code
  now.
- **Closing a tab now takes you back to the tab you came from.** It used to
  jump to the first tab in the strip — not the one you were last reading, and
  not even a neighbour — so closing a file you had opened to check something
  threw you to the far end of the strip.
- **Dragging a picture inside a note moved nothing — it made a second copy that
  would not open.** Dropping it left the original where it was and inserted a
  duplicate, and right-clicking that duplicate to open it answered "no in-app
  preview for this file type".
- **Tab in a note jumped out of the editor.** Pressing Tab anywhere that was
  not a list moved the focus to the notebook picker at the foot of the window
  instead of indenting, which in the middle of writing is the last thing it
  should do.
- **The editor collapsed runs of spaces.** Two spaces typed in a note rendered
  as one, and a line could not be indented at all: the stylesheet ProseMirror
  requires for whitespace was never loaded, so the editor ran at the browser
  default. Spaces now render as typed, on the desktop and the phone.
- **Settings on the phone.** The attachment list gave four buttons about half
  of every row and truncated the filename to a few characters — the one part
  that says which file it is; the buttons now take their own line and the name
  gets the width.
- **Deleting an attachment asked with a system alert.** Every other destructive
  question in the app is hypha's own dialog; this one was the browser's, which
  on the phone means an iOS alert dropped into the middle of a sheet. It also
  means the sheet could not say "Delete" on the button that deletes.
- **A dialog with nothing to cancel offered Cancel on the phone**, and a
  three-way question — keep a file, move it to the trash, or delete it for good
  — silently lost its middle answer there while the desktop offered all three.
- **One day could end up with two daily notes — again.** This was reported
  fixed once already, and it came back the same week, because the previous fix
  guarded the two ways a daily note gets made against each other rather than
  removing the reason they could disagree.
- **The phone stopped reconnecting after you left Wi-Fi.** Walk out of the
  house — or just switch Wi-Fi off — and the phone would drop its link to the
  desktop and never pick it up again over cellular, until it was back on the
  same network.
- **Long-press menus in the phone's sidebar now open.** Holding a row in the
  sidebar was supposed to give you the same menu a right-click gives on the
  desktop — rename, delete, pin as a shortcut.
- **Links in notes: you can put the cursor in them, and on the phone they open
  at all.** Clicking a link went straight to opening it, which meant there was
  no way to place the text cursor inside link text to edit the words — the
  click was always taken as "follow this".
- **Renaming a colour no longer wipes it out.** Renaming a colour in the
  sidebar made it look deleted: it lost its dot and the notes carrying it lost
  their tint.
- **The rename box for a colour accepts more than one character.** Typing in it
  re-selected everything after each keystroke, so every new character replaced
  the one before it and you could never get past a single letter.
- **The phone no longer quits itself while you have it locked.** Lock the
  screen with Hypha open, come back half a minute later, and you were on the
  home screen with the app starting from scratch — losing whatever you had on
  screen.
- **Opening a note no longer counts as editing it.** Simply opening a note
  wrote it back to disk a moment later, exactly as though you had typed in it —
  which bumped it up a list sorted by Modified, and sent the write out to your
  other devices.
- **A note you edit now stays at the top of the list, on every device.**
  Sorting by Modified, editing a note moved it to the top — and then it slid
  back to where it had been.
- **An open Settings panel now notices what your other devices did.** With
  Settings → Sync open, a device joining or being revoked somewhere else did
  not appear until you restarted the app — and the same was true of Settings →
  Attachments when a file was deleted on another device.
- **Deleting a note now shows up on the Trash screen straight away.** If the
  Trash screen was already open — in a second window, or beside the list you
  deleted from — the deleted note did not appear there until you navigated away
  and back, and a second window kept showing the note in All Notes as though
  nothing had happened.
- **A big sync no longer skips the Archive screen.** When a device came back
  after a while offline, or joined a vault for the first time, it took a
  shortcut and rebuilt the notes list in one go — and that shortcut stepped
  past the Archive refresh.
- **The phone's log now says how much memory the app was holding when it went
  away.** iOS can kill a backgrounded app for several unrelated reasons that
  all look the same from the outside — you unlock the phone and you are on the
  home screen.
- **Typing on the phone no longer drags the whole app around.** Tapping into a
  note brought the keyboard up and left the app with two scrollers: the note
  scrolled, and so did everything behind it, sliding the nav bar off the top of
  the screen while the formatting toolbar disappeared behind the keyboard.
- **A device that was refused now says so, instead of pretending to sync.** If
  you joined a vault with an invite link that had already been used, or that
  had expired, or from a device the owner had since revoked, the join appeared
  to work: the vault was registered, your passphrase opened it, and the app
  looked entirely normal.
- **Daily Notes on the phone opens today's note.** Tapping Daily Notes in the
  sidebar landed on the day timeline, which is a date picker whose answer is
  the same every day — two taps to reach the note you wanted.
- **Reordering the sidebar shortcuts now reaches your other devices.** Dragging
  a pinned notebook, tag or favourite note into a different position was only
  ever stored on the machine you did it on — the order lived in local browser
  storage, where no sync path could reach it — so every other device kept the
  old arrangement forever.
- **Settings changes no longer wait for an unrelated edit before syncing.** The
  same underlying fault held up everything stored as a setting: the sidebar
  colour order, date and time formats, the toolbar layout, your publishing
  target and profile.
- **A selected image shows it.** Clicking an image in a note gave you no sign
  it was selected — the video player has always drawn a ring when you pick it,
  and the image, which is all picture and has no caret to read, had nothing at
  all. It now draws the same ring, on the picture's own edge rather than the
  full width of the line, and on the placeholder if the image is still
  arriving.
- **The window buttons on macOS sit on the same line as the title-bar icons.**
  The red/yellow/green buttons were drawn two pixels above the row of icons
  beside them, which is exactly the kind of misalignment you see without being
  able to name it.
- **Every theme is on the page; the theme list no longer scrolls inside a
  scrolling page.** Settings → Appearance capped the theme grid at a little
  over half the window height and gave it its own scrollbar, so you were
  scrolling a small box inside a scrolling pane and the wheel went to whichever
  of the two the pointer happened to be over. The grid now grows to its full
  height and the settings pane scrolls it, like every other section.
- **Tapping a phone search result opens that note, at the line it found.** On
  the phone, picking a result from the new title-bar search moved to the editor
  but left whatever note was already open sitting there — and picking a
  command, a tag or a notebook ran the wrong one, whichever happened to sit at
  that position in the unfiltered list.
- **Checklists put the text next to the checkbox again.** Every row in a
  checklist rendered its checkbox on its own line with the text underneath it,
  in the editor on the desktop and on the phone.
- **The "Checklist" list type lost everything typed into it.** Choosing
  *Checklist* (as opposed to *Simple checklist*) produced a list that showed no
  rows at all, and the text in it was dropped on the way to storage — a
  checklist saved by an earlier version came back empty, or as an empty bullet
  list.
- **A note someone else trashed or archived turned your typing into duplicate
  "Untitled" notes.** With a note open on this device and the same note trashed
  or archived on another, the open editor quietly stopped being bound to it and
  became a *draft*: every few seconds of typing forked a brand-new "Untitled"
  note holding the whole body, and none of the edits reached the real note.
- **A note trashed on another device stayed in All Notes.** The sync path
  decided a note was still live by asking whether the database still returned
  it — but a trashed note *is* still returned (the row is a tombstone, not an
  absence), so a peer's trash was read as an ordinary edit and the note was put
  straight back in the list. Trashing now replicates to the list on both the
  sync path and the between-windows path; previously neither carried it.
- **macOS packaging never ran: the notarization block was written in the
  previous electron-builder's syntax.** electron-builder 26 made `mac.notarize`
  a plain boolean; the `{ teamId: … }` object it replaced is not deprecated
  there, it fails schema validation, so every `--mac` leg died in the config
  validator before packaging started.
- **The release build failed at the iOS bridge-frame gate.** The user's
  diagnostic-logging flag (`__hyphaLoggingEnabled`, shipped in 0.12.0) is the
  fifth non-bridge user script the shell injects into all frames, alongside the
  `crypto.randomUUID` shim, the CPU probe and the two debug flags — but it was
  never added to the gate's allowlist, so `release:local` refused every build
  after it landed.
- **"Back up now" worked once and then seemed to do nothing.** On the phone the
  first manual backup landed and the second changed nothing at all: the button
  stayed enabled, tapping it produced no file and no message.
## [0.12.0] - 2026-08-19

### Changed
- **Hypha's licence has changed, and Hypha is no longer open source.** It is
  now *source available* under the Hypha Source Available License 1.0.
- **The brand is written `hypha`, in lowercase, and the App Store listing is
  called "hypha notes".** The name "Hypha" was already reserved by someone else
  on the App Store, and the listing name has to be globally unique — so the
  store entry carries the longer name while the app on your home screen is just
  **hypha**.
- **The iOS app has a new identifier, so it installs as a new app rather than
  an update, and it has to re-join your other devices.** It changed from
  `app.hypha.mobile` to `app.miniml.hypha.ios`, under a new Apple developer
  account.
- **The desktop app also has a new identifier** (`org.hypha.desktop` →
  `app.miniml.hypha.desktop`). Your notes are untouched — macOS and Windows
  treat the old and new data directories as the same place — but macOS sees a
  new app and will ask for **Local Network** permission again the first time
  you sync.
- **Automatic backups are a desktop feature now; on iPhone, backups happen when
  you ask for them.** The schedule was never going to work on a phone and the
  way it failed was the bad way — quietly. iOS suspends an app shortly after
  you leave it, and a suspended app runs no timers, so "back up daily" only
  ever fired if you happened to open Hypha and leave it open.
- **A new app icon on both platforms**, drawn from the redrawn `hy` monogram.
- **macOS 12 (Monterey) is now the declared minimum.** It was always the real
  floor, inherited from Electron; it just was not written down, so the
  installer would happily install onto a Mac the app then crashed on at launch.
- **"Full offline mode" is gone; in its place is "Download attachments
  automatically", and unlike its predecessor it does something.** The old
  checkbox's value reached a parameter no syncer ever read — there was no
  consumer of it anywhere, on either host, for its whole life — while the
  behaviour it claimed to control ran unconditionally: every connection swept
  the whole vault for attachments, so a phone joining pulled down every file in
  it.
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
  collecting, in one place, everything that is missing, unproven or
  deliberately absent; and a privacy policy. The honest headline from the
  security page is that only *notes* are encrypted — tag and notebook names,
  reminder text and attachment filenames are stored in the clear, including
  inside a backup file.
- **A list of the third-party components Hypha includes and their licences.**
  This was owed before and had never been written.
- **Type `@today` in a note to link to that day's daily note.** The `@` menu
  that links to another note now understands `@today`, `@tomorrow` and
  `@yesterday`, and offers the matching daily note — creating it if it does not
  exist yet.
- **Archive, Trash and Web Notes look like the notes list now, and their rows
  open.** All three drew their own cramped list with actions that only appeared
  on hover, and in Archive and Web Notes clicking a row did nothing at all.
  They use the same row as the notes list, and clicking one opens it: read-only
  in Archive and Trash, in the normal editor in Web Notes.
### Fixed
- **On iPhone, the on-screen keyboard covered the bottom of the note you were
  typing in.** iOS does not shrink a web page's layout for the keyboard, so the
  lower part of every screen — the note's text above all — was laid out behind
  it.
- **The `/` menu in the editor listed a code word beside every entry.** Typing
  `/` at the start of a line opens a menu of formatting actions, and each row
  was printing the internal *name* of its icon as text — "remove-formatting
  Clear formatting", "list-ordered Numbered list". It now draws the icon, as
  the toolbar always did.
- **Sync settings put the master switch below everything it switches off.** The
  "Enable sync" and "Full offline mode" options sat at the bottom, under the
  whole list of paired devices.
- **An archived note did not show up in Archive until you restarted the app.**
  Archiving removed the note from All Notes immediately and reached your other
  devices immediately, but the Archive screen itself only rebuilt its list when
  you navigated to it fresh — so if you were already looking at it, or looking
  at a second window, the note simply was not there. It appears at once now,
  whether the archiving happened here, in another window, or on another device.
- **Archived notes were fully editable.** "Archived" meant the note left the
  main list and nothing more: a tab left open when you archived, or a link to
  an archived note, gave you an ordinary editor that saved and synced every
  keystroke. Archived notes are read-only now, like notes in the trash, with an
  Unarchive button where the formatting toolbar used to be.
- **A note could end up with its own text twice, permanently, on every
  device.** A note's text lives in two places, and a note opened before its
  text had arrived from your other device would convert the copy it had into
  the shared document — producing a second copy of something that was already
  there.
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
  Updates → Logging only ever reached the app's main window.
- **The *What's New* window showed a stale, built-in copy of the release
  notes.** It fetches them from a public repository, and that repository was
  empty — no branches at all — so the fetch had been failing for every
  installed copy of Hypha since the source moved private.
### Removed
- **The "check for new versions" setting, which never checked anything.** The
  setting existed, defaulted to on, and promised a daily check — but the code
  that would have performed it had never been written, so turning it off
  changed nothing and leaving it on got nothing. Updating still works as it
  always did; only the setting that misdescribed it is gone.
### Tooling / Dependencies
- **Release credentials can live in a gitignored `.env`.** A signed and
  uploaded release needs six App Store Connect and notarization variables, and
  a shell export is lost the moment the terminal closes — discovering that
  after a 20-minute build is the failure this prevents.
- **The version bump now cuts the changelog, and the public copies have a sync
  step.** Bumping a version left the notes for it under `[Unreleased]`, which
  the *What's New* window skips — so a new version would have appeared in the
  app with nothing under it.
## [0.11.0] - 2026-08-18

### Added
- **A way to find out what an extra open vault costs.** Nothing on the desktop
  has ever been measured — every power instrument this project has is for the
  iPhone — while on the desktop each open vault quietly runs its own network
  stack.
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
  icon in the Dock, the app switcher and every file dialog, and the iPhone
  build had none at all.
### Changed
- **The screen you see before your vault exists now names its fields.** The
  passphrase boxes on the first-run screen were labelled only by the grey hint
  text inside them — which vanishes the moment you type, is the faintest text
  in every theme, and is not a name a screen reader can announce.
- **"What's New" and the update check point somewhere they can be read.** Both
  pointed at a private location, so the release-notes fetch and the link to a
  release both failed silently for everyone; the window quietly fell back to
  the notes built into the app, which is why this was not visible.
### Security
- **A web page embedded in a note could reach into the app on your iPhone.** A
  note can hold an embedded web page, and notes arrive from the people you sync
  with — so the page inside your note may be someone else's website.
- **Your search terms and the names of files you opened were kept in plain text
  on your iPhone too.** The same problem fixed on the computer in 0.10.0 was
  still there on the phone: the record of your open tabs held the exact text
  you last typed into search, the real filename of any attachment you had open,
  and a fingerprint of that file's contents — unencrypted, in the app's own
  files, which is exactly what a computer you have trusted can copy off the
  phone.
- **The app's own screen could have been replaced by another web page on
  iPhone.** Nothing was known to be able to do this, and that is the point:
  what kept it from happening was three unrelated details of how links, windows
  and pop-ups happen to be set up, none of them written down as a rule and any
  of them changeable by accident.
- **Every reminder you had set was sitting in the iPhone's own notification
  store, with its title, months ahead of time.** When you set a reminder, the
  phone has to be told about it in advance — that is the only way it can alert
  you while Hypha is closed.
- **Joining a vault left an invisible, empty leftover vault behind every time,
  and a mistyped passphrase left the app pointing at a vault you had never
  opened.** When you add a vault, Hypha has to prepare one before it can ask
  whether you are making a new one or joining someone else's.
### Fixed
- **A file that had finished transferring to your phone was reported as never
  having arrived.** A 64 MB attachment reached the device, was stored, and took
  up its 60 MB — and every attempt to open it answered "this attachment's file
  hasn't reached this device yet".
- **An attachment inside a note could not be opened on iPhone.** The file chip
  in a note's body responded only to a double-click, and on iOS a double-tap
  inside text is how the system selects a word — so the tap never reached the
  app and the chip did nothing at all, while still showing the pointer that
  says it can be clicked.
## [0.10.0] - 2026-08-18

### Security
- **Adding a photo to a note left a full-size copy of it, GPS and all, sitting
  in the app's files on the phone.** Not a thumbnail and not encrypted — the
  original image, under its own filename, with everything the camera recorded
  in it: the model of phone, the date and time, and where you were standing.
- **Your search terms, and the names of files you opened, were kept in plain
  text on your computer.** The file that remembers your open tabs also
  remembered the exact text you last typed into search, the real filename of
  any attachment you had open, and a fingerprint of that file's contents.
- **Opening an attachment in another app left the decrypted file where other
  people using the computer could read it.** Hypha writes the file out so the
  other app can open it.
- **The folder holding your attachments was readable by other accounts on the
  computer, and its filenames give away what is in it.** The files themselves
  are encrypted and reveal nothing when opened — but each is named after a
  fingerprint of its contents, so being able to *list* the folder answers "does
  this person have this exact file".
- **The list of your vaults' names was readable by other accounts too**, and is
  now private. It stays unencrypted on purpose: it has to be readable before
  any vault is unlocked, or you could not choose which one to open.
- **Your notes were readable in the phone's own files, with no key needed at
  all; the database on the phone is now encrypted.** Moving the keys into the
  Keychain (below) was the smaller half of this problem. **This is not an
  automatic upgrade**: a vault created before this change cannot be opened by
  this version and is not converted in place — remove the vault on the phone and
  re-join it from your computer.
- **The iPhone kept your vault's keys in plain text; they now live in the iOS
  Keychain.** Everything that protects a vault on the phone — the key that
  decrypts your notes, this device's identity, the owner key that proves who
  may invite others, the shared sync secret, the membership credential and any
  stored invite — was written to ordinary browser storage inside the app, with
  no encryption of any kind. **This is not an automatic upgrade.** No attempt is
  made to move the old keys: remove the vault on the phone and re-join it from
  an invite on your computer.
- **Correction: a backup file is not fully encrypted, and never was.** Hypha's
  own notes said a backup "is always encrypted", on the grounds that it carries
  the database's own already-encrypted contents. That is true of your notes and
  nothing else: tag names, notebook names, reminder titles and descriptions,
  settings, and attachment filenames, types and sizes are all in a backup in
  plain readable form. Nothing about this changed in this release — the claim
  was wrong, and you may have put backup files somewhere on the strength of
  it.
- **The iPhone's app switcher held a picture of the note you last had open.**
  When iOS sends an app to the background it photographs the screen, so it has
  something to show on the app-switcher card — and it stores that picture among
  the app's own files.
- **Attachments you opened in another app, and photos you inserted, were left
  unprotected in the phone's files.** Opening an attachment in another app, and
  exporting or backing up, both write a decrypted copy into a working area
  first; inserting a photo writes the **full-size original** there, which for a
  camera photo or a raw file can be very large.
- **A stored attachment's filename revealed which file it was.** Attachment
  contents have always been encrypted. But each stored file was *named* after a
  fingerprint of its unencrypted contents — so anyone who could see a list of
  those files, and who already had a copy of some document, could work out
  whether that exact document was in your vault, without decrypting anything.
- **On desktop, the keys to your vault could be written unencrypted — and one
  badly-timed crash could destroy them.** Hypha stores the key that decrypts
  your notes in your operating system's keychain.
### Fixed
- **Your reminder titles, your search terms and your attachment filenames were
  being written to the iPhone's system log.** Hypha forwards its diagnostic
  output to the iOS log so that problems can be investigated on a real device.
## [0.9.0] - 2026-08-17

### Added
- **Scan an invite QR with your iPhone to join a vault.** Point the Camera at
  the code another device is showing, tap the notification, and the phone
  creates the vault and joins it.
### Fixed
- **Settings showed one vault's sync and devices under another vault's
  heading.** With more than one vault, Settings lists each vault's sections
  separately — but clicking Sync under a second vault kept showing the first
  one's owner fingerprint, its device list, its connected peers and its
  last-synced time.
- **The sidebar kept showing the vault you had just left.** After switching
  vaults, the sync line in the sidebar went on reporting the previous vault's
  connected devices and its last-synced time.
- **Finishing an invite left you on a blank screen, on any device.** Accepting
  an invite — by link or, now, by scanned code — tried to open a Settings page
  that no longer exists, and rendered nothing at all.
- **"Remove orphaned" could delete files that were still in use.** The list of
  unused attachments is worked out by reading every note and seeing which files
  they mention. Deleting an attachment removes it from **every** device and
  cannot be undone, so this could throw away a photo that was sitting in a note
  you had open somewhere else.
- **Trashed notes show their real titles again.** Every note in the trash
  listed as "Untitled" with "no additional text" underneath, whatever it was
  actually called and whatever it contained.
- **The trash lists files as well as notes.** Deleted attachments now appear
  there alongside notes and notebooks, and can be restored or deleted for good
  from the same place.
- **You can read something before deciding to delete it.** Clicking an item in
  the trash opens a read-only preview — the note as it actually looked, with
  its headings, lists, formatting and images, or the name, type and size of a
  file. Nothing in the trash can be edited: the preview has no way to save.
- **Deleting an attachment can be undone.** Until now, deleting a file from
  Settings → Attachments erased it immediately, on every one of your devices,
  with no way back.
- **Attachments in the trash are no longer treated as unused.** A note in the
  trash can be restored, but the app had stopped counting it as a user of its
  own pictures and files. So "Remove orphaned" offered those files up for
  deletion — and deleting one removes it from every device with no way back, so
  restoring the note afterwards gave you the note with its images missing.
  Emptying the trash, or a note ageing out of it, is what releases them — so
  the reversible step stays reversible, and the irreversible one is the one you
  choose.
- **The Peers popover in the sidebar is readable.** Clicking the sync line at
  the bottom of the sidebar opens a small panel listing the devices in your
  vault.
- **The frosted-glass panels had no frosting.** When the window is translucent,
  panels like the Settings cards and the vault passphrase screen are meant to
  be a tinted sheet of glass — you see your desktop through them, dimmed.
- **The invite QR could grant more than the panel said it did.** When you added
  a device, the role you picked and the code on screen could disagree: the QR
  and link were only generated when the panel opened or when you pressed the
  button, so changing the role afterwards left the previous code sitting under
  the new label.
- **More colours that only worked on a dark theme.** Pinned and starred
  markers, shortcut and favourite icons, the reminder chips, the daily-notes
  dot, and the error messages in Publishing and the changelog were all drawn in
  fixed colours chosen against a dark background.
- **On a light theme, the "delete permanently" buttons were invisible.** In the
  trash, the archive, the reminders list and web notes, the button that
  destroys an item for good was drawn in a pale pink that had been picked to
  sit on a dark background.
- **"Search by meaning" missed everything that arrived from another device.**
  Notes you wrote on this computer were understood by search; notes that synced
  in from your phone or another laptop were not, and neither were notes brought
  back from history.
- **"Rebuild search index" left search by meaning worse than it found it.** It
  cleared the index first and then failed to refill it, so the button you press
  when search feels wrong was the one that emptied it. It repaired itself on
  the next launch, slowly, by re-reading the whole vault.
- **Notes were being read by the model twice, and with the feature switched
  off.** Every save ran the text through the language model once for a result
  that was then thrown away, and again to store it.
- **A file too big to sync was offered over and over.** When one device holds
  an attachment larger than another will accept, the second correctly declines
  it — and then asked for it again every time the two reconnected or exchanged
  changes.
- **Sync failures never reached the sync indicator.** When syncing failed for a
  reason that isn't a single file — a vault that can't be opened, a peer that
  can't be understood — the app was supposed to stop claiming everything was
  fine and show "Sync error".
- **Search by meaning now notices when the way it reads notes changes.** The
  index records what built it — the model, its settings, and how notes are
  split into passages — and rebuilds itself when any of those change.
### Changed
- **iPhone: the vault switcher is not a settings section any more.** It used to
  sit at the bottom of Settings, below a screenful of scrolling, built from the
  same rows and chevrons as everything above it — so it read as a section
  called "Vaults".
- **Settings: "Devices" and "Sync" are now one section.** They were two places
  answering one question. Devices held who is in the vault — start or join,
  invite, revoke; Sync held the connection — last synced, sync now, the offline
  toggles — and, at the bottom, a second list of the same devices showing which
  ones were currently connected.
- **iPhone: adding a device is one tap from anywhere.** Tapping the sync dot in
  the navigation bar used to open a sheet that told you the state of things and
  then, if you wanted to do anything about it, sent you to Settings → Sync.
## [0.8.1] - 2026-08-16

### Fixed
- **iPhone: the app could stop finding your other devices, and stay that way.**
  0.7.1 made this one visible — if the app failed to claim the network port it
  listens on, it said so instead of pretending all was well.
### Changed
- **iPhone: version history now slides up from the bottom of the note instead
  of covering it.** It used to open as a full screen with its own back button,
  which hid the very note you were comparing against — and it arrived carrying
  the desktop's sizes: entries you could barely tap, and a "Restore this
  version" button about half the size Apple asks for.
## [0.8.0] - 2026-08-16

### Added
- **Attachments can be tagged, filed in notebooks, and given a colour — and
  they do it themselves.** A file used to carry nothing but its name, its type
  and its size, so the only way to find one was to remember what it was called.
- **iPhone: "Colorize blocks" can now be turned on for a single note.** The
  device-wide default was in Settings, but the per-note switch lives in the
  desktop editor's toolbar — and the phone replaces that toolbar with the bar
  above the keyboard, which has nowhere to put it.
### Changed
- **The editor no longer tells you that it saved.** It used to read "Saved"
  from the moment you typed your first character until you closed the note,
  flipping to "Saving…" every time it wrote — a word blinking beside your text
  for the whole time you were writing, to report the thing that is true of
  every save.
- **iPhone: Hypha now requires iOS 16.4 or later** (it was 16.0). No iPhone is
  left behind by this: iOS 16.4 came out in March 2023 and runs on every device
  iOS 16.0 runs on, so any phone that could open Hypha before can still open it
  after a free update it has already been offered.
- **iPhone: your vault is now written to disk as you work, instead of being
  saved as a whole copy on a timer.** Until now the phone kept your entire
  vault in memory and wrote the whole thing out again shortly after you stopped
  making changes — which meant the cost of saving grew with the size of your
  vault, and anything written since the last copy existed only in memory.
### Fixed
- **iPhone: a note you had just written could be lost if the app was killed
  moments later — and a vault you had just created could vanish entirely.** The
  phone keeps your vault in memory and writes it out shortly after you stop
  making changes.
- **iPhone: the bar above the keyboard could sit behind the keyboard.** Tapping
  into the middle of a long note raised the keyboard over the formatting bar,
  which then only reappeared once you had scrolled back to the top. Introduced
  in 0.7.1, as a side effect of removing a blur effect that rendered nothing —
  the blur was also, invisibly, the only thing keeping the bar drawn on top.
- **A failed save could quietly stop a note from receiving edits from your
  other devices.** If a write failed, the editor went on believing one was
  still in progress — and while it believes that, it refuses to take in changes
  arriving from another device, to avoid overwriting what you are typing.
- **iPhone (development builds only): launching from the home-screen icon
  showed a blank white screen.** A build started from the icon gets none of the
  settings Xcode passes in, so it looked for a development server on the phone
  itself, where nothing is listening. It now loads the built app in that case,
  which is what a release build has always done.
### Tooling / Dependencies
- **Releases now run every iPhone test, and the linter, before they build.**
  They already ran three of the nineteen iPhone tests, but only if you passed
  an extra flag — and one of those three had been failing all along over the
  data loss fixed above.
- **A mobile smoke that kills the app without warning — landed deliberately
  red.** The phone keeps its vault in memory and writes the whole thing out on
  a timer, so anything written since the last write-out is lost if the app dies
  uncleanly.
## [0.7.1] - 2026-08-16

### Fixed
- **iPhone: a discovery problem that could hide itself.** If the app failed to
  claim the network port it listens on for other devices — which can happen
  when Wi-Fi changes at just the wrong moment — it carried on as though nothing
  had gone wrong, and simply never heard another device again.
### Changed
- **iPhone: the app does less drawing and fewer wakeups while idle.** Every row
  in every list was permanently held in the phone's graphics memory in case you
  swiped it, and the bar above the keyboard was applying a blur effect over a
  background you can't see through — invisible, but not free.
## [0.7.0] - 2026-08-16

### Fixed
- **iPhone: the app no longer heats up the phone.** This is the real fix for
  it. The part of the app that finds your other devices was asking the system
  "can I send data yet?" — and the system, having nothing to send, answered
  "yes" **38,000 times a second**, every second the app was open. Measured on
  the device: more than a full core down to **0.5%**. **The 0.6.0 note below was
  wrong** and is corrected there — those changes are real improvements, but they
  were not what made the phone hot.
## [0.6.0] - 2026-08-16

### Added
- **Indent and outdent buttons in the editor toolbar.** Nesting a list used to
  need the Tab key, which is fine on a laptop and impossible on a phone — the
  iPhone keyboard doesn't have one.
### Fixed
- **iPhone: the app does much less work while you type.** *(Corrected: this was
  first published as the fix for the phone getting hot. It was not — see 0.7.0.
  The improvements below are real, but the heat had a different cause
  entirely.)* The phone used to rewrite your entire vault to storage every time
  anything changed; it now saves after you pause, and at most every 30 seconds
  during a long stretch of typing. *(This entry originally insisted the
  device-finding connection was not the cause. That was exactly backwards — see
  0.7.0.)*
- **Bullet lists show their bullets again.** Every bulleted list in every note
  was rendering as plain indented text with no dots at all, on the computer and
  on the phone.
- **iPhone: the Collections screen is one screen again.** Three things on it
  were wrong at once. The favourite ★ on a notebook or tag row was half the
  size of the ★ on a colour row just below it.
### Changed
- **iOS: the app no longer zooms like a web page.** Pinching with two fingers
  magnified the whole app — the note list, the nav bar, settings — the way a
  web page zooms in a browser, and there was no way to undo it: the zoom stuck
  across every screen and nothing in the app could put it back.
## [0.5.3] - 2026-08-15

### Fixed
- **The iPhone no longer gets hot looking for a network it doesn't have.** Out
  of coverage — a train, a tunnel, a day out with one bar of 5G — the app kept
  trying to reach the wider internet every minute, forever.
- **Devices stop dialling each other over the internet when they're already
  talking on the local network.** When your phone and computer are on the same
  Wi-Fi they find each other twice — once locally, once over the wider internet
  — and Hypha keeps the local connection because it's faster.
### Changed
- **The phone tells you what sync is doing, from every screen.** There is now a
  small status dot in the top bar of every screen — green when a device is
  connected, grey when there's nothing to talk to, red when something is wrong.
- **On cellular, sync respects Low Data Mode and Low Power Mode.** Ordinary
  mobile data is fine and syncs as usual; it's only when you've also asked iOS
  to economise that Hypha stays off the wider internet until you're back on
  Wi-Fi.
- **The app recovers if iOS reclaims the page while it's in the background.**
  On a busy phone iOS can throw away a background app's screen contents to free
  memory.
## [0.5.2] - 2026-08-15

### Fixed
- **Sync works again on the computer.** Since 0.3.0, the desktop app has not
  synced with anything at all: starting sync failed immediately, every time, on
  every vault.
## [0.5.1] - 2026-08-15

### Fixed
- **The iPhone stops doing search work it then throws away.** Semantic search
  was switched on by default there, but an iPhone has nowhere to keep the
  embeddings it depends on — so on every single launch the app treated every
  note as unindexed, downloaded a ~94 MB language model, and worked through the
  whole vault computing embeddings that were discarded as fast as they were
  made.
### Changed
- **Settings → Search names the right model.** It still described
  `snowflake-arctic-embed-s` at "~33 MB"; the app has since moved to
  `granite-embedding-97m-multilingual-r2`, which is ~94 MB.
## [0.5.0] - 2026-08-15

### Fixed
- **Saving a large file out of a note works again.** In 0.4.0, Download did
  nothing for any attachment over about 32 MB — it stopped with an error about
  the file being too large, on exactly the files most worth getting back out.
### Changed
- **Opening a file in another app no longer loads it into memory first.** "Open
  externally" used to read the whole attachment at once before handing it over
  — the same thing Download stopped doing in 0.4.0.
- **Backups copy attachments in pieces too.** Taking a backup with attachments,
  and restoring one, used to hold each file whole while it was copied.
- **Quitting during a save no longer leaves a stray file behind.** Closing the
  app while a file was being saved out of a note left the half-written copy on
  disk. It is now cleaned up on the way out, and files staged for "Open
  externally" are cleared out after an hour rather than kept forever.
## [0.4.0] - 2026-08-14

### Added
- **You can add audio and video to a note on the iPhone.** There was no way to
  at all: the formatting bar above the keyboard offered images and nothing
  else, and dragging a file or pasting one — the two other ways in — are not
  things you can do on a phone.
- **Photos that show a grey placeholder can be given a picture, on the
  iPhone.** Camera raws, and every iPhone photo added before 0.3.0, were stored
  exactly as you gave them and nothing on any device could open them to draw —
  so they show a placeholder in the note and a blank tile in the list,
  permanently.
### Changed
- **Downloading an attachment no longer loads it into memory first.** Saving a
  file out of a note used to decrypt the whole thing at once — fine for a
  photo, and the reason a very large video could fail on a device with less
  memory than the file.
### Fixed
- **A file you have just added can no longer be deleted as "unused".** Adding
  an attachment and writing it into a note are two separate steps, and in the
  moment between them nothing in your notes referred to the file yet — so
  "Remove orphaned" in Settings → Attachments would offer it up and delete it,
  on every device.
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
  until you came back.
- **Large photos, videos and files now actually reach your other devices.**
  0.2.3 could only tell you when a file was too big to send; sending it was
  named there as the next piece of work, and this is it.
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
  download at risk.
### Fixed
- **Devices could only ever sync on the same Wi-Fi.** Hypha is meant to find
  your other devices two ways: directly over the local network, and over the
  internet through a distributed lookup — the second being what lets a laptop
  at home and a laptop at work stay in step, and what an always-on relay exists
  to be found by.
- **A file too big for your iPhone was sent to it anyway, over and over.** When
  a computer held an attachment larger than the phone would accept, the phone
  said so, the computer agreed — and then sent the entire file regardless.
- **Syncing went quiet for a while after your iPhone had been asleep.** Locking
  the phone kills its connection to your computer, but the computer carries on
  believing the two are still talking — so when the phone tried to reconnect,
  it was turned away as a device that was already connected.
- **An always-on relay sent every attachment to every device in the vault.**
  When two computers moved a large file through a relay, every other device on
  the vault — your phone included — was sent the whole thing, whether or not it
  had asked for it or had any use for it.
- **A device syncing through an always-on relay could not turn a file down.**
  When a device decides it does not want an attachment — it already has it, or
  the file is bigger than that device can open — it says so, and the sender
  stops.
- **Very large attachments could quit the app when you opened them.** Since
  large files started syncing between devices, a phone could receive a file far
  bigger than it could open — and playing or previewing one loads the whole
  thing into memory at once, several times over.
- **Photos kept in their original format still had no thumbnail on your other
  device.** 0.2.3 fixed this only on the device the photo was added on; the
  note list on the *other* device went looking for the original file, which no
  computer can open, and left a blank tile — after doing a lot of work to find
  that out. The list now uses the viewable copy everywhere.
- **Quitting the app could lose whatever you had typed in the last few
  seconds.** Your note itself was always safe — this was the saved *version* in
  note history, which is supposed to capture where you left off when you quit,
  and never once did on the desktop.
- **A note opened in its own window did not sync what you typed in it.** The
  edit was saved, and it appeared in your other windows on the same computer —
  it just never left the device.
- **Version history sat on "…" instead of showing the version you opened.** The
  older version had already loaded; the panel simply did not notice, and kept
  its placeholder until something unrelated made it redraw — at which point
  every version you had opened appeared at once. It reads as a fluke, which is
  why it survived so long.
- **Daily notes could stop working entirely on a device.** A single note whose
  title had gone missing was enough: the code that keeps daily notes in order
  gave up on the whole list rather than skipping that one note, so today's
  daily note stopped being found or created. Seen on an iPhone and in an
  account window.
- **Six toolbar buttons were blank on iPhone.** Undo, redo, code block, table,
  insert date and clear formatting drew nothing at all — the buttons worked if
  you knew where to press. Two of them named symbols that do not exist, and the
  rest only appeared after some other part of the app had loaded its full set
  of symbols, which made them look intermittent rather than missing.
- **The always-on relay could not be installed by following its own
  instructions.** Two breaks on the way to a running `hypha-peer`, both in the
  first five minutes: the daemon had no `--help` at all, so the check the
  deploy guide gives you for a successful install could never pass and reported
  a correct install as broken; and the documented `npm install -g` step is
  something npm refuses outright for a workspace package. `--help` now exists
  (and lists every command and option), and the install is the one that
  actually works — drop the bundle and its dependencies in a directory, with a
  wrapper at the path the systemd unit expects.
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
  kept arriving on the phone, so syncing looked like it was working.
- **Syncing did not come back after the phone had been locked for a while.**
  iOS shuts down a sleeping app's network connections without telling it, so
  the phone stopped announcing itself and nothing tried again.
- **Adding camera raws (DNG) or very large photos quit the app on iPhone.** A
  raw file is small on disk but enormous once opened — a 95 MB DNG becomes 186
  MB of image in memory — and Hypha opened every picture it was given, at full
  size, before deciding what to do with it. iOS shut the page down mid-insert,
  which cost a deletion and four photos in one sitting.
- **Adding several photos at once quit the app on iPhone.** Picking three or
  four pictures from the photo library reloaded Hypha with an empty note and
  nothing saved.
- **Images in a note leaked memory every time you opened it.** Each visit kept
  another full copy of every picture in the note until the app was restarted.
  Long sessions with image-heavy notes should feel steadier.
- **iPhone photos kept as originals were invisible on the desktop.** Photos
  from an iPhone are HEIC files and no desktop browser can open one — so a
  photo added on the phone and kept in its original format synced correctly,
  arrived correctly, and showed as a broken image on your Mac.
- **Photos kept in their original format had no thumbnail in the note list.** A
  camera raw or iPhone photo displayed properly inside the note but left a
  blank tile in the list beside it. The list now uses the same viewable copy.
### Added
- **Camera raws and iPhone photos now work, and you choose what to keep.**
  Hypha makes a viewable copy of each one — an iPhone does this without ever
  unpacking the full picture, so a 95 MB raw becomes a sharp 1.4 MB copy in
  about two seconds — then asks once per batch whether to keep the originals as
  well.
- **A photo or video too big to send now says so, instead of looking broken.**
  Files above Hypha's transfer limit were refused by the device holding them,
  and the device waiting for them was never told — so a picture added on your
  phone showed up on your laptop as a blank grey box that never resolved,
  looking for all the world like a slow connection.
### Changed
- **The keyboard's grey ↑ ↓ ✓ bar is gone on iPhone.** iOS adds that bar for
  web pages with lots of form fields, so you can jump between them — a note has
  one field, so both arrows did nothing and it sat on top of Hypha's own
  formatting bar taking up a row of screen. Use the formatting bar's chevron to
  put the keyboard away.
## [0.2.2] - 2026-08-11

Six iPhone fixes from a day of actually carrying the app. Nothing here changes
syncing or your notes — it is all the app being usable in one hand.

### Fixed
- **Taking a photo into a note crashed the app.** Insert image → "Take Photo"
  quit Hypha instantly, every time: iOS shuts an app down on the spot if it
  reaches for the camera without declaring why it needs it, and we never did.
- **The keyboard covered things you needed to tap.** On iOS the keyboard slides
  over the page rather than making room, so anything anchored to the bottom of
  the screen ends up underneath it.
- **The formatting bar itself sometimes ended up under the keyboard.** Two
  causes: pinch-zooming while typing dropped it, and a keyboard change the app
  was never told about — coming back from another app, typically — left it
  parked where it was. Both fixed.
- **Tapping the note you just came back from did nothing.** Open a note, go
  back to the list, tap that same note: nothing happened, and it stayed
  unreachable until you opened a different note first. Tapping a pinned
  notebook had the same bug from the other direction — it opened whatever note
  was already open instead of showing the notebook.
- **Returning to the app looked like it had restarted.** A white flash and the
  app starting over. iOS reclaims memory from backgrounded apps and Hypha's
  page is a fat target; the recovery is a reload, which is fine, but it ran
  while the app was still off-screen and flashed white on the way back.
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
  never saved. *If you hit this, the invitation really is used up: remove the
  vault on the phone and re-join from a fresh invite.*
- **The note that was already open when you started the app didn't sync your
  edits.** Reopening the app restores whichever note you had open, and that
  happens before syncing has finished starting up — so that one note was never
  registered for live sync.
- **A note open on two devices could stop showing the other device's changes
  once you started typing.** Incoming changes are never applied on top of what
  you are in the middle of writing — but they were then forgotten rather than
  applied a moment later, so they stayed invisible until the note was closed
  and reopened.
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
  unreadable — on both.** Attachments are encrypted individually, so two
  devices that add the same picture while apart each produce a *different*
  encrypted file from the same original. Existing attachments are moved to the
  new naming quietly in the background after you unlock, a little at a time,
  and stay readable throughout; nothing is re-encrypted and nothing is deleted
  until its replacement has been written and read back.
- **A note Hypha could not decrypt looked like an ordinary untitled one.** If a
  note's key cannot be unwrapped — a note carried over from another vault, a
  half-restored backup — its title cannot be read, and the note was shown with
  the same blank "Untitled" every note you never got around to naming shows.
- **A paired iPhone could stop syncing entirely.** A bug introduced in the last
  round meant that the moment another device was found, an internal error threw
  in the middle of the introduction — so the connection was abandoned before it
  finished.
- **A single bad message could make an attachment permanently unreadable.**
  Because an attachment's file is encrypted before it travels, the receiving
  device cannot tell a genuine file from a forged one until it opens it — and
  once it had stored anything under that attachment's name, it never asked
  anyone else for the real one. Nothing is deleted in the process — the file
  that would not open is kept until a good one arrives to replace it.
- **With two vaults open, one vault's reminders never fired.** Reminders were
  scheduled for the whole app rather than per vault, so whichever window most
  recently updated its reminders took ownership of all of them — and the other
  vault's simply never went off.
- **The Find bar reported "NaN / 3".** The match counter was reading a value
  that did not exist, so the position never showed a number — for the whole
  life of the feature.
- **Cancelling "Attach file" leaked a little memory each time.** Dismissing the
  file chooser without picking anything left an invisible element behind;
  enough cancelled attempts in one session added up. It is now cleaned up
  whether you choose a file or not.
- **Leaving or switching a vault did not stop it looking for that vault's
  devices.** Hypha kept the network listener and the announcement running for
  the vault you had left, and kept the connection to the old vault's devices
  wired up behind the scenes — so a session that switched vaults a few times
  was still announcing every one of them.
- **On iPhone, connections that could never succeed were never given up.**
  Trying to reach a device that had left the Wi-Fi network left the attempt —
  and its open socket — in place for as long as the app ran, once per attempt.
- **On iPhone, an error at the wrong moment could stop syncing silently and
  permanently.** If the phone reported a failure whose text ran onto a second
  line, the message it sent back to the app was malformed and thrown away, so
  the operation that was waiting for it waited forever — with nothing shown and
  nothing logged. Those messages are now built safely, and any request that
  gets no answer within fifteen seconds fails with a real error instead of
  hanging.
- **On iPhone, the app announced itself to other phones only once, at
  startup.** It should announce itself every second, so that devices that
  arrive later — or after the Wi-Fi drops and comes back — can find it.
### Security
- **A device on the same network could make Hypha chase peers that were never
  there.** To be found by your other devices, Hypha announces itself on the
  local network in the clear — that announcement has to be readable before any
  keys are exchanged, so anything on the same network can send one too.
- **An iPhone could be killed by the system while catching up on a big sync.**
  Data arriving from another device was accepted as fast as the network
  delivered it, with no way to say "wait" — so a large catch-up landing while
  the phone was busy drawing the screen piled up in memory until iOS shut the
  app down.
- **A device on the same network could exhaust Hypha's resources.** Anything
  that could reach the app's sync port could open connections and simply never
  complete the introduction — each one holding a slot open indefinitely, with
  no limit on how many.
- **A large vault could not sync at all.** Above roughly thirty thousand notes,
  tags and notebooks, the batch of metadata one device sends another outgrew
  what a single message can carry — and instead of sending it in parts, Hypha
  reported a sync error and sent nothing.
- **Note history never saved a single version.** The history sidebar — the
  timeline, the per-version diff, the Restore button, on desktop and iOS alike
  — had nothing behind it: no version was ever written, for the whole life of
  the feature.
- **"Open externally" on an attachment did nothing on iPhone but show an
  error.** Opening a file Hypha cannot preview — a PDF, a spreadsheet, an
  archive — is handed to the operating system on the desktop, and on iOS there
  was nothing behind the button at all.
- **The spell-check settings on iPhone were controls that did nothing.**
  Language settings offered a spell-check switch, a status line and a language
  list, none of which iOS lets an app change — the switch flipped back, the
  status stayed "off" and the list was always empty.
- **Importing from Standard Notes produced nothing at all.** Settings → Import
  walked the export folder, matched up the media files, and then reported
  "Imported 0 notes" as a success, on desktop and iOS alike — the converter at
  the centre of it returned an empty document for every note, and an empty
  document is what the importer treats as "not a note" and skips.
- **Images could disappear from a note permanently.** An image's link to its
  stored file was dropped every time a note was loaded from HTML rather than
  from its live document — which is what happens to any imported note, and to a
  note that has not yet been opened on that device.
- **Reminders never actually fired — on any platform.** The function that
  computes a reminder's next fire time was a placeholder that always answered
  "never", and it is the only input to the schedule every platform arms from.
### Added
- **Photos from a phone can now be compressed when you attach them.** The
  Settings → Attachments compression preference already existed and nothing
  read it; it works now, and it understands the formats phones actually produce
  (HEIC and AVIF, alongside JPEG and PNG).
- **iOS: Backup & Export, Restore and Import.** These settings sections were
  hidden on iOS because the platform had no file picker behind them. iOS can
  now save a backup to Files, restore one, and import a Standard Notes export
  folder; a chosen backup folder is remembered across app launches, so
  scheduled backups work there too.
- **iOS: reminders that alert on the device.** Reminders were synced items
  only: one created on a phone could alert a paired desktop, but never the
  phone.
### Changed
- **"Monographs" is now "Web Notes".** The inherited name is gone from the
  whole tree — the sidebar entry, the `/web-notes` route, the command palette
  entries, the `WebNote` contract type, the `WebNotesFacade`, the
  `hypha://webNote/<id>` deep-link kind, and the `webNotes.*` translation keys.
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

- **Backup & restore (Phase 7) — the feature that looked finished and was
  not.** The Settings panel, the per-account scheduler, the deduplicated
  attachment pool, rotation and garbage collection had all been built against a
  data engine that returned nothing: **every backup Hypha wrote was empty**,
  and it reported success.
- Initial Hypha repository bootstrap (Phase 0): brand-clean desktop shell with
  a stubbed data engine, clean-room editor, own-model contracts, and AGPL-3.0
  licensing. Local-first CRDT + P2P architecture scaffolded for the upcoming
  phases.
- Direction record for first-run onboarding and the sync/account model: Hypha is
  local-first and peer-to-peer with no central auth server — one vault
  passphrase is the only credential, and further nodes are paired as peers via
  `hypha://invite` tokens. README carries the same direction statement.
- **iOS app (`apps/mobile`) — runs on real hardware.** A Swift WKWebView shell
  around the *desktop renderer*, reused through per-file Vite alias swaps
  rather than a second UI: the sql.js/sqlite-wasm engine replaces the Electron
  SQLite bridge, and a swipe stack of Sidebar / List / Editor replaces the
  fixed three-column shell.
- **Headless relay daemon (`apps/peer`) — Phase 6.** A **ciphertext-only**
  store-and-forward relay, not a full replica: it holds opaque encrypted
  envelopes and can never read a note. `hypha-peer` CLI (`init` / `join` /
  `run` / `status` / `prune`), a `FileSecretStore`, durable SQLite opaque
  stores, a `daemon`-role first contact, a `systemd` unit and a multi-stage
  Docker image.
- **Tombstone and projection GC (Phase 8, §4l).** CRDT tombstones, removed
  edges and deleted notes' bodies were retained forever on every client — only
  the daemon's stores were ever pruned.
- **Sync hardening (§4m).** HLC clock-skew convergence (a peer skewed +100s is
  absorbed via `observeRemote` instead of splitting the causal order); a
  cross-peer actor tiebreak so a tied `(wall, counter)` resolves to the same
  winner on both sides; and opt-in live-META push coalescing that collapses an
  N-write burst to at most two pushes without losing the final delta.
- **Vault passphrase rotation.** The passphrase now *wraps* the vault key
  instead of *being* it (key indirection), so it can be changed without
  re-encrypting the vault.
### Changed
- **The test suite is now typechecked.** Every other tree in the repo is; the
  tests were not, so a spec could call a method that no longer existed and only
  find out if that line happened to run.
- **The editor's extension list has one definition**,
  `createEditorExtensions()` in `@hypha/editor-vue`. It used to be an array
  literal inside the renderer's `Editor.vue`, which meant a test could only
  approximate the editor people actually type into — and an approximation
  cannot catch a configuration the app gets wrong.
- **Editor: Tiptap v2 → v3** (2.6.6 → 3.29.2). StarterKit's History extension
  was renamed `UndoRedo`, so the `history: false` disable became `undoRedo:
  false` (the rename was initially missed — see Fixed).
- **IPC: tRPC v10 → v11**. Upstream `electron-trpc` is tRPC-10-only and
  dormant, so both halves are vendored from scratch to speak tRPC 11 while
  keeping the upstream wire protocol (so the preload's `exposeElectronTRPC()`
  is unchanged): `src/renderer/src/platform/ipc-link.ts` (terminal link; v11
  empties the link runtime so the transformer is read per-link) and
  `src/shared/electron-trpc-handler.ts` (`createIPCHandler` via v11
  `callProcedure` / `getErrorShape` / `getTRPCErrorFromUnknown`, with full
  subscription lifecycle and per-`webContents` teardown).
- **Renderer sandbox: the preload is CommonJS (`out/preload/index.cjs`)**, not
  ESM. Electron loads a sandboxed preload as CJS only.
- **Sync is per vault.** `desktop.sync.*` procedures take an optional `ctx`;
  main keeps one coordinator session per vault context rather than one
  globally. See Fixed for what that repaired.
### Removed
- **A dead storage layer inherited from the fork.** `NNStorage` — an IndexedDB
  key-value store with its own password-crypto and PGP surface — was built on
  every launch, on desktop and iOS, and then dropped: the data engine never
  read the option it was passed in.
- **Everything else that was wired to nothing.** The same question asked of
  every remaining option the data engine is handed — "does anything ever read
  this?" — removed four more: a gzip compressor (built on every launch, on both
  platforms, with its own IPC channel to the main process), a server-events
  adapter and the dependency behind it (Hypha has no server), and two settings
  the engine ignored. None of it was reachable from the app; the one part that
  *was* reachable turned out to be the broken attachment backup under Fixed.
### Security
- **A second barrier around clipped web pages.** Clipping a page brings someone
  else's HTML into the app, and the app strips anything dangerous out of it
  before it is ever shown.
### Fixed
- **Opening a note re-downloaded the whole note, every time.** When Hypha asked
  another device (or your always-on relay) for a note's contents, it always
  asked for *everything* — even for a note it already had and had only come
  back to.
- **Two devices on the same network flooded it with discovery traffic.** Hypha
  announces itself on the local network once a second and answers announcements
  it hears, so that a device whose announcement can't reach you still gets
  found.
- **A deleted reminder kept firing on your other devices.** Deleting a reminder
  removed it here and told no one. Every other device kept the reminder and
  kept notifying you at its scheduled time, with no way to stop it from the
  device you deleted it on — and no later sync could fix it, because the
  deletion was never recorded as one.
- **Unpinning a shortcut only unpinned it here.** A shortcut removed from the
  sidebar on one device stayed in the sidebar on all the others, permanently.
- **An attachment whose file never arrived stayed broken forever.** Your
  devices send a note's *record* and its *file* separately, and the file was
  asked for only once, from a single device, at the moment the record arrived.
- **A "with attachments" backup never contained an attachment.** The engine
  writes the notes and names each attachment it references; copying the actual
  files is the app's job, and the app's half was a placeholder that reported
  "not stored on this device" for every one of them.
- **iOS: a joined vault's notes were invisible until you wrote a note
  yourself.** A merged peer batch reached SQLite and refreshed nothing — the
  notes list, the sidebar, the trash view, the open editor and the "last
  synced" stamp all reload off `syncItemMerged`/`syncCompleted`, and on mobile
  nothing published them.
- **iOS: no keyboard, in any field.** `Info.plist` specified a launch screen
  with an empty colour name, which is not a valid specification — so iOS ran
  the app in compatibility mode, and on iOS 27 an app in that mode is never
  given a keyboard session at all: tapping a field showed a caret and an
  accessory bar and no keys. (Native text fields in the same app were equally
  mute; Safari on the same device was fine. iOS 26 tolerated it.)
- **iOS: the app began below the notch, under a black bar.** The web view's
  scroll view was insetting the page by the safe area, which also zeroed the
  `env(safe-area-inset-*)` values the mobile shell pads itself with — so the
  padding written for the notch did nothing and the strip above the page showed
  the native view's background. The page now owns the whole screen and paints
  it, including the strips around the notch and the home indicator.
- **iOS: the app could freeze and go blank while a peer typed in the same
  note.** Persisting the database copies the entire thing out of the WASM heap
  and writes it to OPFS.
- **The restore file picker could not see backup files.** Both the save and the
  open dialog filtered for a file extension left over from the project this
  shell was forked from — one Hypha has never written.
- **Two undo systems ran in every editor.** Hypha's undo is y-prosemirror's
  collaborative `UndoManager`, which reverts only your own edits and leaves a
  peer's alone.
- **Closing the last window on macOS left the app running but inert.** The dock
  `activate` handler created a window and re-registered nothing, so sync could
  never start again (`getMainWindow()` stayed undefined), `hypha://` links went
  nowhere, cross-window refresh was dropped, and the tray's menu items pointed
  at a destroyed renderer. All window-bound wiring is now re-established on
  `activate`, and the registrations it calls were made genuinely idempotent —
  the tray in particular would otherwise have left one dead icon per
  dock-reopen.
- **A torn-off note window auto-locked on its own schedule and took the main
  window's database with it.** Note and pane windows armed the idle auto-lock
  timer despite a comment saying they did not; locking calls `db.close()`, and
  main shared one SQLite handle across every renderer, so the main window's
  next save failed with `Database not found for id: hypha-local` and every
  query after it failed until a manual reload. The handle is now ref-counted by
  the windows holding it (including a release when a window is destroyed
  without closing cleanly), and only the main shell window arms auto-lock.
- **A dead renderer hung the sync coordinator silently.** The main→renderer
  seam had no close handler and no per-call timeout, so when the seam-owning
  window went away every pending call stayed pending forever and the
  coordinator simply stopped. Pending calls now reject with a named
  `SyncSeamError` on close, and each call is bounded at 30 s for the other case
  — a renderer still alive but wedged, which emits no close event at all.
- **Auto-backup never tracked a fresh install's main-window size**, because
  only the session-restore path attached the bounds listeners.
- **Bulk wire length prefixes widened to u32 — a silent `u16` overflow
  corrupted every payload over 64 KiB. This changes the wire format; peers must
  share a build.** `lpBytes`, the length prefix on every bulk byte field
  (ciphertexts, attachment blobs, opaque carrier payloads), was `u16`, and the
  encoder *masked* rather than range-checked: a 70,000-byte META_STATE
  ciphertext wrote a length of `70000 & 0xffff` = 4464 and then appended all
  70,000 bytes.
- **An unauthenticated peer could reach handlers behind the HELLO gate.** Frame
  dispatch consulted "is this the first frame?" rather than an explicit
  `verified` flag, and `FrameReader` did not await its callback, so the decode
  loop did not serialize — `HELLO(bad credential) ‖ ATT_REQUEST` written as a
  single TCP write ran the `ATT_REQUEST` handler before the credential's
  *asynchronous* signature check failed. Dispatch now gates on `verified` and
  the reader awaits, so frames after a failed HELLO are never dispatched.
- **A malformed frame killed the process.** A decode error thrown inside a
  stream `data` listener had no catch; `FrameReader.push` now catches and drops
  the connection instead.
- **Wire-supplied attachment hashes are validated as `/^[0-9a-f]{64}$/`** at
  the sync-store boundary *and* again inside the blob storage layer, so a
  traversal path in an `ATT_REQUEST` or `ATTACHMENT` frame cannot escape
  `blobs/`. The daemon does not trust its caller either.
- **Five async seams that could interleave into corruption** (`applyMetaBatch`,
  the Yjs H8 path, `openDoc`, the dirty flag, the invite nonce) were closed;
  `Engine.transaction` now hands its callback an `EngineTransaction` so a
  transaction's repository is an argument rather than ambient state that a
  concurrent caller could swap underneath it.
- **A note opened before its peer was discovered stayed stale forever.**
  `openNoteForSync` pulled only from peers connected *at call time*, on every
  platform. Relatedly, `onLocalMetaChange` recorded a peer's frontier *before*
  sending, so a failed push over-claimed what that peer held for the life of
  the connection.
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
  rejects `btoa` output (the `=` padding / `+` / `/`) with "incomplete input",
  so every "Generate invite" threw and surfaced as red error text.
- **Devices: a fresh device no longer silently becomes its own "owner".** Boot
  sync (`P2PSyncer.start`) called `getRoomCredentials` unconditionally, which
  auto-generates `ownerKey:<ctx>` + `roomSecret:<ctx>` on first call — so as
  soon as the vault was unlocked on first run, every fresh device minted an
  owner key and flipped to the "owner" role, hiding the "Join a room" UI (the
  `devices` section's pending block is `v-if="isPending"`).
- **P2P editor sync: edits no longer stop broadcasting after switching away
  from a note and back.** The broadcast trigger (`YjsSyncStore.onUpdate`) bound
  a `doc.on("update")` listener to the `Y.Doc` *instance* captured at subscribe
  time, and the editor destroys + recreates that `Y.Doc` on note switch
  (`YjsStore.closeDoc` → the next `openDoc` mints a fresh doc with a new Yjs
  `clientID`).
- **Editor: switching to a note with no Yjs snapshot no longer leaves the
  previous note's body visible.** `bindYjsDoc` rendered the bound fragment into
  the editor only when it already had content (`fragment.length > 0`), skipping
  the render for an empty fragment — a workaround (`ae9558a`) for
  `_forceRerender`'s dispatch dropping the `ySyncPlugin`.
- **Sync: tag associations no longer ghost / duplicate across peers.**
  `meta_edges` rows are keyed by a deterministic PK that *encodes direction*
  (`${fromType}:${fromId}|${toType}:${toId}`), and the LWW upsert gate only
  dedups rows with the same PK.
- **Sync: a note synced to a peer is now searchable there without opening it.**
  The `text_index` (FTS5) and `vec_notes` (semantic) projections are
  Yjs-derived with no write trigger; the only indexer was the editor's
  `flushSave`, so a note that arrived via META sync was absent from the
  receiver's search index until the user opened + edited it there (and a
  tombstoned note wasn't removed from the receiver's index).
### Security

The renderer trust boundary, hardened. Every item here assumes the realistic
threat: content that arrives from a synced peer or an imported archive is not
content this device wrote.

- **"Open externally" no longer hands a peer-chosen filename straight to the
  OS.** `shell.openPath` dispatches on the extension and nothing else, and both
  callers pass a name from off-device — a synced attachment's filename, or a
  `file:` link stored in synced note content.
- **Release notes and changelogs are no longer rendered as raw HTML.** The
  markdown renderer preserved HTML by design, and both of its `v-html` sinks
  are fed from the network (the repository's `CHANGELOG.md` and the update
  feed's release notes).
- **Backups and imports are confined to a directory the user actually picked.**
  Both APIs enforced containment against a root the *renderer* supplied on
  every call, which is not containment at all.
- **The renderer runs in the OS sandbox** (`sandbox: true`) with Node
  integration off. The Node flag granted nothing in practice — with context
  isolation on, `require`/`process`/`Buffer` are already undefined in the
  renderer — but it was a latent escalation waiting for someone to relax
  context isolation.
- **Links in a note can no longer name any scheme they like.** The `link` mark
  overrode TipTap's render step without calling the original, which dropped its
  URI check — so a link mark arriving from a peer rendered as a live anchor for
  `javascript:`, `data:`, `file:` or anything else.
- **Internal `hypha://` links survive opening a note.** The protocol was never
  registered with the link mark, so every internal link was stripped the moment
  a note without a sync snapshot was opened — and because that stripped
  document is what gets saved and broadcast, the links were gone on every
  device, silently and permanently.
- **SQL that names a file is refused.** The database layer advertised that a
  compromised renderer could not point SQLite at an arbitrary path, but
  enforced that only on the `open` call — `ATTACH DATABASE '/anywhere'` and
  `VACUUM INTO '/anywhere'` walked straight past it.
### Tooling / Dependencies
- **CI: every GitHub Action is pinned to a full commit SHA**, with the version
  in a trailing comment. A `@v5` tag is a moving pointer its owner can repoint
  at any commit; these jobs hold a token and build the binaries users download.
- **Dropped `npm install -g npm@latest`** from the release and packaging jobs.
  Node 24's bundled npm already matches the lockfile generator, and installing
  an unpinned "latest" into the toolchain that produces shipped binaries
  defeats the SHA pins above.
- **The root `typecheck` covers every workspace.** It was a hand-maintained
  list of 10 `--workspace=` flags that omitted `apps/mobile` (the active
  workstream) and the three Vue packages; it is now `npm run typecheck
  --workspaces --if-present`, so a new package is gated the day it is created.
- **The UDP LAN-discovery spec no longer broadcasts on every test run.** It
  bound a fixed, topic-derived port and put real packets on whatever network
  the machine was attached to; it is now `p2p-udp-beacon-live.spec.ts`, gated
  behind `HYPHA_LAN_LIVE=1` like the other live specs. The topic → beacon-port
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
