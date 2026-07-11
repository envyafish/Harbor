# Harbor

**English** | [中文](README.zh-CN.md)

A native desktop client for [Emby](https://emby.media/), built with **Tauri 2**, **React**, and **Rust**.

Harbor focuses on a calm, desktop-first experience: browse your libraries, pick up where you left off, and play with embedded **libmpv** — plus optional danmaku from danmu_api–compatible sources.

> **Status:** early preview (`0.1.0`). APIs and UI may change.

---

## Screenshots

> Drop image files into [`docs/screenshots/`](docs/screenshots/). Suggested names are listed below.

### Home

![Home](docs/screenshots/home.png)

### Library

![Library](docs/screenshots/library.png)

### Detail

![Detail](docs/screenshots/detail.png)

### Player

![Player](docs/screenshots/player.png)

### Settings

![Settings](docs/screenshots/settings.png)

---

## Features

- **Libraries** — browse views, folders, series, movies, and box sets
- **Continue watching & Next Up** — resume playback; hide items from resume when needed
- **Native playback** — embedded libmpv (macOS / Windows)
- **Subtitles** — server tracks plus local external subtitle files
- **Danmaku (optional)** — multi-server danmu_api–compatible sources, heatmap seek, player source picker
- **Desktop chrome** — macOS overlay title bar; Windows frameless custom title bar
- **Themes** — light / dark / system, multiple accents and backgrounds
- **Secure session** — Emby token stored in the OS keyring via Rust

---

## Platforms

| Platform | Notes |
|----------|--------|
| macOS (Apple Silicon / Intel) | Overlay title bar; libmpv via bundled / local libs |
| Windows (x64) | Frameless window; ship `libmpv-2.dll` with the app |

---

## Requirements

- An Emby server you can reach over the network
- **Runtime:** download a release build (when published), or build from source
- **From source:** Node.js 20+, Rust stable, and libmpv — see [docs/MPV_SETUP.md](docs/MPV_SETUP.md) after the full source tree is present

---

## Getting started

### Use a release

1. Download the latest `.dmg` (macOS) or installer / zip (Windows) from [Releases](https://github.com/envyafish/Harbor/releases).
2. Open Harbor and sign in with your Emby server URL, username, and password.

### Build from source

```bash
npm install
npm run tauri:dev:mpv    # recommended: enable native playback
# or
npm run tauri dev        # UI only / without mpv feature
```

Production build:

```bash
npm run build
npm run tauri build -- --features mpv
```

Danmaku setup (optional): [docs/DANMAKU_SETUP.md](docs/DANMAKU_SETUP.md).

---

## Architecture

```
React (Vite) ── invoke ──► Rust commands ── HTTP ──► Emby Server
                                │
                                └── libmpv (feature: mpv)
```

Design tokens (Liquid Glass): [docs/design/liquid-glass.md](docs/design/liquid-glass.md).

---

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Vite frontend only |
| `npm run build` | TypeScript + Vite production build |
| `npm run lint` | ESLint |
| `npm run test` | Vitest |
| `npm run tauri:dev:mpv` | Tauri dev with mpv |
| `npm run tauri build -- --features mpv` | Desktop release with mpv |

---

## Privacy & security

- Credentials and access tokens are handled on the Rust side and stored in the system keyring.
- Harbor talks to **your** Emby server; it does not require a Harbor cloud account.
- Danmaku (if enabled) is fetched from servers **you** configure; Harbor does not send danmaku.

---

## Contributing

Issues and pull requests are welcome. Please keep changes focused and match existing code style.

---

## License

TBD — license file will be added when the public release is finalized.

---

## Acknowledgements

- [Emby](https://emby.media/)
- [mpv](https://mpv.io/) / libmpv
- [Tauri](https://tauri.app/)
- [danmu_api](https://github.com/huangxd-/danmu_api) and compatible danmaku providers
- [弹弹play](https://www.dandanplay.com/) open platform (protocol compatibility)
