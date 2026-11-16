# Changelog

All notable changes to hypha. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.99.44] - 2026-11-16

### Added

- Link suggestions: linking a project, contact or recipe in the text offers to set the matching property.
- Suggestions also come from names in the text, similar notes and contacts that recur with a project.
- Views can filter on "Linked with"; rollups can count or list any connected note.
- A project's linked notes show the line that links it; "+ New" there links through a property.
- "Unlinked mentions" have a "Link" button.
- Properties are vault-wide and can be added to any note; tables, filters, boards and calendars use them all.
- Settings → Note types → All properties: rename, delete, merge and reset properties. A merge cannot be undone.
- "Edit property" changes a property's kind; renaming a value or board column renames it on every note.
- "Convert to object…" for notebooks and tags, with Undo.
- Markdown export writes every property; import turns other frontmatter fields into properties.

### Changed

- Notes pointing to a note are listed by where they come from, not under the property name.
- Values left over after a type change show as properties; "Reset to default" keeps added properties.

### Fixed

- Markdown import no longer drops frontmatter values, aliases, nested tags, colours, notebook paths or daily notes.
- Search finds property values after unlock.
- Renaming a value also renames it in saved filters, rules and boards.
- iPhone and iPad: suggestions by meaning work, and "+ Add property" is easier to tap.
- An open task that links a day is no longer listed twice in the daily stream.

## [0.99.43] - 2026-11-11

### Added

- Settings → Calendars: Microsoft accounts (Outlook.com, Microsoft 365). Work accounts may need IT approval.

## [0.99.42] - 2026-11-10

### Fixed

- Resizing with Daily Notes in a pane is smooth also when days show the weather.

## [0.99.41] - 2026-11-10

### Fixed

- Resizing the window, a split or the sidebar is smooth again while a pane shows Daily Notes.

## [0.99.40] - 2026-11-10

### Added

- iPhone and iPad: recordings keep running in the background, with a Stop button on the Lock Screen and Dynamic Island.
- Archive whole notebooks, with or without their notes.
- Link properties open a picker that can create the linked note; projects list linked notes by type.
- Note lists show each note's type icon and notebook.
- Search results open in a new tab, window or split.
- Four high-contrast themes.

### Changed

- A copied new passphrase is hidden from clipboard managers and cleared after five minutes.
- Turning off "Unlock with keychain" and removing a publishing target ask first.
- Simpler setup; welcome notes in German when the app is.
- Consistent tooltips, focus rings, dialogs and menus; larger dates and tags in lists.
- British spelling throughout; consistent German wording.
- Themes renamed and recoloured; a theme loaded from a file stays unchanged.

### Fixed

- A recording running in the background for over an hour no longer comes back empty.
- A page shared from the phone into today's note is no longer lost if another device started that note.
- Dates, plurals and messages follow the app's language and format settings.
- Many smaller fixes to the phone layout, keyboard shortcuts, Escape and dialogs.

## [0.99.39] - 2026-11-05

### Added

- Calendars in daily notes: subscribe to a webcal, .ics or CalDAV calendar under Settings → Calendars.
- "Write a note" on an event makes a Meeting note.
- A calendar's address stays on the computer that fetches it; only the events sync. Only Owner devices manage calendars.
- Paste an image into the cover or background picker.
- "On this day" shows past years as cards at the top of today's note.

### Changed

- Settings are sorted into vault and device pages; no setting changes value.
- Settings → Sync is one page again, with one card for all relays.
- "Add a device…" opens the same invite everywhere; the invite's lifetime can be chosen.
- ⌘L on a task cycles through open, done and cancelled.
- iPhone and iPad: Settings controls are full-size tap targets.

### Fixed

- iPhone: back and the edge swipe reliably return to the previous screen.
- Android: Back closes the open sheet, menu or dialog first.
- Notes no longer jump while pictures and covers load.
- A list pasted as plain text keeps every item after an indented one.
- Sharing into a note shows progress and can continue in the background.
- The daily notes view no longer keeps the Mac busy.

## [0.99.38] - 2026-11-03

### Fixed

- The desktop app is about 150 MB smaller.
- Settings → Sync no longer misreports a relay serving the vault under a newer key.

## [0.99.37] - 2026-11-02

### Fixed

- Internet sync connects within seconds on slow networks, instead of up to ten minutes per vault.
- The app no longer crashes while quitting.

## [0.99.36] - 2026-11-02

### Fixed

- iPhone and iPad: internet sync works after switching vaults and recovers from failures on its own.
- A device refused once by a relay or computer is let back in without a restart.

## [0.99.35] - 2026-11-01

### Fixed

- Relay: a failed or interrupted vault join no longer stops it.
- Relay: in Docker it restarts after a crash, and a busy port no longer stops it.

## [0.99.34] - 2026-10-31

### Added

- Tab icons that become close buttons on hover.
- Unread comments are marked in the sidebar, folder view and notes list.
- Every sidebar entry can be reordered by dragging.
- Clip summaries: up to six main points in the page's own words; recipe clips keep ingredient groups.
- iPhone and iPad: recovering a damaged vault keeps the original until a backup, a week of sync, or a rejoin.

### Fixed

- Attachments over 16 MB reach a relay again. Update the relay too.
- A revoked relay deletes its copy of the vault and stays revoked.
- iPhone and iPad: after a damaged vault is recovered, a member device is never made its owner.
- Backups made after another device changed the passphrase can be restored on a new device again.
- Undo takes back a pasted or dropped picture again.
- Settings → Sync shows a relay as Connected only while it is.
- Smaller fixes to tags, the daily stream, narrow panes and the iPhone layout.

## [0.99.33] - 2026-10-30

### Fixed

- Removing a cover asks whether to delete an unused image; Attachments lists what uses each file.
- Every link to a note has its menu on right-click and opens a background tab on middle-click.
- iPhone and iPad: pasted formatted text keeps its characters exactly.

## [0.99.32] - 2026-10-30

### Added

- New note types Meeting and Contact; the command palette can create any type and change a note's type.
- A note lists the notes that point to it through a property.
- Title and date formats: a note-type placeholder and a choice of common date formats.
- Bookmark and notebook overviews list their highlighted passages.
- Generate a title with on-device Apple Intelligence.
- A timeline of each day's activity in daily notes.
- A locked vault will show what kind of item arrived, never from whom or what.
- Middle-click and right-click work on notes in every list.

### Changed

- The default title format is type, date and time; titles you wrote are never changed.
- One type pill per note, under the title.
- Desktop: compacting keeps a checked copy of the vault and restores it if the result fails.
- iPhone and iPad: "Reclaim storage" returns, swapping in a checked copy; needs twice the vault's size free.

### Fixed

- Mac: pasted formatted text keeps its characters exactly.
- Folding a checklist item hides its sub-items.
- Opening a comment lands on the commented passage.
- Numbered lists from 10 onwards stay on one line.

## [0.99.31] - 2026-10-28

### Added

- iPhone and iPad: a vault that will not open gets a recovery screen; rows on damaged pages are listed as lost.
- Sync through hypha's relay with an invite code: no account, up to five vaults, 50 MB of attachments.
- The relay only holds encrypted data; its key lives in the device's keychain.
- Every note shows its type; on-device AI can detect it and fill properties without touching your text.
- Desktop: arrange sidebar sections and rows by dragging.

### Changed

- Settings redesigned and regrouped, with search; old links still open the right page.
- iPhone and iPad: "Reclaim storage" is removed for now; compacting is not yet safe on a phone.
- The animated background is more visible and pauses on battery.

### Fixed

- The image and embed privacy settings apply in every window immediately.
- Clips of pages behind Cloudflare's browser check work where the site allows it.
- The interface language is one choice for the whole device.
- iPhone: a crash while the phone sat locked.

### Security

- The search engine's built-in Microsoft usage telemetry is now off. It was uploading since 0.99.25.
- Affected: iPhone, iPad, macOS and Linux; not Windows. It sent technical events, never note content.

## [0.99.30] - 2026-10-24

### Added

- Search finds other word forms and compound words; title matches rank higher.
- Related notes are grouped by topic.

### Fixed

- Searching for a word with punctuation, # or % finds the note.
- Trashed notes no longer appear in search results.
- Relay: a relay removed from a vault and invited again syncs again.
- Relay: `hypha-peer join` reports while it waits; `--timeout 10m` makes it give up.

## [0.99.29] - 2026-10-24

### Added

- A note's cover picture can be repositioned and opened full size.

### Fixed

- A vault left waiting by an older relay retries once the relay is updated; rows get "Try again now".
- Quitting the desktop app no longer flashes "Startup failed".

## [0.99.28] - 2026-10-24

### Fixed

