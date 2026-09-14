# Security

Hypha encrypts your notes and syncs them directly between your own devices. If
that is going to be worth anything, the failures have to be findable and
reportable. This page is how.

## Reporting a vulnerability

**krst@riseup.net**

Please report privately first, and give a reasonable window before disclosing.
There is no bug bounty — this is one person's project — but every report gets a
reply and credit in the changelog unless you would rather not have it.

Useful in a report:

- what an attacker gets, and what they need to have or to be in order to get it;
- steps to reproduce, or the reasoning if it is a design flaw rather than a bug;
- the version, and which platform.

**Do not attach a backup file or a vault to a report.** A backup is not an
encrypted file — see below.

## What Hypha claims, and what it does not

Claiming precisely matters more here than claiming strongly.

**What is protected**

- **Note titles and bodies are encrypted at rest**, with a key derived from your
  passphrase (Argon2id) and sealed with XChaCha20-Poly1305. Titles live in a
  cipher column; bodies are sealed CRDT snapshots.
- **Attachments are encrypted at rest**, and addressed by the hash of their
  ciphertext.
- **Sync traffic is end-to-end encrypted** between paired devices, over a Noise
  handshake. There is no server that can read it, because there is no server.
- **There is no account, no telemetry, no analytics and no crash reporting.**
  Nothing is sent anywhere you did not pair with.

**What is not protected, and you should assume is readable**

- **Everything that is not a note.** Tag names, notebook names, reminder titles
  *and* descriptions, settings values, attachment filenames, MIME types, sizes
  and plaintext hashes are stored **in the clear**. Only notes are sealed.
- **Vault names**, which sit in the clear in the local registry. This was a
  decision, not an oversight.
- **A backup file**, which carries all of the above in the clear plus the vault
  credential. Treat a backup as sensitive even though the notes inside it are
  encrypted. `docs/BACKUP-CONFIDENTIALITY.md` is the full accounting, taken by
  exporting a vault and reading the bytes rather than by reading the code.
- **Metadata about your activity** — how many notes you have, when they changed,
  how big your attachments are — is visible to anything that can read the
  database file.
- **Anyone with your passphrase and your device.** There is no second factor.
- **A search index and, where semantic search is on, an embedding index, both
  over plaintext, inside the encrypted database file.** They are cleared when
  the vault locks and rebuilt after unlock. Until the lock — including after a
  crash or a force-quit — a copy of every note's text is in that file, protected
  by the database key (kept in the OS keychain) and not by your passphrase.
  Being fixed; see `docs/SECURITY-AUDIT-2026-08-25.md`.
- **Attachment names on the sync wire and in a relay's blob store** are, for
  attachments stored before ciphertext addressing landed, a hash of the file's
  plaintext — a "do you have this exact file" oracle for anyone who can see a
  frame or list the directory. Ciphertext addressing exists and is not yet the
  default.
- **Anything that can run code in the note window** — a renderer XSS — can read
  the database key and the vault key out of the OS keychain through the same
  bridge the app uses. The window is the crypto boundary; a compromise of it is
  a compromise of the vault at rest, not only while it is unlocked. That is why
  synced note content is treated as untrusted input (external images are not
  fetched without your say-so, embeds cannot open windows or take permissions).

**What has not been established**

- **The cryptography has not been independently audited.** It is built from
  standard, well-regarded primitives (libsodium, Argon2id, XChaCha20-Poly1305,
  Noise-XX) rather than invented ones, and that is a much weaker statement than
  "audited". Nobody outside this project has reviewed how they are composed.
  An internal audit on 2026-08-25 (`docs/SECURITY-AUDIT-2026-08-25.md`) found
  real problems in how they are composed — among them, that the context
  binding (AAD) designed for every sealed field is not yet switched on, that
  the passphrase KDF runs at libsodium's *interactive* cost while its verifier
  travels in backups and invite links, and that a joining device shows its
  invite to any peer that connects. Those are open and listed there with the
  rest; do not read "standard primitives" as "composed correctly".
- **The desktop-to-desktop path over the internet is unproven.** Everything to
  date has been one Mac and one phone.

## Passphrases and recovery

There is **no recovery**. No reset link, no support account, no escrow. If you
forget the passphrase, the notes are unrecoverable by anyone including the
author. This is the intended behaviour and the direct cost of having no server.

Keep the passphrase somewhere you will still have it in a year, and keep your
own backups of anything you cannot lose.

## Scope

In scope: anything that reads note contents without the passphrase, anything
that lets a device sync into a vault it was not paired with, anything that
writes plaintext where the design says ciphertext, and anything that lets a web
page or another app reach the native bridges.

Out of scope: an attacker who already has your unlocked device; the known
plaintext listed above, which is documented rather than fixed; and anything that
requires physical access to a machine that is already compromised.
