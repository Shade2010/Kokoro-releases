# Changelog

All notable changes to Kokoro are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Release channels:
- **Stable** — full releases (e.g. `0.1.0`). What the auto-updater installs by default.
- **Beta / hotfix** — prereleases (e.g. `0.2.0-beta.1`), published as GitHub *prereleases*.
  Only delivered to users who opt into the beta channel in Settings → App updates.

## [Unreleased]

## [0.9.0] — 2026-07-29
The in-app updater now works reliably — and downloads only what changed.

### Fixed
- **Auto-updates no longer stall at "100% downloaded"** and now install correctly. On this unsigned
  build a code-signing publisher check was blocking a finished download from installing; it's removed.
- **Small, fast updates**: updates download only the changed parts of the installer (a few MB) via
  differential (delta) downloads, instead of the whole ~400 MB file every time.
- **Updater diagnostics**: the updater writes a log to the app-data `logs/updater.log`, so any future
  hiccup can be pinpointed instead of failing silently.

## [0.8.2] — 2026-07-29
Reader navigation polish and a fix for updates that could get stuck at "100% downloaded".

### Changed
- **Long-strip navigation**: in Long strip mode the chapter buttons now default to right-to-left
  (Next on the left, Previous on the right), matching manga convention.
- **Display panel auto-closes**: the reader's ⚙ Display panel now dismisses itself after 15 seconds
  with no interaction, or as soon as you click outside it.

### Fixed
- **Updates no longer stall at "100% downloaded"**: the updater now downloads the full installer
  rather than a differential (blockmap) patch, which could hang at 100% and never install.

## [0.8.1] — 2026-07-29
Engine update that gets Cloudflare-protected sources reading again, plus extension-repository management.

### Added
- **Extension repositories**: a new **Extension repos** section in Settings → manage a collection of
  repos, adding or removing any by URL. **Keiyoushi** (primary) and **Suwayomi's** repo come preloaded.
  Each extension now shows **which repo it installs from**, and you can **filter the extension list by
  repo**.

### Fixed
- **Cloudflare sources read again**: updated the bundled manga engine, whose embedded-browser update
  fixes the Cloudflare check that was hanging on sources like AllManga — chapters now load in a couple
  of seconds instead of spinning indefinitely.
- **Seamless engine upgrades**: when a Kokoro update ships a newer engine, your installed extensions are
  automatically re-prepared for it on first launch (otherwise they'd silently fail to load and their
  sources would vanish). Your library, reading history, and downloads are untouched.
- **"Check for updates"**: the extension update-check button was erroring out and doing nothing; it
  works again.
- **Honest extension updates**: updating an extension no longer claims "Updated" when the repo can't
  actually provide a newer version — you're told nothing changed instead of being left with a button
  that never clears.

## [0.8.0] — 2026-07-27
First **stable** release — **Kokoro** (心). Formerly the Riot Manga Viewer beta series, now brought
together under the new name as the first build on the stable channel. It carries the full feature set
from the 0.1.0-beta.1 → beta.4 previews (reader overhaul, install-anywhere storage, tag picker,
ultraviolet themes, CBZ downloads, auto-updates — see the sections below) plus the rebrand:

### Changed
- **New name and logo**: the app is **Kokoro** everywhere — window title, system tray, taskbar,
  desktop and Start-menu shortcuts, the installer, and the Apps & Features entry. A new gold-on-black
  brush icon replaces the old logo across every theme.
- **Seamless move from Riot Manga Viewer**: the first time you open Kokoro it automatically carries
  over your existing data — library, reading history, settings and theme, installed extensions, the
  engine database, and any downloaded chapters — so you pick up exactly where you left off. The
  download folder is re-homed for you, and your old Riot Manga Viewer data is left untouched as a
  backup (safe to delete once you're happy).
- **Installs as a new app**: because of the rename, Kokoro installs alongside your old
  "Riot Manga Viewer" rather than updating it. Uninstall the old entry whenever you're ready — your
  data has already been carried over.

## [0.1.0-beta.4] — 2026-07-27
Fourth beta — a big reader overhaul, install-anywhere storage, and performance fixes.

### Added
- **Reader**
  - **Auto view mode** (new default): each title opens in the right mode automatically — webtoons/manhwa
    (tall vertical strips) in Long strip, page-based manga in Paged. Choose a fixed default (Auto / Paged
    / Long strip) in Settings → Reader or the reader's View-mode dropdown; explicit modes still offer a
    one-tap switch when a title doesn't match.
  - **Pages at once**: show 1–10 pages side by side in Paged mode. Right-to-left reverses the spread so
    the earlier page sits on the right (manga order); stepping and resume align to spreads.
  - **Page scaling**: choose how a page is sized — **Fit** (whole page on screen), **Fill width**, or a
    **Custom %** of the column width (Fill/Custom scroll if the page is taller).
  - **Hide pages**: right-click a page (or hover it and press **h**) to hide a stray notes/ad page so it
    stops throwing off two-page spreads; **u** undoes the last hide. Persists per chapter.
- **Install anywhere, keep C: clean**: the installer lets you choose the install location, and if you
  install off the C: drive, ALL app data — the manga engine, installed extensions, downloaded chapters,
  caches, the bundled Cloudflare services, and even update downloads — is kept on that drive. Nothing of
  ours lives on C:. The new Settings → Storage locations section shows exactly where everything is.

### Changed
- **Reader**
  - **True paged mode**: each page now fits entirely on screen, so a tall page no longer scrolls like a
    strip.
  - **Mode-aware settings**: the Display panel shows only the options that apply to the current view mode
    (Paged hides the long-strip options; Long strip hides reading direction).
  - **Directional nav**: the chapter/page buttons and their ‹ › arrows mirror the reading direction
    (forward on the left for right-to-left and top-down).

### Fixed
- **Query cancellation**: leaving a page (search, details, reader) now cancels its in-flight source
  queries, so a slow request no longer leaves the rest of the app stuck loading.
- **Changelog viewer**: a bullet whose text wraps across lines no longer breaks mid-sentence into a
  separate, differently-styled paragraph.

## [0.1.0-beta.3] — 2026-07-24
Third beta — ultraviolet themes plus update and changelog polish.

### Added
- **Ultraviolet themes** (Settings → Appearance → Theme): a violet-accented family with a recolored
  app logo — **Ultraviolet Warm** and **Ultraviolet OLED**, each as a flat **(lite)** variant and a
  full variant with a violet glow, a glammed-up title bar, and a smooth sheen that sweeps over the
  logo while the app loads.

### Fixed
- **Update notes**: the "update available" prompt now shows this version's changelog (rendered as clean
  text) instead of the raw commit message with visible HTML tags. Release notes are published from
  CHANGELOG.md automatically.
- **"What's new" viewer**: now shows only the version you just installed (with a link to GitHub for the
  full history) instead of the entire changelog, and no longer renders cramped or cut off mid-item
  (the modal was being squeezed to 400px by a CSS specificity clash).

### Changed
- **Library cards**: show the source's name at the bottom instead of its numeric source ID.
- **"What's new" popup**: wider, with a larger, more prominent Riot Manga icon.

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

[Unreleased]: https://github.com/Shade2010/Kokoro-releases/releases
[0.9.0]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.9.0
[0.8.2]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.8.2
[0.8.1]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.8.1
[0.8.0]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.8.0
[0.1.0-beta.4]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.1.0-beta.4
[0.1.0-beta.3]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.1.0-beta.3
[0.1.0-beta.2]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.1.0-beta.2
[0.1.0-beta.1]: https://github.com/Shade2010/Kokoro-releases/releases/tag/v0.1.0-beta.1
