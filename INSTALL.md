# Installing Hypha

Hypha is a beta. It is a real notes app holding real notes. Read
[Known limitations](KNOWN-LIMITATIONS.md) before you put anything in it that you
would be upset to lose, and **keep your own backups**.

> **This is a beta**, and the procedure below was written and checked long
> before it was ever walked by a stranger — so if a step does not match what you
> see, that is worth reporting rather than working around.

Downloads: <https://github.com/marcolaux/hypha-releases/releases>

---

## macOS

**Requirements: an Apple-silicon Mac (M1 or later), macOS 12 Monterey or newer.**

Intel Macs are not supported and there is no Intel build. This is deliberate,
not an oversight.

1. Download `hypha_mac_arm64.dmg` from the latest release.
2. Open the `.dmg` and drag Hypha to Applications.
3. Open Hypha from Applications.

If macOS says Hypha cannot be opened, see
[If macOS refuses to open it](#if-macos-refuses-to-open-it) at the end of this
page.

**What to expect on first run:** Hypha will ask for permission to find devices
on your local network. That is how it syncs to your other devices directly,
without a server. If you decline, the app still works; sync over Wi-Fi will not.

**Updates.** Hypha checks for updates and will offer to install them. If a build
turns out not to be notarized, each update is signed with a different identity,
so macOS asks you to re-grant local-network permission after updating — expected,
not the app misbehaving. Auto-update has also **never been observed working end
to end**; see [Known limitations](KNOWN-LIMITATIONS.md).

---

## iPhone

**Requirements: iOS 16.4 or newer, on an iPhone.**

There is no iPad build. The app was designed and tested on a phone and has
never been run on an iPad, so shipping it there would be a guess — see
`apps/mobile/ios/project.yml`'s `TARGETED_DEVICE_FAMILY`.

The iOS build is distributed through **TestFlight**. You need an invitation —
ask for one at the address in [SECURITY.md](SECURITY.md), or use the public
link on the releases page if one is posted.

1. Install **TestFlight** from the App Store.
2. Open the invitation link on the device.
3. Install **hypha notes** from TestFlight — that is the App Store listing
   name; the app itself appears on the home screen as **hypha**.

TestFlight builds expire after 90 days. When one does, update from TestFlight
again — **your notes are not affected**, they live on the device and on
whatever other devices you have paired.

**There is no `.ipa` on the releases page, and there will not be one.** From
0.13.0 the iOS build is an `app-store-connect` export — the package format Apple
accepts for TestFlight and the App Store, which iOS refuses to side-load at all.
Publishing it would offer a download that nobody, including the developer, can
install. TestFlight is the only way onto a phone.

(Before 0.13.0 the `.ipa` WAS published, as a `development` export installable
on devices registered to the developer account. That stopped being true the
moment the first TestFlight build was cut.)

---

## An always-on relay (optional)

Hypha syncs your devices directly, so both have to be awake at the same time.
Write on your phone with the laptop shut and the laptop gets it the next time
you open it — not before. A relay is a third peer that is always awake, which
removes that wait.

It holds **ciphertext only**. It joins your vault as a member with no ability to
read anything in it, and a stolen relay disk yields sealed blobs, not notes. It
is a convenience, not a backup, and nothing about syncing changes if you never
run one.

It wants a machine that is always on — a home server, a NAS, a small VPS.
**Linux is the right home**: on macOS and Windows, Docker cannot pass multicast
through, so the relay will not find devices on your own network and falls back
to the internet path only.

From the [releases page](https://github.com/marcolaux/hypha-releases/releases),
download `hypha-peer-compose.yml` and `hypha-peer.env.example` into an empty
directory:

```sh
mv hypha-peer-compose.yml docker-compose.yml
mv hypha-peer.env.example .env
# open .env and set HYPHA_PEER_SECRETS_PASSPHRASE — `openssl rand -base64 32`

docker compose run --rm peer init
docker compose run --rm peer join "hypha://invite/…"
docker compose up -d
```

The invite comes from the desktop app: **Settings → Sync → Add a device**, for
a relay. **The inviting device has to be online while you run
`join`** — the two complete a live handshake, because there is no server to
redeem a token against.

Afterwards, `docker compose logs -f` shows what it is doing and
`docker compose run --rm peer status` prints a snapshot without disturbing it.

Two things worth knowing before you rely on it. Its data volume holds the
relay's identity, so **back it up** — losing it means re-inviting the relay
(your notes are unaffected; they live on your own devices). And it accumulates
ciphertext forever unless you set `HYPHA_PEER_AUTO_PRUNE_AGE`; the example file
explains the trade-off.

---

## Setting it up

Hypha has **no account and no server**. There is nothing to sign up for and no
password to recover.

- **First device:** you choose a passphrase, and it encrypts the vault. If you
  forget it, the notes are gone. Nobody can reset it. Write it down somewhere
  safe — a password manager, or paper.
- **Second device:** on the first device, open **Settings → Sync → Add a
  device**. On an iPhone, open the code with the Camera app; on a Mac, paste
  the invite link. The new device then asks for the vault's passphrase. The two
  devices sync directly to each other, over Wi-Fi when they are on the same
  network and over the internet when they are not.

Sync needs both devices to be running. There is no server holding a copy while
one of them is asleep.

---

## If something goes wrong

**Report it.** The address is in [SECURITY.md](SECURITY.md). For a
security problem, use that address and please do not post it publicly first.

Useful things to include:

- what you did, and what happened instead;
- the version (Settings → the version is at the bottom);
- your OS version;
- whether it involved two devices, and if so what each was doing.

**Do not send your notes or a backup file** to report a bug. A backup carries
your vault credential, and on a machine with no keychain slot for the backup key
it also leaves names and filenames in the clear — see
[Known limitations](KNOWN-LIMITATIONS.md).

---

## Building it yourself

macOS and iPhone both have builds now (above); building from source is the way
to run it on anything else, or to run unreleased work.
[`README.md`](README.md) has the steps: Node.js 22 or newer, `npm install`,
then `npm run dev` for the desktop app or
`npm run package:mac --workspace apps/desktop` for an installable build.

---

## If macOS refuses to open it

**The first launch may need a right-click.** If double-clicking shows
*"Hypha" cannot be opened because Apple cannot check it for malicious
software*, that is Gatekeeper. A release build should be signed and notarized,
but no published build has exercised that end to end yet, so the prompt is
possible rather than a bug. **Right-click** (or Control-click) Hypha in
Applications → **Open** → **Open** in the dialog. You only have to do this once.

If macOS refuses even after that, first **verify what you downloaded.**
Download `SHA256SUMS.txt` from the same release, put it beside the `.dmg`, and
run:

```sh
shasum -a 256 -c SHA256SUMS.txt
```

You want `OK` on the line for your file. `FAILED` means the download is corrupt
or has been altered — do not open it. (Lines for files you did not download will
say `No such file`; that is fine.)

With the checksum verified, clear the quarantine flag:

```sh
xattr -d com.apple.quarantine /Applications/Hypha.app
```

Only run that on a build whose checksum you verified.