- Relays on your network reach Connected reliably, including after "Connect all my vaults" and approval.
- A relay removed from a vault says so instead of waiting forever.
- "Connect all my vaults" works with more than five vaults; the relay must be updated.

## [0.99.27] - 2026-10-24

### Added

- Clip summaries by Apple Intelligence are headed "Excerpt", with a note that AI can make mistakes.
- iPhone and iPad: several shares are added in the background and listed when done.
- A relay on the local network asks the vault owner once whether to connect.
- Phone and iPad: properties are edited in a drawer.

### Fixed

- iPhone and iPad: sharing a web page from Safari works again.
- Phone: sharing many links no longer stalls, and nothing is added twice.
- Phone: link properties can be set again.

## [0.99.26] - 2026-10-23

### Added

- Settings → Appearance → "Text size in notes", from 13 to 24 px.
- Properties that link to other notes or to people; Projects gain Lead, People, Parent and Related.
- Rollups and formulas as properties.
- Note map: a Links view, and a Connections view in the sidebar.
- Phone and iPad: notebooks, tags and links are edited in a drawer.

### Changed

- Templates are their own kind of note under Settings → Templates; notes tagged "template" are converted.
- Each note type can name a template; Markdown export includes templates.
- A tap on a task checkbox ticks and unticks it; cancel from the Block sheet or right-click menu.
- Mac: every vault syncs in the background by default.
- Compact notices in today's note; a two-colour animated background.

### Fixed

- Phone: larger tap targets and swipes that follow your finger.
- Table formulas: IF skips the branch it does not take; new TODAY, DAYS, CONCAT, LEN and ISBLANK.
- Property changes from another device show in tables and filters right away.

## [0.99.25] - 2026-10-23

### Added

- Note types (Movie, Book, Recipe, Project and your own) with properties; web clips get type and details.
- Saved views on every list: Cards, List, Table, Board and Calendar.
- Bookmarks (formerly colours) also mark passages in notes and PDFs.
- Search finds pictures and PDFs by content; search by meaning needs no download and works on iPhone.
- Photos keep the date and place they were taken.
- Tasks: priorities with !, !! or !!!, and a cancelled state.
- Notices: reminders that stay on today's note until done.
- Notifications for chat, comments and mentions; on iPhone while closed, via a relay that forwards them.
- Summary of the day by Apple Intelligence, written on the device.
- iPhone quick capture from the Action button, Control Center, the Lock Screen or Siri.
- See who else is in a note.
- Mac: keep a vault syncing from the menu bar with no window open.
- Sync: add a relay by address; rotate the owner key after revoking a device.
- Relay: many vaults on one port, with storage quotas.
- Tables: sticky header, full width, and row and column handles.

### Changed

- Pasted Markdown arrives formatted.
- "Turn into" changes only the selected list items.

### Fixed

- Undo puts the cursor back where it was.
- Many smaller fixes to lists, tables, chat, comments, search and the iPhone app.

## [0.99.23] - 2026-10-13

### Changed

- "Format at the selection" is now called "Compact mode"; your choice is kept.

### Fixed

- Desktop: publishing works again and reports why it failed.

## [0.99.22] - 2026-10-09

### Added

- Desktop: "Format at the selection" shows a bar over selected text in place of the toolbar.
- The slash menu lists blocks first and opens after a space mid-line.
- Phone: an Insert sheet, and Find in note and cover options in the ⋯ menu.
- Code blocks: language, Wrap and Copy. Tables: add a row or column from the edges.
- Pictures: alignment and captions.
- Page style → Font: text size and line height.
- Smart punctuation, on by default on the desktop.
- Hovering a note link shows a preview.
- Headings can be folded.
- The daily stream takes a page style; each day can have a cover.

### Fixed

- Typing at the end of a link no longer extends it.
- ⌘. folds a list item without toggling superscript.
- Pasting a URL over a selected URL replaces it.

## [0.99.21] - 2026-10-09

### Fixed

- iPhone: sharing into an existing note no longer gets stuck in search.
- iPhone: the dock's calendar button has its glass again.

## [0.99.19] - 2026-10-08

### Added

- PDFs: highlights, reference chips and a viewer inside the note.
- Vaults can have an icon or emoji.
- Settings → Sync shows each person with their devices.
- Right-click Trash to empty it.
- iPhone: the iOS 26 Liquid Glass look.

### Changed

- Restoring a backup made by a newer version says so and suggests updating.

### Fixed

- iPhone: Back always returns to the previous screen, also from a PDF.
- iPhone: the screen no longer jumps when the keyboard opens.
- Chat restored from a backup is searchable right after unlocking.

## [0.99.18] - 2026-10-07

### Added

- People: devices in a vault are grouped into named people.
- Chat: one conversation per vault, with replies, reactions, attachments, mentions and disappearing messages.
- Chat notifications name the sender but never show the text.
- Link previews are fetched by the sender's device only; Settings → Privacy turns them off.
- Comments on selected text, with resolvable threads.
- Search finds chat messages and comments.

### Fixed

- Chat messages are always attributed to the device that signed them, also from iPhone.
- Show passphrase asks the device owner first; Copy is concealed and expires.
- Undo and Redo keep working when a note is open on several devices.
- Text recognition no longer reads a picture twice.
- Smaller fixes to panes, windows, lists and pasted text.

## [0.99.17] - 2026-10-07

### Added

- Live cursors show where other devices are typing.
- Text in pictures and recordings is read on the device and is searchable; nothing leaves the device.

### Changed

- First start leads straight into setup; hypha creates a six-word passphrase, shown once.
- With the key in the keychain, the passphrase can be shown again after Touch ID or Face ID.

### Fixed

- iPhone: a crash shortly after opening while syncing.

## [0.99.15] - 2026-10-05

### Added

- Whiteboard notes: a "Board text" sidebar with typed text and read handwriting.
- Generated pages: select notes like files; the middle button now opens a background tab.
- Daily Notes lists each day's reminders.

### Changed

- Phone and Android: back follows your screen history.
- A folder on a notebook's page opens in the same tab.

### Fixed

- Phone: a repeating reminder fires again after the first time in the background.
- Suggestions under "+ Notebook" and "+ Tag" can be clicked again.

## [0.99.13] - 2026-10-05

### Added

- Android: a first experimental APK to install by hand. Files, sharing, notifications and local sync are missing; sync is untested.
- iPad: the desktop layout with sidebar, list, editor, tabs and split panes.
- Whiteboards in notes and as notes, with copy, paste and zoom; edits from two devices merge.
- Whiteboard text is searchable, handwriting too on macOS 27 and iOS 27.
- Desktop: a "Folders" sidebar layout with notebook overview pages.
- Sixteen built-in page styles, plus textures, card styles, papers and five fonts.
- Keyboard and screen-reader navigation in the sidebar.
- A "New note" button in the sidebar.
- Type @remind in a note to set a reminder.
- Google Maps links can be embedded.

### Changed

- Dates go in with @ and "Pick a date…".

### Fixed

- Returning to a note's tab restores its scroll position at once.
- Duplicating a note copies its whiteboard drawings.

## [0.99.12] - 2026-10-03

### Added

- Page styles for notes, which can be saved and set as the default.
- An Unsorted list of notes with no notebook, tag or colour.

### Changed

- Dragging a sidebar's edge far enough hides it.
- Rearrange the toolbar by holding an icon.
- A note's notebooks and tags sit under its title.
- All Notes leaves out daily notes unless "Show daily notes" is on.

## [0.99.11] - 2026-10-02

### Changed

- One link picker for notes and web addresses.

### Fixed

- With two panes, paste, find and the toolbar act on the pane you are working in.

## [0.99.10] - 2026-10-02

### Changed

- Automatic backups can include attachments, stored once for all backups.
- Backups are kept by day, week and month; the old "keep last" number becomes the daily count.

### Fixed

- Leftovers of an interrupted backup are cleaned up after a day.

## [0.99.9] - 2026-10-01

### Added

- Phone: a Block button and Callout on the format bar.
- A "Dim unfocused panes" setting.

### Fixed

- Copying into plain-text apps keeps lists, checkboxes and tables.
- Sidebar counts stay correct; duplicating a note keeps its notebook, tags and colour.
- Phone: images and files can be selected and deleted.

## [0.99.8] - 2026-09-30

### Fixed

- "Edit link…" saves a changed web address.

## [0.99.7] - 2026-09-30

### Added

- Sidebar rows show note counts and an open-tasks mark.
- The daily notes stream lists the notes that link to each day.
- Desktop: reopening the app returns to the list you were in.

### Fixed

- Clicking a task in the daily stream opens its note at the task.
- Weather set to "This device" uses where each daily note is written.
- Layout fixes in the sidebar and Settings.

## [0.99.6] - 2026-09-28

### Changed

- Desktop: hiding sidebars that widened a narrow window restores its size.

