# Harbor

[中文](README.md) | **English**

A native desktop client for [Emby](https://emby.media/).

Harbor is built for everyday desktop use: browse your libraries, continue where you left off, and play with embedded **libmpv**. Optional danmaku is available from danmu_api–compatible sources you configure yourself.

---

## Screenshots

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
- **Continue watching & Next Up** — resume playback; remove items from resume when needed
- **Native playback** — embedded libmpv on macOS and Windows
- **Subtitles** — server subtitle tracks and local external subtitle files
- **Danmaku (optional)** — multiple danmu_api–compatible sources, heatmap seek, in-player source picker
- **Desktop experience** — macOS overlay title bar; Windows frameless custom title bar
- **Themes** — light / dark / system, with multiple accents and backgrounds
- **Secure session** — Emby credentials and tokens stored in the system keyring

---

## Platforms

| Platform | Notes |
|----------|--------|
| macOS 26+ (Apple Silicon only) | Overlay title bar; native playback bundled with the app |
| Windows 10+ (x64) | Frameless window; native playback bundled with the app |

Current installers support **Windows 10** (x64) and **macOS 26** or later (**Apple Silicon only**).

---

## Requirements

- An Emby server you can reach over the network
- Windows 10+ (x64), or macOS 26+ (Apple Silicon only)

---

## Get started

1. Download the latest `.dmg` (macOS) or installer / zip (Windows) from [Releases](https://github.com/envyafish/Harbor/releases).
2. Open Harbor and sign in with your Emby server URL, username, and password.

---

## Privacy & security

- Credentials and access tokens are stored in the system keyring.
- Harbor connects only to **your** Emby server. It does not require a Harbor cloud account.
- If danmaku is enabled, requests go only to servers **you** configure. Harbor does not send danmaku.

---

## Feedback

Bug reports and feature requests are welcome via [GitHub Issues](https://github.com/envyafish/Harbor/issues).

Source code is not publicly available.

---

## License

Proprietary. All rights reserved.

---

## Acknowledgements

- [Emby](https://emby.media/)
- [mpv](https://mpv.io/) / libmpv
- [Tauri](https://tauri.app/)
- [danmu_api](https://github.com/huangxd-/danmu_api) and compatible danmaku providers
- [弹弹play](https://www.dandanplay.com/) open platform (protocol compatibility)
