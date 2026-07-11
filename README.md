# Harbor（港湾）

**中文** | [English](README.en.md)

面向 [Emby](https://emby.media/) 的原生桌面客户端。

Harbor 面向日常桌面使用：浏览媒体库、继续观看，并通过内嵌 **libmpv** 播放。可选接入你自行配置的、兼容 danmu_api 协议的弹幕源。

---

## 截图

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
- **原生播放** — macOS / Windows 内嵌 libmpv
- **字幕** — 服务器字幕轨与本地外挂字幕
- **弹幕（可选）** — 多弹幕源、热力条跳转、播放器内选源
- **桌面体验** — macOS Overlay 标题栏；Windows 无边框自定义标题栏
- **主题** — 浅色 / 深色 / 跟随系统，多种强调色与背景
- **安全会话** — Emby 账号与令牌保存在系统钥匙串

---

## 支持平台

| 平台 | 说明 |
|------|------|
| macOS（Apple Silicon / Intel） | Overlay 标题栏；原生播放随应用分发 |
| Windows（x64） | 无边框窗口；原生播放随应用分发 |

---

## 环境要求

- 可访问的 Emby 服务器
- 上述 macOS 或 Windows 系统

---

## 开始使用

1. 从 [Releases](https://github.com/envyafish/Harbor/releases) 下载最新 `.dmg`（macOS）或 Windows 安装包 / 压缩包。
2. 打开 Harbor，填写 Emby 服务器地址、用户名与密码登录。

---

## 隐私与安全

- 账号与访问令牌保存在系统钥匙串中。
- Harbor 只连接**你自己的** Emby 服务器，不需要 Harbor 云账号。
- 若启用弹幕，请求仅发往**你配置的**弹幕服务器；本应用不支持发送弹幕。

---

## 反馈

欢迎通过 [GitHub Issues](https://github.com/envyafish/Harbor/issues) 提交问题与功能建议。

本项目不开放源代码。

---

## 许可证

专有软件，保留所有权利。

---

## 致谢

- [Emby](https://emby.media/)
- [mpv](https://mpv.io/) / libmpv
- [Tauri](https://tauri.app/)
- [danmu_api](https://github.com/huangxd-/danmu_api) 及兼容弹幕服务
- [弹弹play](https://www.dandanplay.com/) 开放平台（协议兼容）