## [0.99.5] - 2026-09-28

### Added

- Desktop: rearrange the toolbar by ⌘-dragging icons (Ctrl on Windows and Linux).
- Typing # offers notebooks and colours as well as tags.

### Fixed

- Sidebar folding and notebook order are kept per vault.
- YouTube videos play in the desktop app and on the phone.

## [0.99.4] - 2026-09-28

### Fixed

- Phone: the Due date button works again; Indent and Outdent are on the format bar.
- A note can be scrolled while its vault is syncing.
- Tab on the empty line below a list nests a new row.
- Phone: sheets and dialogs stay clear of the notch.

## [0.99.3] - 2026-09-26

### Fixed

- Changing or removing a sub-list item's list type no longer splits the list.
- Enter and ⌘L on nested tasks behave as expected.

## [0.99.2] - 2026-09-25

### Added

- Archived and trashed notes open in read-only tabs.

### Fixed

- Tabs keep their search, undo history and scroll position when switching screens.
- Clicking a task in the daily notes scrolls to it.

## [0.99.1] - 2026-09-25

### Added

- Enter in a note's title starts a new first line.
- Drop a block onto a list item to nest it.

### Changed

- Steadier block dragging.
- Desktop: notes lists show two lines of preview.

### Fixed

- A numbered item dragged into a task list no longer becomes a bullet.
- Tooltips stay on screen.

## [0.99.0] - 2026-09-24

### Added

- Editor animations; the system "Reduce motion" setting turns them off.
- Dragging a block while several are selected moves all of them.
- Screen readers name each task's checkbox.

### Fixed

- Text typed into an empty day of the daily stream is no longer lost when the day scrolls away.
- Desktop: a line typed right after reopening a note now reaches other devices.
- Syncing several large attachments no longer stalls.
- Renaming a notebook, tag or colour keeps its pin, description and creation date.
- Changing one vault's passphrase no longer locks your other vaults' windows.
- A refused phone no longer retries every second and drains the battery.
- In dialogs, Enter confirms only from a text field.

### Security

- Updated the editor library to fix two published vulnerabilities in how it handles note content.

## [0.98.9] - 2026-09-24

### Changed

- Mac: updates are installed by Sparkle and ask for an administrator password when needed.
- Mac: a copy that stayed on the old version after updating needs one fresh install from the DMG.

## [0.98.8] - 2026-09-24

### Fixed

- A device that joined on an owner invite stays connected after reconnecting.
- Mac: hypha explains when it cannot update itself instead of restarting into the old version.
- hypha writes a log file; diagnostic logging in Settings → Updates adds sync.

## [0.98.7] - 2026-09-23

### Changed

- "Add a device" asks whose device it is: Mine, Someone I trust, or a relay.
- New vaults start with three short notes and a "Getting started" card.
- The always-on device is called a Relay everywhere.
- Notification and location permission are asked only when needed.
- Moving notes to the trash or archive no longer asks; a toast offers Undo.
- Large images are compressed by default; "Keep originals" and a setting keep them.
- Device lists show device names.
- Mac: closing the window keeps syncing from the menu bar; Settings → Sync turns it off.
- After creating a vault, hypha shows the passphrase once, warns it cannot be reset, and offers backups.
- iPhone: scan an invite code when joining; optional Face ID unlock.
- Shorter editor toolbar and phone format bar.
- Shortcuts are now favourites; pinning is now "Keep at top".
- Settings, reminders and errors in plain words; a Help menu with shortcuts.

### Fixed

- iPhone: no longer crashes after a while with sync running.
- The language menu no longer offers a developer test language.

## [0.98.6] - 2026-09-23

### Changed

- Vaults with a passphrase open faster and are usable straight after unlocking.
- The notes list loads thumbnails and previews as you scroll.
- Typing in a note with a checklist no longer re-saves every task.
- A second window on the same vault no longer repeats the unlock work.
- The vault dock stays at the bottom of the sidebar; update and indexing status appear under it.
- The "Initialising database…" dialog no longer covers the window at startup.
- Semantic search is on by default; Search settings rebuild or clear the index for every vault.

### Fixed

- Semantic search finds unedited notes in vaults with a passphrase.

## [0.98.5] - 2026-09-22

### Fixed

- Standard Notes import keeps images in Super notes, including inside tables and lists.
- An indented list in an imported Super note no longer gets an extra empty bullet.
- Standard Notes import brings in every attachment; files no note uses are collected in one note.

## [0.98.4] - 2026-09-22

### Added

- iOS 17 or later: the Daily Note and New Note widgets can be pinned to one vault or ask each time.

### Fixed

- iPhone: clipping a page from Safari fills in the page's address.
- A new notebook appears straight away in the notebook picker of every open window.
- The list buttons in a just-created note leave the cursor inside the new list.
- Drag-selecting across list checkboxes or fold marks no longer stalls.

## [0.98.3] - 2026-09-21

### Added

- Each list remembers its own sort, grouping and filters, synced with the vault; ⋯ → Reset restores the default.
- Lists can be filtered to notes with tasks or open tasks; "Tasks first" lifts them to the top.
- A new sub-tag or sub-notebook starts with its parent's list settings.
- The Archive and the Trash have a ⋯ menu with their own sorting; the Trash sorts by deletion date.

### Changed

- The "also show files" switch is remembered per tag, notebook or colour list.

## [0.98.2] - 2026-09-21

### Changed

- Standard Notes import asks before writing; for a conflicted note you choose the version to keep, the others go to the trash.
- Standard Notes import checks the backup first and names any attachments it is missing.
- Standard Notes import no longer creates tags from #words in note text unless you opt in; existing tags still apply.
- The end of a Standard Notes import lists every skipped item with a reason; the list can be saved.

### Removed

- The Standard Notes decrypted-export import; the backup-folder import replaces it and brings across more.

## [0.98.0] - 2026-09-20

### Changed

- Desktop: each vault runs in its own background process; a crash in one vault no longer affects the others.
- Two windows on one note edit together live, and opening windows no longer restarts sync.
- Automatic backups also cover vaults with no window open.
- Switching vault reloads the window onto the chosen vault, on iPhone too.

### Fixed

- Creating or removing a vault updates the vault switcher in every open window.
- Opening a note in a locked vault says the vault is locked instead of reporting a database error.
- "Force unlock" can no longer clear a vault's journal files while another window opens it.
- After a crash, new edits are no longer ordered before edits made just before it.
- With two vaults open, device lists, sync and window actions no longer mix up the vaults.
- Picking another vault in Settings no longer disconnects the main window's devices.
- Closing the window that kept a vault in sync hands sync to that vault's other window.
- Reloading the first window no longer opens a different vault.
- Importing into a vault other than the one on screen works again.
- Remembered device lists are reset once; offline devices reappear when they next connect.

### Security

- Desktop: vault keys are held only by the vault's background process and never reach a window.

## [0.24.1] - 2026-09-17

### Added

- Relay: vaults can be added with `hypha-peer join` and removed with `hypha-peer leave` while the relay runs, without a restart.
- Relay: a relay started with no vaults waits for the first one to be joined.

### Changed

- The gradient background and following the system appearance are the defaults where you never chose otherwise.
- The animated background drifts slightly faster.
- Quick note preselects the vault you last worked in, also from the tray.
- In a narrow window the search dropdown uses the window's width.

### Fixed

- A quick note for a vault whose window is still starting is no longer lost.
- In a narrow window the block grip sits in the margin, not over the text.
- Drag-selecting no longer pauses when crossing the block grip.
- Sidebar vault tiles and the title-bar vault name have correct padding.
- Relay: a vault joined while the relay was running could be erased from its secret store on credential renewal.

## [0.24.0] - 2026-09-16

### Added

- Middle-click a note link to open it in a tab; Shift-click opens it in a new window.
- Click the vault name in the title bar to switch, open or add vaults.
- Windows can be resized down to 480×320.
- Narrow windows hide title-bar details, and the sidebar and notes list step aside automatically.
- Quick Capture is a glass popover near the top of the current screen.
- Quick Capture shows vault tiles and sends the text to the chosen vault.
- The Quick Capture shortcut (⇧⌘H, Ctrl+Shift+H) is shown in menus and can be changed in Settings → Notes.
- Links to other apps open those apps, after asking once per kind of link.
- A note link's edit option is "Change note…" and opens note search.
- Settings → Appearance → Background: a subtle gradient, optionally animated; animation respects reduced motion.
- iPhone: any notebook, tag or note can be pinned as a home-screen tile from its long-press menu.

### Changed

