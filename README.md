# hypha — releases

Downloads, the changelog and the privacy policy for **hypha**, a local-first,
end-to-end-encrypted notes app for macOS and iOS.

**There is no source code here.** hypha is source available, not open source,
and the source lives in a private repository. This repo exists because GitHub
release assets inherit repository visibility: a private repo cannot serve public
downloads, and `electron-updater` cannot read an update manifest it needs a
token to fetch.

- **[Releases](../../releases)** — the installers, with `SHA256SUMS.txt` for each.
- **[CHANGELOG.md](CHANGELOG.md)** — read by the desktop app's *What's New*
  window, which fetches this file directly.
- **[Privacy policy](https://marcolaux.github.io/hypha-releases/privacy)** —
  short version: hypha collects nothing.

The app is on iOS through TestFlight, listed as **hypha notes**.

Both Markdown files here are copies. The originals live in the source repo
(`CHANGELOG.md` and `docs/PRIVACY-POLICY.md`) and are updated there first.

## Licence

hypha is distributed under the Hypha Source Available License 1.0. The licence
text ships with every release and lives in the source repository.
