<div align="center">

<img src="docs/logo.png" width="120" height="120" alt="Harbor">

# Harbor（港湾）

**面向 [Emby](https://emby.media/) / [Jellyfin](https://jellyfin.org/) 的桌面、电视与移动客户端**

[![桌面版](https://img.shields.io/github/v/release/envyafish/Harbor?style=flat-square&label=desktop)](https://github.com/envyafish/Harbor/releases/latest)
[![电视版](https://img.shields.io/github/v/release/envyafish/Harbor-Android-TV-Release?style=flat-square&label=tv)](https://github.com/envyafish/Harbor-Android-TV-Release/releases/latest)
[![移动端](https://img.shields.io/github/v/release/envyafish/harbor-android-mobile-release?style=flat-square&label=mobile)](https://github.com/envyafish/harbor-android-mobile-release/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/envyafish/Harbor/total?style=flat-square)](https://github.com/envyafish/Harbor/releases)

[下载](https://github.com/envyafish/Harbor/releases/latest) · [Harbor TV](https://github.com/envyafish/Harbor-Android-TV-Release) · [Harbor 移动端](https://github.com/envyafish/harbor-android-mobile-release) · [反馈 Bug](https://github.com/envyafish/Harbor/issues) · [购买](https://wzyp.cn/shop/767OK1ZS) · [TG 交流群](https://t.me/HarborRelease)

</div>

---

本仓库是 **Harbor 桌面端**。其他客户端请前往对应发行仓：

- [Harbor TV](https://github.com/envyafish/Harbor-Android-TV-Release)
- [Harbor 移动端](https://github.com/envyafish/harbor-android-mobile-release)

亦兼容 [极影视](https://www.zspace.cn/)（桌面端，缺乏充分测试）。

---

## 购买

可通过 [店铺](https://wzyp.cn/shop/767OK1ZS) 购买 Harbor Pro。同一许可证可用于桌面端、[Harbor TV](https://github.com/envyafish/Harbor-Android-TV-Release) 与 [Harbor 移动端](https://github.com/envyafish/harbor-android-mobile-release)。

---

## Harbor 桌面端

桌面端面向 Emby / Jellyfin 的日常使用：侧栏切换媒体库，首页继续观看，详情页选音轨与字幕，再用内嵌 libmpv 播放。账号与令牌保存在系统钥匙串，不需要 Harbor 云账号。

### 首页

打开后是 Hero 推荐与媒体库入口。下方是继续观看，以及各库的最新内容；剧集海报会标出未看集数。

<img src="docs/素材/pc/企业微信20260901-084343.png" alt="首页 Hero 与媒体库" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084423.png" alt="继续观看与最新内容" width="100%" />

### 媒体库

每个库是海报网格。可按全部 / 继续观看 / 未观看 / 已观看 / 收藏筛选，也可按年份、评分、添加日期排序，并搜索本库。

<img src="docs/素材/pc/企业微信20260901-085321.png" alt="媒体库网格" width="100%" />

### 详情

电影与剧集都是沉浸式详情：海报取色背景、播放 / 收藏 / 已看、音轨与字幕、媒体信息，以及 IMDb、TMDb、Trakt 外链。剧集页可按季浏览，点进单集继续看。

详情页还可以**生成本地中文字幕**（Pro）：从音轨识别，日语可直译或转译。

<img src="docs/素材/pc/企业微信20260901-084437.png" alt="电影详情" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084612.png" alt="剧集详情" width="100%" />

向下滚动可见章节、演职员与相似内容。点演员会进入作品列表。

<img src="docs/素材/pc/企业微信20260901-084454.png" alt="章节、演职员与相似内容" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084530.png" alt="剧集分集列表" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084507.png" alt="演职员页" width="100%" />

### 收藏与搜索

收藏按媒体库分组。搜索支持电影、剧集、单集、音乐与演职员，并记住最近关键词。

<img src="docs/素材/pc/企业微信20260901-084711.png" alt="收藏" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084728.png" alt="搜索" width="100%" />

### 播放器

内嵌 libmpv，Direct Play / Direct Stream 自动回退。进度条、倍速、音量、音轨 / 字幕 / 双字幕、弹幕、画中画、全屏都在播放器里完成。进度会回写服务器。

<img src="docs/素材/pc/企业微信20260901-085213.png" alt="桌面播放器" width="100%" />

播放相关能力：

- **原生播放** — macOS / Windows 随应用分发 libmpv；也可改用外部 mpv / VLC / PotPlayer，并同步进度
- **字幕** — 服务器字幕轨、本地外挂、双字幕；字号、位置、颜色、描边、底框可调
- **生成中文字幕（Pro）** — 本机 Whisper 识别音轨，可选译成中文，并可上传回 Emby
- **弹幕（Pro，可选）** — 兼容 danmu_api 的多源、热力条跳转、播放中换源；只看不发
- **Anime4K（Pro）** — 动画超分，可仅对动画生效
- **跳过片头片尾（Pro）** — 手动 / 自动延迟 / 自动即时；服务器无标记时用 IntroDB 补缺
- **HDR / 杜比** — 检测到 HDR10 / HDR10+ / HLG / 杜比视界时，可自动切独立窗口或外部播放器

### 观影统计

按月看总时长、电影 / 剧集占比、题材与年代，以及本月 Top 剧集 / 电影。还有星期偏好、时段分布、评分画像和连续打卡日历。

<img src="docs/素材/pc/企业微信20260901-084801.png" alt="观影统计总览" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084814.png" alt="本月 Top 剧集与电影" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084825.png" alt="星期偏好与时段分布" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084834.png" alt="连续打卡日历" width="100%" />

### 日历

连接 Trakt 后，按「播出 / 新剧」看本周或本月更新，方便追更。想看列表也在侧栏。

<img src="docs/素材/pc/企业微信20260901-084902.png" alt="播出日历" width="100%" />

### 控制台

查看服务器上正在播放的会话、在线设备，必要时可踢出。播放历史可按今天 / 7 天 / 30 天筛选。

<img src="docs/素材/pc/企业微信20260901-084919.png" alt="控制台在线设备" width="100%" />

<img src="docs/素材/pc/企业微信20260901-084927.png" alt="控制台播放历史" width="100%" />

### 设置

设置按账号、媒体库、外观、播放、字幕、Trakt、弹幕、快捷键、存储、关于分区。播放页可调内置 / 外部播放器、默认音轨字幕语言、硬件解码、缓存、跳过片头片尾、字幕外观、Anime4K，以及生成本地字幕的识别模型。

<img src="docs/素材/pc/企业微信20260901-085031.png" alt="播放设置" width="100%" />

<img src="docs/素材/pc/企业微信20260901-085049.png" alt="字幕外观设置" width="100%" />

<img src="docs/素材/pc/企业微信20260901-085108.png" alt="Anime4K 与生成字幕" width="100%" />

主题支持浅色 / 深色 / 跟随系统，多种强调色与背景。macOS 使用 Overlay 标题栏，Windows 为无边框自定义标题栏。

### 桌面端功能一览

- **媒体库** — 浏览视图、文件夹、剧集、电影、合集、播放列表
- **继续观看 / Next Up** — 断点续播；可从继续观看中移除
- **收藏、搜索、想看** — 侧栏直达
- **原生播放** — 内嵌 libmpv；可选外部播放器
- **字幕** — 服务器轨、本地外挂、双字幕、外观微调、本地生成中文字幕
- **弹幕** — 多源、热力条、播放中选源
- **Trakt** — 播放同步、已看对账、日历、想看
- **观影统计** — 月度时长、题材、打卡、Top 榜
- **控制台** — 在线会话与播放历史
- **安全会话** — 服务器账号与令牌保存在系统钥匙串

---

## 支持平台

| 平台 | 说明 |
|------|------|
| macOS 26+（Apple Silicon / Intel） | Overlay 标题栏；原生播放随应用分发 |
| Windows 10+（x64） | 无边框窗口；原生播放随应用分发 |

当前安装程序支持 **Windows 10**（x64）与 **macOS 26** 及以上。

电视与移动端见 [Harbor TV](https://github.com/envyafish/Harbor-Android-TV-Release)、[Harbor 移动端](https://github.com/envyafish/harbor-android-mobile-release)。

---

## 支持的媒体服务器

| 服务器 | 说明 |
|--------|------|
| [Emby](https://emby.media/) | 主要支持 |
| [Jellyfin](https://jellyfin.org/) | 已支持 |
| [极影视](https://www.zspace.cn/) | 兼容，缺乏充分测试 |

---

## 开始使用

**桌面端**

1. 从 [Releases](https://github.com/envyafish/Harbor/releases) 下载最新 `.dmg`（macOS）或 Windows 安装包 / 压缩包。
2. 打开 Harbor，填写服务器地址、用户名与密码登录。

若需手动准备字幕生成模型（Sidecar），见 [手动下载教程](docs/MANUAL_SIDECAR_MODELS.md)。

电视与移动端请到 [Harbor TV](https://github.com/envyafish/Harbor-Android-TV-Release)、[Harbor 移动端](https://github.com/envyafish/harbor-android-mobile-release) 下载。

---

## 隐私与安全

- 账号与访问令牌保存在系统钥匙串中。
- Harbor 只连接**你自己的**媒体服务器，不需要 Harbor 云账号。
- 若启用弹幕，请求仅发往**你配置的**弹幕服务器；本应用不支持发送弹幕。

---

## 反馈

欢迎通过 [GitHub Issues](https://github.com/envyafish/Harbor/issues) 提交问题与功能建议。

电视版见 [Harbor TV](https://github.com/envyafish/Harbor-Android-TV-Release)，移动端见 [Harbor 移动端](https://github.com/envyafish/harbor-android-mobile-release)。本项目不开放源代码。

---

## 许可证

专有软件，保留所有权利。

---

## 致谢

- [Emby](https://emby.media/)
- [Jellyfin](https://jellyfin.org/)
- [极影视](https://www.zspace.cn/)
- [mpv](https://mpv.io/) / libmpv
- [Tauri](https://tauri.app/)
- [danmu_api](https://github.com/huangxd-/danmu_api) 及兼容弹幕服务
- [弹弹play](https://www.dandanplay.com/) 开放平台（协议兼容）