- Switching vaults is one click: the sidebar, the iPhone vault bar and Settings show a dock of vault tiles.
- Vault tiles start in alphabetical order and can be dragged into your own; the order syncs.
- iPhone: today's note has its own button in the floating dock.
- iPhone: swiping up on the vault bar grows it into the vault drawer.
- Sidebar sections remember whether they are folded, per vault and device.
- iPhone: sidebar sections look like the desktop's.
- A pane with exactly one tab hides its tab bar.
- Desktop sidebar vault tiles are painted softer.
- The tray icon is redrawn.

### Fixed

- A revoked device says so and stops syncing instead of looking healthy.
- Right-clicking a link no longer also opens the link popover.
- Drag-selecting past the edge of the note keeps selecting.
- With transparency on, light themes keep a hint of the theme colour.
- Arrow keys in the daily stream's pickers and the editor's menus no longer jump to another day.
- A task's row in the daily stream no longer repeats the date.
- iPhone: the sync, share and trash-preview sheets can be dragged down to dismiss.

## [0.23.3] - 2026-09-14

### Added

- The relay appears in the device list and can be revoked; existing relays get an "Add to devices" button in Settings → Sync.
- Tap a device's fingerprint to see and copy its full key.
- `hypha-peer vaults` prints each vault's device fingerprint.

### Changed

- Device fingerprints are written the same way in the app, the relay and the activity feed.
- `hypha-peer leave` accepts the vault as an argument or an unambiguous prefix.

### Fixed

- `hypha-peer leave` and `hypha-peer prune` refuse to run while the relay is running.

## [0.23.2] - 2026-09-14

### Changed

- The "Daemon" device role is renamed "Server"; relays already joined keep working.

### Fixed

- Splitting a previously resized pane no longer leaves a blank strip.
- A Server invite is refused by desktops and phones, and the relay accepts only Server invites.
- A relay joined with a Member invite never receives attachments: re-join it with a Server invite and revoke the old device.

## [0.23.1] - 2026-09-13

### Added

- hypha has a website, in English and German, with the downloads.

### Fixed

- A note no longer doubles on a phone that opened it before the relay answered.
- iPhone: note edits lost on a flaky connection are re-sent when it returns.
- An image added on another device no longer triggers a "delete these files?" prompt.

## [0.23.0] - 2026-09-12

### Changed

- Desktop: new look, with the notes list and editor in one rounded card.
- The active editor stands out from the list and from inactive split panes.
- The sidebar, notes list and tabs are denser.
- Sidebar sections are simpler and their contents align with other rows.
- The note open in the editor is outlined in the list.
- Menus, popovers, tooltips and dialogs share one appearance.

## [0.22.0] - 2026-09-11

### Added

