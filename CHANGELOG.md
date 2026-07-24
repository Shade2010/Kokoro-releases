# Changelog

All notable changes to Riot Manga Viewer are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Release channels:
- **Stable** — full releases (e.g. `0.1.0`). What the auto-updater installs by default.
- **Beta / hotfix** — prereleases (e.g. `0.2.0-beta.1`), published as GitHub *prereleases*.
  Only delivered to users who opt into the beta channel in Settings → App updates.

## [Unreleased]

## [0.1.0-beta.2] — 2026-07-24
Second beta — stability and safe-update fixes on top of beta.1.

### Fixed
- **FlareSolverr process leak**: its detached Chromium/driver children could orphan and pile up across
  sessions. They're now reliably killed (by folder path) on stop, and any strays are reaped at startup.
- **Update status**: a failed update check no longer dumps a raw error blob into Settings; beta builds
  follow the beta channel automatically so beta→beta updates work.
- **Update safety**: auto-updates never touch your data — the silent uninstall phase now hard-skips the
  optional data-deletion prompt (library, extensions, settings and downloads are always kept on update).

### Changed
- **Networking**: the installer now grants Windows Firewall access to the app and bundled engine up
  front, and the Cloudflare solver binds to localhost — so there are no first-run firewall prompts.
- **Installer**: the optional Cloudflare helpers (Browser / Solver) are now checked by default.
- **Uninstall**: your library, history, settings and downloads are now kept by default — the
  uninstaller asks first, and only removes them if you choose to.
- **Program name**: the installed app now shows as just "Riot Manga Viewer" in Apps & Features (the
  version lives in the file's Properties → Details, not the name).

## [0.1.0-beta.1] — 2026-07-24
First beta release — the full feature set, published to the **beta channel** for testing before a
stable cut. Enable *Settings → App updates → Include beta & hotfix releases* to receive it.

### Added
- **Manga engine**: bundles Suwayomi as a local engine and acts as a themed Electron client to the
  Keiyoushi/Mihon extension catalog (1300+ sources). Uses a bundled JDK — no separate Java install.
- **Search & browse**: aggregated search across all enabled sources (one row each) plus a
  single-extension grid with infinite scroll.
- **Native genre/tag search** using each source's real filter API, with a **tag picker** dropdown to
  choose a source's actual tags (include / exclude, multi-select) instead of guessing names.
- **Tag-click fallback**: clicking a metadata tag a source can't filter by now falls back to a
  client-side genre scan so it still finds matches.
- **Reader**: paged (RTL/LTR) and long-strip modes, read tracking, and read-ahead prefetch.
- **Library** with unread counts, reading history, and per-chapter **CBZ downloads** for offline reading.
- **Cloudflare access options**: embedded browser (CEF), FlareSolverr, and an in-app assisted solver
  for interactive challenges.
- **Desktop app polish**: system tray, close-to-tray, start-with-Windows, frameless themed window
  (dark / OLED / OLED-red), and a themed NSIS installer.
- **Automatic updates**: silently checks GitHub Releases at startup and prompts to download & install
  a newer version. Opt-in **beta channel** in Settings delivers prereleases (hotfixes / unstable builds).
- **In-app changelog**: a "What's new" viewer in Settings → App updates, and the changelog pops up
  automatically the first time you launch after an update.

[Unreleased]: https://github.com/Shade2010/RiotMangaViewer-releases/releases
[0.1.0-beta.2]: https://github.com/Shade2010/RiotMangaViewer-releases/releases/tag/v0.1.0-beta.2
[0.1.0-beta.1]: https://github.com/Shade2010/RiotMangaViewer-releases/releases/tag/v0.1.0-beta.1
