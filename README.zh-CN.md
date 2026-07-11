# Harbor（港湾）

[English](README.md) | **中文**

面向 [Emby](https://emby.media/) 的原生桌面客户端，基于 **Tauri 2**、**React** 与 **Rust**。

Harbor 面向桌面使用场景：浏览媒体库、继续观看，并通过内嵌 **libmpv** 播放；可选接入兼容 danmu_api 协议的弹幕源。

> **状态：** 早期预览（`0.1.0`），接口与界面可能调整。

---

## 截图

> 将图片放入 [`docs/screenshots/`](docs/screenshots/)。建议文件名如下。

### 首页

![首页](docs/screenshots/home.png)

### 媒体库

![媒体库](docs/screenshots/library.png)

### 详情

![详情](docs/screenshots/detail.png)

### 播放器

![播放器](docs/screenshots/player.png)

### 设置

![设置](docs/screenshots/settings.png)

---

## 功能

- **媒体库** — 浏览视图、文件夹、剧集、电影、合集
- **继续观看 / Next Up** — 断点续播；可从继续观看中移除
- **原生播放** — 内嵌 libmpv（macOS / Windows）
- **字幕** — 服务器字幕轨 + 本地外挂字幕
- **弹幕（可选）** — 多弹幕源、热力条跳转、播放器内选源
- **桌面窗口** — macOS Overlay 标题栏；Windows 无边框自定义标题栏
- **主题** — 浅色 / 深色 / 跟随系统，多种强调色与背景
- **安全会话** — Emby Token 由 Rust 侧写入系统钥匙串

---

## 支持平台

| 平台 | 说明 |
|------|------|
| macOS（Apple Silicon / Intel） | Overlay 标题栏；libmpv 本地 / 打包库 |
| Windows（x64） | 无边框窗口；随应用分发 `libmpv-2.dll` |

---

## 环境要求

- 可访问的 Emby 服务器
- **使用发行版：** 从 Releases 下载安装包（发布后）
- **从源码构建：** Node.js 20+、Rust stable，以及 libmpv — 完整源码就绪后见 [docs/MPV_SETUP.md](docs/MPV_SETUP.md)

---

## 快速开始

### 使用发行版

1. 从 [Releases](https://github.com/envyafish/Harbor/releases) 下载最新 `.dmg`（macOS）或 Windows 安装包 / 压缩包。
2. 打开 Harbor，填写 Emby 服务器地址、用户名与密码登录。

### 从源码运行

```bash
npm install
npm run tauri:dev:mpv    # 推荐：启用原生播放
# 或
npm run tauri dev        # 仅界面 / 不启用 mpv feature
```

生产构建：

```bash
npm run build
npm run tauri build -- --features mpv
```

弹幕配置（可选）：[docs/DANMAKU_SETUP.md](docs/DANMAKU_SETUP.md)。

---

## 架构

```
React (Vite) ── invoke ──► Rust commands ── HTTP ──► Emby Server
                                │
                                └── libmpv（feature: mpv）
```

设计令牌（Liquid Glass）：[docs/design/liquid-glass.md](docs/design/liquid-glass.md)。

---

## 常用脚本

| 命令 | 说明 |
|------|------|
| `npm run dev` | 仅 Vite 前端 |
| `npm run build` | TypeScript + Vite 生产构建 |
| `npm run lint` | ESLint |
| `npm run test` | Vitest |
| `npm run tauri:dev:mpv` | Tauri 开发模式 + mpv |
| `npm run tauri build -- --features mpv` | 带 mpv 的桌面发行构建 |

---

## 隐私与安全

- 账号与访问令牌在 Rust 侧处理，并写入系统钥匙串。
- Harbor 只连接**你自己的** Emby 服务器，不需要 Harbor 云账号。
- 若启用弹幕，请求发往**你配置的**弹幕服务器；本应用不支持发送弹幕。

---

## 参与贡献

欢迎 Issue 与 Pull Request。请保持改动聚焦，并尽量遵循现有代码风格。

---

## 许可证

待定 — 正式公开发布时补充 License 文件。

---

## 致谢

- [Emby](https://emby.media/)
- [mpv](https://mpv.io/) / libmpv
- [Tauri](https://tauri.app/)
- [danmu_api](https://github.com/huangxd-/danmu_api) 及兼容弹幕服务
- [弹弹play](https://www.dandanplay.com/) 开放平台（协议兼容）