- Reopening a note restores the cursor position.
- A day's tasks appear in the daily-note stream, including on days with no writing.
- Notebooks and tags can be moved by dragging, and notebooks from the context menu.
- The sidebar selects several notebooks, tags or colours to delete or move together.
- Table cells can hold formulas (SUM, AVERAGE, IF and more), including German number formats; exports contain the values.
- Typing a sum such as "3 + 3 =" fills in the result; Backspace undoes it.
- The command palette can insert a template into the current note.
- Vaults can have a colour and be renamed in Settings → Appearance; both sync.
- Every sidebar row and settings section has an icon, on desktop and iPhone.
- Escape closes the Settings and What's New windows.
- The vault selector has a settings button, and the iPhone vault bar a button for today's note.
- The @ and [[ note pickers search note content and show recent notes.
- Eleven more theme families, each with a light and a dark variant.

### Changed

- The menu-bar icon is the hypha hand alone.
- The open note in the list no longer has a border.
- Settings moved from the sidebar to the gear beside the vault name.
- Choosing a theme takes one click; themes you use are listed first.
- The title bar dims when its window is not focused.

### Fixed

- Deleting a notebook deletes its sub-notebooks, and restoring it brings them back.
- Sub-notebooks left at the top level by an earlier delete return under their parent.
- Deleting several sidebar rows deletes all of them, or names any that failed.
- @today, @tomorrow, @yesterday and @date work again in the note picker.
- The note picker, slash menu and tag menu follow the theme.
- An embedded web page no longer takes keyboard focus when its note opens.
- Opening and creating notes no longer slows down in large vaults.
- A task given a due date appears on that day in the daily stream immediately.
- Note titles and notebook rows align with the content around them.
- A text selection stays visible when switching tabs or panes.
- Search results no longer repeat a note's title as its snippet.
- Cmd/Ctrl+W closes the window when no tab is open.
- A pane scrolled to the top stays there when you return to its tab.
- Selecting near the bottom of a short pane no longer scrolls it away.

## [0.21.8] - 2026-09-09

### Changed

- A new window (Cmd/Ctrl+Shift+N) opens empty on the current vault.

### Fixed

- Quitting with several windows open restores all of them, with their tabs, panes and positions.

## [0.21.7] - 2026-09-09

### Added

- Any list row with nested rows can be folded (Cmd/Ctrl+.); folds sync.

### Changed

- Cmd/Ctrl+Alt+Up/Down moves all selected blocks.
- Any kind of list can be nested under any list row.
- Picking a list style changes only the selected rows.
- Cmd/Ctrl+L makes the current row a task.
- Lists are less indented and all kinds align.
- The drag handle sits in the left margin at every depth.
- Deleting a notebook, tag or colour asks whether to keep its notes or move them to the trash.
- The semantic search question is the last slide of the welcome wizard.

### Fixed

- Changing light or dark from Settings updates the main window correctly.
- A failure setting a window's theme no longer closes the app.
- Deleting a notebook or tag removes it from Shortcuts.
- The notebook delete confirmation describes what actually happens.

### Removed

- The Outline list; existing outline lists become numbered lists when their note is opened.

## [0.21.6] - 2026-09-08

### Changed

- Documentation corrected: auto-update and the Windows and Linux builds have worked since 0.20.2.

## [0.21.5] - 2026-09-07

### Changed

- A daily note's weather shows the whole day's forecast.

### Fixed

- Ticking a task completes its sub-tasks, in task counts and progress too.

## [0.21.4] - 2026-09-07

### Fixed

- A note no longer duplicates its body after another device opened it before it synced.
- After switching vaults, connected devices show as connected.

## [0.21.3] - 2026-09-06

### Changed

- iPhone: Daily Notes no longer keeps a list of days; going back returns to the home screen.

### Fixed

- iPhone: the app reopens on what you left open, including the daily stream.
- Backspace after an unwanted Enter returns to the end of the previous line.
- Text on dark highlights is light and readable.
- Chosen text colours adjust to stay readable in each theme.

## [0.21.2] - 2026-09-06

### Fixed

- A permanently deleted note stays deleted when another device sends a late update.
- A permanently deleted note can no longer be written back by an editor that still had it open.
- The activity feed shows notes permanently deleted on another device as deleted.
- iPhone: permanently deleting a note also removes its search data.

### Security

- The relay keeps encrypted copies of permanently deleted notes until its operator prunes them by age.

## [0.21.1] - 2026-09-06

### Changed

- Emptying the trash removes the notes on all your devices, not just this one.

### Fixed

- A deleted note can no longer come back as an "Untitled" copy.
- iPhone: trashing the open note returns to the list.
- Trashing an archived note updates every list and window.

## [0.21.0] - 2026-09-05

### Added

- Cmd/Ctrl+A selects a whole list; Backspace or Delete moves the selection to the trash.
- The desktop title bar shows the current vault.
- Drag any block by its grip to move it, including between lists.
- Cmd/Ctrl+Alt+Up/Down moves the current block.
- Embed a web page in a note from the toolbar, /embed or the command palette; also on iPhone.
- Settings → Global → Privacy → "Load embedded web pages in notes", off by default.
- Settings → Import reads Standard Notes encrypted backup folders.
- Cmd/Ctrl+L turns a line into a checklist item, or ticks it.
- Tables can be wider than the editor and scroll sideways.
- Relay: `hypha-peer leave <context>` removes a vault and its stored data; it does not revoke the relay's access.
- Web clips get a tag, set in Settings → Notes.
- Clicking a task row opens the note at that task.

### Changed

- One checkbox list instead of two; existing checklists convert when opened, without loss.
- Interface text no longer highlights when dragged across; note content still selects.
- Enter confirms dialogs, except for irreversible actions, where Cancel stays focused.
- The omnibar shrinks in narrow windows.
- Desktop Settings shows one vault at a time, with a vault picker.
- The desktop editor toolbar follows the iPhone's order and gains five tools.
- The note-link and web-link buttons have distinct icons.

### Fixed

- Highlighted text is readable in every theme.
- Embeds focus the address field, fill the note's width and have reachable resize corners.
- Embedded players such as YouTube, Vimeo and Spotify work, still isolated from the app.
- YouTube, Vimeo and Spotify page links play in the note; addresses they refuse to embed are declined.
- Undo covers creating a checklist.
- Clicking an image corner no longer marks the note as edited.
- Wide tables scroll instead of overflowing the page.
- Table controls are in the right-click menu again.
- Clicking beside the text no longer jumps the cursor to the end.
- The open note's footer updates when a notebook, tag or colour is assigned elsewhere.
- "Link to note" from the toolbar shows its popover and links selected text.
- "Synced N minutes ago" and the unsynced marker update when paired only with a relay.
- Settings → Encryption shows "Never" for auto-lock on a vault that never locks.

### Removed

- The toolbar's move up and move down buttons; use the drag grip or the keyboard shortcut.

## [0.20.2] - 2026-09-04

### Fixed

- The app can update itself again; "Restart to update" installs the new version.
- What's New checks for updates instead of always saying up to date.
- A failed update check says so instead of reporting "Up to date".
- The release notes window no longer jumps to the front during a download.

## [0.20.1] - 2026-09-03

### Added

- A "Lock vault now" command in the omnibar.

### Changed

- Auto-lock is off by default; when it fires, every window of the vault locks and decrypted notes are unloaded.
- iPhone: auto-lock counts time spent away from the app.
- A scanned page's recognised text appears under it and can be corrected.

### Fixed

- The auto-lock timeout in Settings → Encryption is respected, including Never.
- Settings no longer asks for the passphrase when Touch ID is on.

## [0.20.0] - 2026-09-02

### Added

- Home: today's note, due tasks, recent edits and "on this day"; windows with nothing restored open on Home unless set otherwise.
- Activity lists notes your other devices edited since you last looked.
- Print a note (Cmd/Ctrl+P) or export it as PDF, with images embedded.
- Find: Cmd/Ctrl+G and Cmd/Ctrl+Shift+G move between matches.
- iPhone: pin notebooks, tags, colours or notes as home-screen tiles and reorder them; pins and order sync.
- Due dates on tasks, as links to the daily note; today's note shows overdue tasks; also on iPhone.
- Mac: optional Touch ID before unlocking, under Settings → Encryption.
- iPhone: voice notes with on-device transcription; the audio is never sent anywhere.
- iPhone: scan documents; their text is searchable on every device.
- Tag suggestions from similar notes, computed on your device; can be turned off in Settings → Notes.
- Quick Capture (Ctrl/Cmd+Shift+H or the tray) adds text to today's note or a new note.
- Templates fill in placeholders for date, time, weekday and title.
- The notes list, Archive and Trash support keyboard navigation and selection.
- A web clipper bookmarklet in Settings → Notes.
- References show unlinked mentions of the open note.
- Callouts, including Obsidian callouts on import and in Markdown export.
- Pasted Markdown becomes formatting; the selection menu has "Copy as Markdown".
- Syntax highlighting in code blocks.
- Welcome slides on first start, explaining each permission before asking for it.
- Export a note or a whole vault as Markdown, with attachments.
- Import an Obsidian vault or a folder of Markdown notes.
- A new device can restore a backup before creating or joining a vault; the restored vault is a separate copy.

### Changed

- Backup settings are split into per-vault "Backup & export" and global "Backups".
- Home opens notes in an editor beside it.
- Home's reminder tile counts all active reminders.
- The notes list header is one row with a ⋯ menu; sort settings survive a restart.
- A pinned shortcut's menu matches the item it opens.
- Reminders open in a tab for editing.
- Manual notes-only backups go to the backup folder and count toward the keep limit.
- iPhone: the vault bar sits at the bottom of the home screen; its drawer adds and removes vaults.
- iPhone: tapping the sync dot opens the invite QR code.
- A task counts for a day only if it links to that day or lives in that day's note.
- Tooltips are the app's own, and buttons dim while pressed.

### Fixed

- Backup and restore act on the vault they are listed under; a restore could adopt another vault's identity.
- A backup schedule without a folder says it will not run.
- Dialogs: Escape closes one layer at a time, and focus starts on a button and stays inside.
- Tabs show the note's name on hover, switch immediately and scroll into view.
- Mac: the Dock icon and tray work again after using Quick Capture.
- Cmd+S no longer hides the sidebar; the sidebar and focus toggles moved to Cmd+Alt+S and Cmd+Alt+.
- Windows reopen on screen after a monitor is unplugged, and in full screen if closed that way.
- hypha:// links open the note, also when the window is closed.
- Find's regular-expression and case-sensitive options work.
- The slash, tag and note menus behave consistently.
- Outline lists keep their content, and copied tag chips paste as working tags.
- PDF export and Print work with large images.
- Search works again on vaults without a passphrase after the index upgrade.
- The first Quick Capture of a session is no longer lost.
- A task pasted within the same note no longer hides the tasks after it.
- A window left open past midnight moves to the new day.
- A search with no matches says so.
- Dark mode with transparency is easier to read; dark themes no longer show a large tiled logo.
- iPhone: fixes to gestures, landscape layout, popovers above the keyboard and screen-reader labels.
- iPhone: the format bar adds links, table rows and columns, and alignment; long-press opens right-click menus.
- iPhone: trashed notes can be read before restoring, and swiping a note asks before deleting.
- The German interface uses consistent terms.

### Removed

- The daily tag on daily notes; it is hidden on existing ones.

### Security

- After a crash, a vault's task due dates are wiped from disk at startup.
- Backup settings warn when a backup is not fully sealed; unlocking once with the passphrase fixes it.
- Backups saved through the save panel are readable only by your account.
- Removing a vault's key from the keychain disarms Touch ID; a passphrase change elsewhere removes the stored key.

## [0.19.0] - 2026-08-29

### Added

- Daily notes record the day's weather (sky, temperature, high and low, rain or snow) in the day header.
- Weather uses your coarse device location or a typed place, set under Settings → Notes; a switch turns it off.
- Only a coarse position is sent, to Open-Meteo; the note stores nothing but the weather.
- Each day in the daily stream has a ⋯ menu with the note actions; Mac: right-click the day header.
- "Add a vault" asks whether the new vault gets the example notes; joined vaults never do.

### Changed

- Breaking: profiles from 0.18 and earlier are not migrated. Export what you need first (Settings → Backup).
- To start fresh, delete the app's data (iOS: reinstall), create a vault on one device and join it from the others.
- Relay: remove its data directory and run `hypha-peer init` and `hypha-peer join` again.
- There is no special "local" vault any more; every vault is created, listed, switched and removed the same way.
- A first start creates a vault with its own identity, like "Add a vault".
- Reminder editor: Mode and Priority are icon toggles on one row, named for VoiceOver.

### Fixed

- Daily notes: the active day changes only on click, tap, arrow keys or picking a date, not on scroll.
- A trashed daily note leaves the daily stream at once; restoring it brings the day back.
- Daily notes: the day header no longer paints a solid band when transparency is on.
- Daily notes are titled with their day in tabs, the iPhone title bar and the omnibar.
- The preview line in the notes list survives a restart, in Archive too.
- Joining a vault can no longer overwrite a vault this device holds for a different owner.
- iPhone: pinned tiles and the activity feed appear at startup without waiting for a sync.
- iPhone: tapping a tag or notebook that is already open shows its list again.
- iPhone: going back from an attachment returns to where it was opened; files from a note open in place.
- iPhone: the home screen and the navigation bar are one colour.
- iPhone: the reminder editor keeps its form on screen when the keyboard appears.
- iPhone: picture resize handles are larger, and dragging them no longer scrolls or swipes back.

### Removed

- Relay: `hypha-peer migrate` and the pre-multi-vault layout it converted.

## [0.18.0] - 2026-08-29

### Added

- Settings → Sync: "Over cellular, send attachments only to the relay" (on by default, shown on iPhone).

### Fixed

- iPhone: a file added over cellular is uploaded once, to the relay, instead of three times.
- Relay: an attachment requested while still arriving is delivered as soon as it lands.
- Removing a device disconnects it at once on every device that learns of the removal.
- A large attachment one device cannot send is fetched from another device that can.
- Desktop: with two vaults open, each window lists only its own devices and sync errors.
- Relay: joining a second owner's vault no longer replaces another vault's keys.
- An attachment held by two devices is fetched from one at a time, no longer corrupting the file.
- A newly admitted device syncs with the relay and other members without a restart.
- Notes no longer skip the relay when written while it was reachable only through another device; some older notes still may.
- Desktop: Settings → Attachments updates when a file is removed from a note or the trash is emptied.
- Desktop: removing a file no other note uses asks whether to delete it; other devices no longer ask too.
- Daily notes: the day header uses the pane's frosted surface instead of a solid slab.
- iPhone: a file opened from a note no longer hides its controls under the top bar; swiping back returns to the note.

## [0.17.1] - 2026-08-28

### Added

- Relay: the always-on peer keeps attachments too, so other devices can fetch them while the sender is off.
- Interrupted attachment transfers resume where they stopped; both devices need this version.
- Settings → Storage shows reclaimable space and compacts the vault; no notes, edits or history are deleted.
- Relay: `hypha-peer prune --vacuum` returns pruned space to the disk; run it with the daemon stopped.

### Changed

- The release notes for 0.1.0–0.13.0 are shorter; no version or warning was removed.

### Fixed

- Relay: a file it could not keep is offered again later, and a file it has is not resent.
- Relay: `hypha-peer join` is faster; the passphrase key is derived once per start.
- Relay: space left by interrupted transfers is reclaimed; they could block all further attachments.
- Relay: the container image runs on x86 (amd64) servers as well as arm64.
- Relay: `hypha-peer prune` reports disk and database space separately instead of overstating what it freed.
- A note marks files it references that were deleted; one still in the Trash can be restored from the note.
- iPhone: trashed files appear in Trash and can be restored or deleted.
- iPhone: a failure to delete a file's data is reported instead of silent.

## [0.17.0] - 2026-08-27

### Added

- iPhone: light, dark and tinted app icons.
- Settings → Notes → "Opens on": the home screen or a specific note, chosen by search.

### Changed

- iPhone: the widgets use hypha's own calendar and note glyphs, larger.
- iPhone: the home screen leads with a two-column grid of tiles with live counts.
- A new vault opens on the home screen.
- Releases carry macOS and iOS only; there is still no Windows or Linux download.

## [0.16.0] - 2026-08-26

### Added

- Relay: one `hypha-peer` data directory can serve several vaults, each with its own identity and storage.
- A dot on a notebook or tag row, and in Shortcuts, marks an unticked task inside it.
- The sidebar remembers which notebooks and tags are expanded.
- Daily Notes opens ready to write: Mac places the cursor in today; iPhone keeps the keyboard down until you tap.

### Changed

- Relay: storage moves to one folder per vault on first start; back up the data directory first, there is no way back.
- Relay: the published compose file pulls the latest image; images carry their version as a label.
- Editor toolbar: text colour is a brush, highlight a marker; iPhone gets both, with swatches.
- iPhone: the daily stream has narrower margins.
- Sidebar: favourite stars show on hover only; on iPhone they are gone from rows.
- iPhone reconnects faster after unlocking by dialling known devices directly.
- Devices on the same network no longer keep redialling each other over the internet.

### Fixed

- Relay: no passphrase prompt when no store exists, a clear failure when it cannot read one, and shared vaults are relayed.
- Daily Notes opens on the requested day, or today from the sidebar, and holds its position while loading.
- Daily notes: clicking an empty or loading day places the cursor; tapping or scrolling no longer jumps between days.
- Note links in encrypted vaults show their titles instead of "Untitled".
- Sub-notebooks are reachable again; those in a trashed notebook move to the top level until it is restored.
- A link to a trashed note is marked; deleting a note for good removes the links to it.
- Importing from Standard Notes creates notes again.
- Mac: vaults open again; the 0.15.0 build failed to open them.

### Security

- Sync validates incoming data, holds a device whose clock is over an hour ahead, and deletes attachments only once synced.
- Device credentials expire after 30 days and renew automatically; a used invite cannot be revived by sync.
- A locked vault leaves no readable copy: search indexes are emptied at startup and lock, nothing is saved unencrypted.
- Notes in the trash when a passphrase is first set are now encrypted; unencrypted vault files are refused.
- LAN discovery no longer reveals the vault's sync topic; an invite is handed only to the owner's device.
- Devices on this and older versions cannot find each other over the LAN until both update.
- Images on other servers load only if Settings → Global → Privacy → "Load external images in notes" is on.
- Embedded web pages cannot open windows or request permissions; network-share links are refused; local file links ask first.
- Shipped desktop builds drop developer tools, cannot be run as a Node runtime and verify their bundle at start.
- Windows: uninstalling keeps your vault on disk.
- iOS: diagnostic output reaches the system log only while Logging is on.
- Files beside the vault, backups and exports are readable only by your account.
- Protected published pages hide the note title until unlocked; What's New no longer sends a GitHub token from the environment.
- An internal security audit is published; the security page lists its findings and open items.

## [0.15.0] - 2026-08-25

### Changed

- Semantic Vector Search is one app-wide setting in Settings → Global → Search; index rebuilds stay per vault.

### Fixed

- A tab dragged onto another vault's window is refused instead of vanishing.
- Closed windows stay closed when a vault reopens.
- Restarting reopens only the vaults that were open.
- Edits and new notes in one window appear in other windows on the same vault.

## [0.14.1] - 2026-08-25

### Added

- iPhone: sharing into hypha asks which vault when there are several.
- iPhone: a notification when a share needs you to pick an existing note.
- A shared link is clipped as an article wherever it goes.
- A single-note window can show the daily stream.

### Changed

- Scrolling the daily stream puts the cursor in the day you land on.
- iPhone: the share sheet shows the item, the vault and three destinations, in English and German.
- A waiting share can be discarded from the in-app sheet.

### Fixed

- Cmd+D no longer leaves the daily tab flipping between two dates.
- Dragging a note window's last tab to the main window no longer closes the main window.
- Today's date is never dimmed and stays today after midnight; "Go to today" works after midnight.
- A joined vault shows its real name after the first sync.
- The daily tab can be dragged into its own or another window.
- Closing the daily tab clears the stream from the pane.
- Dragging a note out of its window can no longer lose it.

## [0.14.0] - 2026-08-25

### Added

- iPhone: share into hypha from any app; links become clipped notes, other items go to a chosen note.
- iPhone: Lock Screen and Home Screen widgets for today's daily note and a new note.
- Settings → Notes: choose what each vault opens on; the choice syncs.
- iPhone: Settings → Open on Launch pins which vault opens at start; it stays on this phone.

### Changed

- Daily stream date headings are dimmed except the day you are reading.
- Search across all notes is ⇧⌘F (Ctrl+Shift+F on Windows and Linux), was ⌥⌘F.
- ⌥⌘F opens find and replace in the current note.

### Fixed

- iPhone: long-pressing + opens its menu on every screen.
- The daily stream no longer jumps when scrolling into older days.
- iPhone: a long press in the notes list no longer selects text.
- Going back from a linked note returns to the note you came from.
- Tapping a date in Daily Notes opens that day at the top of the screen.
- The day's date no longer flickers between sizes while scrolling.
- Windows, Linux: the window buttons follow the theme.

## [0.13.3] - 2026-08-24

### Changed

- iPhone: the top bar is solid and includes the notch strip; back is a plain chevron; titles sit left.
- iPhone: Collections leads with the app logo; swipe across to reach your notes.
- Daily notes: dates shrink and hold at the top; unwritten days take one line.
- Daily notes: a day's notebooks, tags, links and files are one row; tap it for the full set.
- iPhone: the daily notes editor runs full width.
- Desktop: daily notes is one tab named for the view, including for unwritten days.
- Desktop: days in the daily stream line up with the note column.

### Fixed

- iPhone: the Join button was behind the keyboard when unlocking or joining a vault.
- The formatting toolbar appears in daily notes.
- Windows of vaults with clashing light and dark themes use solid backgrounds; Settings → Appearance says so.
- Pin, star and shortcut icons use the right shade when vault themes differ.

## [0.13.1] - 2026-08-24

### Added

- Daily notes are one continuous page; scroll between days, and arrow keys cross from day to day.
- The always-on relay ships as a container image with a compose file and example configuration.
- The relay holds ciphertext only and cannot read your notes; it is optional and not a backup.

### Changed

- iPhone: the top bar floats over content and frosts; large titles scroll with the page.
- iPhone: a floating + button on every screen creates what fits the screen; hold it for more.
- iPhone: search has its own bottom-left button and opens as a drawer above the keyboard.
- iPhone: swipe navigation starts only at the screen edges.
- iPhone: iOS-style motion, corners and type; Reduce Transparency and Reduce Motion are honoured.
- The releases page no longer offers an iOS download; iPhone installs come through TestFlight.

### Fixed

- iPhone: content reaches the bottom of the screen, and every surface uses one background colour.
- Desktop: the 0.13.0 app no longer fails to start with an error box.

## [0.13.0] - 2026-08-21

### Added

- First installable build: a notarized macOS .dmg with auto-update, and iPhone through TestFlight.
- Typing `@` or `[[` with an unmatched title offers to create that note.
- Tags can have icons: right-click a tag → "Set icon…".
- Colours can be changed: right-click a colour → "Change color…".
- Archive and Trash support shift-click and cmd-click selection.
- Removing a file from a note asks whether to delete it when no other note uses it.
- iPhone: a setting for downloading attachments over cellular, on by default.
- iPhone: full-text search from any screen, via the title bar.
- An insertion line shows where a drag will land in a note.
- Double-click a picture to preview it in a pane beside the note.
- Drag a picture's corners to resize it.

### Changed

- Read the Known limitations page before storing anything you cannot lose, and keep your own backups.
- Not yet tried by anyone: sync between two desktops over the internet, and auto-update between installed versions.
- Settings reports results in a dialog instead of a line at the foot of the section.
- Pictures in list rows sit on the right, beside the title and preview.
- Archive and Trash open a note beside the list.
- The per-list search boxes are gone; the title-bar search covers note text.
- iPhone: split-pane and window commands are hidden.
- Placeholder text is readable on all built-in themes.
- Note map: options are a side panel with explanations, kept per vault on this device.
- Note map: the default grouping distance is looser; opening a note from the map shows its local map.

### Fixed

- The "Checklist" list type no longer loses its text; checklists show text beside the checkbox.
- A note trashed or archived on another device no longer turns your typing into duplicate "Untitled" notes.
- A note trashed on another device leaves All Notes; Settings, Trash and Archive update for remote changes.
- One day could get two daily notes again; fixed.
- Opening a note no longer counts as editing it; an edited note stays at the top of a Modified sort.
- Sidebar shortcut order and settings changes sync to other devices promptly.
- A refused device (used or expired invite, or revoked) says so instead of appearing to sync.
- Editor: pasting `@`, links in code, Tab, runs of spaces, moving pictures and editing link text behave correctly.
- Closing a tab returns to the tab you came from; a selected image shows a ring.
- Renaming a colour no longer removes it, and its rename box accepts more than one character.
- The note map draws the same layout on every open.
- Settings layout fixes; deleting an attachment asks in hypha's own dialog; Mac window buttons line up.
- iPhone: reconnects over cellular after leaving Wi-Fi, and no longer quits while the phone is locked.
- iPhone: typing no longer scrolls the whole app; dialogs no longer open behind the keyboard.
- iPhone: sidebar long-press menus open, Daily Notes opens today, and search results open at the match.
- iPhone: "Back up now" works more than once.

### Security

- There is no recovery for a forgotten passphrase.
- A backup file still carries the vault credential.
- The cryptography has not been independently audited.
- Backups now encrypt tag, notebook and reminder names.

## [0.12.0] - 2026-08-19

### Added

- Mac: builds are signed and notarized, so no right-click → Open, stable permissions and working auto-update.
- An install guide, a security page, a known-limitations page, a privacy policy and a third-party licence list.
- `@today`, `@tomorrow` and `@yesterday` link to the matching daily note, creating it if needed.
- Archive, Trash and Web Notes use the notes-list rows, and their rows open.

### Changed

- Licence: hypha is no longer open source. It is source available under the Hypha Source Available License 1.0.
- Versions 0.1.0–0.11.0 were released under AGPL-3.0-or-later; those grants stand.
- The name is written "hypha"; the App Store listing is "hypha notes".
- iPhone: the app has a new identifier; it installs as a new app and must re-join your other devices.
- Desktop: new app identifier; notes are untouched, but macOS asks for Local Network permission again.
- Automatic backups are desktop-only; on iPhone, back up manually.
- A new app icon on both platforms.
- Mac: macOS 12 (Monterey) is the minimum.
- "Full offline mode", which did nothing, is replaced by a working "Download attachments automatically".

### Fixed

- A note could permanently contain its text twice on every device.
- One day could get two daily notes.
- Sync between paired devices no longer stops until the refused device is restarted.
- Archived notes are read-only, with an Unarchive button, and appear in Archive at once.
- iPhone: the keyboard no longer covers the bottom of the note.
- The `/` menu shows icons instead of icon names.
- Settings → Sync puts "Enable sync" at the top.
- Packaged builds respect the Logging switch in Settings → Updates.
- What's New shows the current release notes.

### Removed

- The "check for new versions" setting, which never did anything; updating works as before.

### Security

- Only notes are encrypted: tag and notebook names, reminder text and attachment filenames are stored in the clear, backups included.

## [0.11.0] - 2026-08-18

### Fixed

- Sync no longer stops after a phone leaves the shared Wi-Fi until the desktop app is restarted.
- Devices now detect and drop a connection to a peer that has gone away.
- iPhone: switching from Wi-Fi to cellular rebuilds the internet sync connection.
- Internet sync resumes after the network changes, instead of staying paused from an earlier local connection.
- iPhone: the log in release builds reports why sync is not connecting.
- A connection reset during an incoming internet connection no longer crashes the desktop app.

## [0.10.1] - 2026-08-18

### Added

- App icon on desktop and iPhone.

### Changed

- The passphrase fields on the first-run screen have visible labels that screen readers announce.
- "What's New" and the update check fetch release notes from a public location.

### Fixed

- An attachment that finished transferring to a phone is no longer reported as missing.
- iPhone: tapping an attachment chip in a note opens the attachment.

### Security

- iPhone: a web page embedded in a note can no longer reach into the app.
- iPhone: search terms, open attachment names and file fingerprints are no longer stored unencrypted with the open tabs.
- iPhone: the app's own screen can no longer be replaced by another web page.
- iPhone: reminder titles are no longer exposed in the system notification store months ahead.
- Joining a vault no longer leaves an empty hidden vault behind.
- A mistyped passphrase no longer leaves the app pointing at a vault you never opened.

## [0.10.0] - 2026-08-18

### Fixed

- iPhone: reminder titles, search terms and attachment names are no longer written to the system log.

### Security

- iPhone: the database is now encrypted; notes were previously readable in the app's files without a key.
- iPhone: vault keys, device identity, sync secret and stored invites now live in the iOS Keychain instead of plain storage.
- iPhone: this is not an automatic upgrade. Remove each existing vault on the phone and re-join it from your computer.
- Correction: backups were never fully encrypted. Note contents are; tags, notebook names, reminders, settings and attachment names are not.
- iPhone: inserting a photo no longer leaves an unencrypted full-size original, with GPS and camera data, in the app's files.
- iPhone: decrypted copies made for "Open in", export and backup are now protected and cleaned up.
- iPhone: the app-switcher snapshot no longer shows the note you had open.
- Desktop: search terms and open attachment names are no longer stored in plain text with the open tabs.
- Desktop: files opened in another app are no longer readable by other users of the computer.
- Desktop: the attachment folder and the list of vault names are no longer readable by other accounts.
- Stored attachment file names no longer reveal which file they contain.
- Desktop: vault keys are no longer written unencrypted, and a crash during a write can no longer destroy them.

## [0.9.0] - 2026-08-17

### Added

- iPhone: scan an invite QR code with the Camera to join a vault.
- The trash lists deleted attachments, which can be restored or deleted for good.
- Clicking an item in the trash opens a read-only preview.
- Deleting an attachment can be undone from the trash.

### Changed

- Settings: "Devices" and "Sync" are merged into one section.
- iPhone: the vault switcher is no longer shown as a settings section.
- iPhone: tapping the sync dot opens adding a device directly.
- Search by meaning rebuilds its index when the model or its settings change.

### Fixed

- Settings no longer shows one vault's sync and devices under another vault's heading.
- The sidebar no longer shows the previous vault's sync status after switching.
- Accepting an invite no longer ends on a blank screen.
- "Remove orphaned" no longer deletes attachments still used by an open note or a note in the trash.
- Trashed notes show their real titles.
- The Peers popover in the sidebar is readable.
- Translucent panels show their frosted-glass effect again.
- The invite QR code and link now always match the selected role.
- Light themes: markers, icons, reminder chips, error messages and "delete permanently" buttons are now visible.
- Search by meaning finds notes synced from other devices or restored from history.
- "Rebuild search index" no longer leaves search by meaning empty.
- Notes are no longer processed by the language model twice, or when the feature is off.
- A file too big for a device is no longer offered to it repeatedly.
- Sync failures now show "Sync error" in the sync indicator.

## [0.8.1] - 2026-08-16

### Changed

- iPhone: version history opens as a sheet over the note, with larger touch targets.

### Fixed

- iPhone: the app no longer stops finding other devices permanently.

## [0.8.0] - 2026-08-16

### Added

- Attachments can be tagged, filed in notebooks and given a colour.
- iPhone: "Colorize blocks" can be turned on for a single note.

### Changed

- iPhone: requires iOS 16.4 or later; every device that runs iOS 16.0 can update.
- The editor no longer shows a "Saved"/"Saving…" indicator.
- iPhone: the vault is written to disk as you work instead of copied whole on a timer.

### Fixed

- iPhone: a just-written note, or a just-created vault, is no longer lost if the app is killed.
- iPhone: the bar above the keyboard no longer slips behind the keyboard.
- A failed save no longer stops a note from receiving edits from other devices.
- iPhone: development builds launched from the home screen no longer show a blank screen.

## [0.7.1] - 2026-08-16

### Changed

- iPhone: less drawing and fewer wakeups while idle.

### Fixed

- iPhone: a failure to start local discovery is now reported instead of hidden.

## [0.7.0] - 2026-08-16

### Fixed

- iPhone: the app no longer heats up the phone; device discovery was busy-looping.
- Correction: the 0.6.0 note wrongly named its changes as the heat fix.

## [0.6.0] - 2026-08-16

### Added

- Indent and outdent buttons in the editor toolbar.

### Changed

- iPhone: pinching no longer zooms the whole app.

### Fixed

- iPhone: much less work while typing; the vault is saved after a pause, not on every change.
- Correction (see 0.7.0): this was first published as the fix for the phone getting hot; it was not.
- Bulleted lists show their bullets again.
- iPhone: the Collections screen layout is fixed.

## [0.5.3] - 2026-08-15

### Changed

- iPhone: a status dot in the top bar of every screen shows sync state.
- iPhone: on cellular, sync stays off the internet in Low Data Mode and Low Power Mode.
- iPhone: the app recovers when iOS discards its page in the background.

### Fixed

- iPhone: no longer gets hot retrying the internet when out of coverage.
- Devices on the same Wi-Fi stop also connecting over the internet.

## [0.5.2] - 2026-08-15

### Fixed

- Desktop: sync works again; it had failed on every vault since 0.3.0.

## [0.5.1] - 2026-08-15

### Changed

- Settings → Search names the current search model and its size (about 94 MB).

### Fixed

- iPhone: semantic search no longer downloads a model and re-indexes the whole vault on every launch.

## [0.5.0] - 2026-08-15

### Changed

- "Open externally" and backups no longer load whole attachments into memory.
- Quitting during a save no longer leaves a half-written file; staged files are cleared after an hour.

### Fixed

- Downloading an attachment larger than about 32 MB works again.

## [0.4.0] - 2026-08-14

### Added

- iPhone: add audio and video to a note.
- iPhone: photos showing a grey placeholder can be given a picture.

### Changed

- Downloading an attachment no longer loads it into memory first.

### Fixed

- A just-added attachment can no longer be deleted by "Remove orphaned".

## [0.3.0] - 2026-08-14

### Added

- iPhone: sync over the internet, not only on the same Wi-Fi.
- Large photos, videos and files now sync to other devices.
- iPhone: swipe in from the right edge to return to the note.
- Attachments are refused when the device lacks storage space.

### Fixed

- Devices can find each other over the internet, not only on the same Wi-Fi.
- A file too big for the iPhone is no longer sent to it anyway.
- Sync resumes promptly after the iPhone wakes.
- Relay: attachments go only to devices that asked for them, and a device can decline one.
- Opening a very large attachment no longer quits the app.
- Photos kept in their original format have thumbnails on other devices.
- Quitting the desktop app now saves a final version to note history.
- Edits in a note opened in its own window now sync.
- Version history shows the selected version instead of "…".
- One note without a title no longer breaks daily notes.
- iPhone: six blank toolbar buttons show their icons.
- Relay: the install instructions work, and `hypha-peer --help` exists.

## [0.2.3] - 2026-08-12

### Added

- Camera raws and iPhone photos get a viewable copy; you choose whether to keep the originals.
- A photo or video too big to send now says so instead of showing a blank box.

### Changed

- iPhone: the keyboard's ↑ ↓ ✓ bar is removed; use the formatting bar's chevron to hide the keyboard.

### Fixed

- Edits made on the iPhone reach other devices reliably.
- Sync resumes after the phone has been locked for a while.
- iPhone: adding camera raws, very large photos or several photos at once no longer quits the app.
- Images in a note no longer leak memory each time it is opened.
- iPhone photos kept as originals display on the desktop and in the note list.

## [0.2.2] - 2026-08-11

### Fixed

- iPhone: taking a photo into a note no longer crashes the app.
- iPhone: the keyboard no longer covers controls or the formatting bar.
- iPhone: tapping the note or pinned notebook you just left now opens it.
- iPhone: returning to the app no longer flashes white.
- iPhone: the suggestions bar's buttons are large enough to tap.

## [0.2.1] - 2026-08-11

### Fixed

- iPhone: a joined vault now reconnects after the app restarts.
- If you hit this, the invite is used up: remove the vault on the phone and re-join from a fresh invite.
- The note open at startup now syncs your edits.
- A note open on two devices shows the other device's changes after you stop typing.

## [0.2.0] - 2026-08-11

### Added

- Photos can be compressed on attach, including HEIC and AVIF.
- iOS: Backup & Export, Restore and Import, with scheduled backups.
- iOS: reminders alert on the device.

### Changed

- "Monographs" is renamed "Web Notes".

### Fixed

- Adding the same file on two devices before syncing no longer leaves a copy unreadable.
- Existing attachments are migrated to new names in the background; nothing is deleted before its replacement is verified.
- A note that cannot be decrypted is no longer shown as an ordinary untitled note.
- A single bad message can no longer make an attachment permanently unreadable.
- With two vaults open, both vaults' reminders fire.
- The Find bar shows the match position instead of "NaN".
- Cancelling "Attach file" no longer leaks memory.
- Leaving or switching a vault stops its discovery and connections.
- iPhone: a paired phone no longer stops syncing when another device is found.
- iPhone: failed connections are released, errors no longer stall sync silently, and the phone announces itself continuously.
- A large vault (above about 30,000 items) syncs instead of failing.
- Note history saves versions; previously none were ever written.
- Reminders fire; previously they never did, on any platform.
- Images no longer disappear from imported or unopened notes.
- Standard Notes import imports notes instead of reporting zero.
- iPhone: "Open externally" opens attachments.
- iPhone: non-functional spell-check settings are removed.
- iPhone: a large sync catch-up no longer gets the app killed.

### Security

- A device on the local network can no longer send fake announcements that make the app chase peers.
- A device on the local network can no longer exhaust connections by never completing the handshake.

## [0.1.0] - 2026-08-08

### Added

- First alpha, licensed under AGPL-3.0.
- Local-first, peer-to-peer notes with no central server; the vault passphrase is the only credential.
- Pair further devices with invite links.
- iOS app for iPhone and iPad.
- Relay: an always-on, ciphertext-only relay (`hypha-peer`) that cannot read notes.
- Publish a note as a static page to any S3-compatible bucket, from desktop, iPhone or iPad.
- Published notes can be passphrase-encrypted and given an expiry date.
- Bucket credentials sync to all devices in the vault.
- Backup and restore; backups written by earlier development builds were empty.
- Change the vault passphrase without re-encrypting the vault.
- Deleted items and history are cleaned up on every device, not only on the relay.

### Changed

- Breaking: the sync wire format changed. Update every device and relay together; mismatched builds refuse to connect.
- Sync runs separately for each vault.

### Fixed

- Payloads over 64 KiB are no longer corrupted in transit.
- Opening a note no longer re-downloads its whole contents.
- Devices on the same network no longer flood it with discovery traffic.
- Deleting a reminder or unpinning a shortcut now applies on every device.
- A missing attachment file is requested again until it arrives.
- Backups "with attachments" now contain the attachments.
- iOS: a joined vault's notes appear without writing a note first.
- iOS: the keyboard appears in text fields.
- iOS: the app fills the screen around the notch.
- iOS: the app no longer freezes while a peer edits the same note.
- The restore file picker shows backup files.
- Undo only reverts your own edits, not a peer's.
- macOS: reopening the app after closing the last window restores sync, links and the tray.
- A note window locking no longer breaks the main window's database.
- Sync no longer hangs when a window closes.
- Malformed or unauthenticated sync messages are rejected instead of crashing or being processed.
- Concurrent operations can no longer corrupt data.
- Notes opened before a peer is found update once it connects.
- Sync errors are reported instead of being silent.
- Settings and Changelog windows open correctly.
- Generating an invite no longer fails with "incomplete input".
- A new device no longer makes itself the vault owner.
- Edits keep syncing after switching notes.
- Switching to an empty note no longer shows the previous note's text.
- Tags no longer duplicate across devices.
- Synced notes are searchable without being opened.

### Removed

- Unused storage and compression components.

### Security

- Clipped web pages are isolated by a second barrier.
- "Open externally" no longer hands a peer-chosen file name straight to the system.
- Release notes are no longer rendered as raw HTML.
- Backups and imports are confined to a folder you chose.
- The desktop app runs in the OS sandbox.
- Links in notes are limited to safe schemes; internal links are no longer stripped.
- The database refuses SQL that names a file path.
- Sync rejects attachment requests that try to reach other files.
