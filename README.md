# grplayer-app
<div align="center">
<img src="./images/icon.png" alt="logo" width="80" />
<h1>GRPlayer</h1>

一款使用 Java 构建的 Android 原生音乐播放器。支持网易云音乐搜索与播放，并兼容 B 站音乐区音频。更轻量、更顺手的搜索、后台播放、收藏夹、缓存导出、歌词体验、频谱可视化与图形均衡器。

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?style=flat-square&logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Java-orange?style=flat-square&logo=openjdk&logoColor=white)
![UI](https://img.shields.io/badge/UI-Material%203-6750A4?style=flat-square)
![Player](https://img.shields.io/badge/Player-Media3-1DB954?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

</div>

---

## 屏幕截图

| 首页 | 播放器 | 歌词页 | 设置 |
| :--: | :--: | :--: | :--: |
| ![首页](./images/home.png) | ![播放器](./images/player.png) | ![歌词页](./images/lyrics.png) | ![设置](./images/settings.png) |

## 主要功能

### 核心播放体验

- **搜索**：支持单曲、歌手、专辑、歌单搜索；单曲搜索并行请求网易云与 B 站音乐区，按相关度合并展示。
- **后台播放**：基于 Media3 `MediaSessionService`，支持通知栏控制与后台稳定播放。
- **迷你播放条**：自动注入到各页面底部，快速切歌、暂停与进入播放页。
- **悬浮播放条**：支持在系统上层显示可拖拽的播放条，需悬浮窗权限。
- **播放控制**：播放/暂停、上一首、下一首、进度拖拽、顺序播放、随机播放、循环模式。
- **单曲播放模式**：搜索结果单曲点击时按单曲播放，避免误把整个搜索结果作为播放列表。
- **定时关闭**：支持自定义分钟数，到点自动暂停播放。
- **播放页**：大封面、歌曲信息、进度条、加载指示器，支持进入歌词页。
- **播放详情**：可查看播放来源、实际音质、缓存状态、文件大小、播放链接与封面链接，并支持复制。
- **音频来源兼容**：网易云歌曲与 B 站音乐区视频音频走同一套播放、缓存、导出、收藏链路。

### 收藏与歌单

- **本地收藏夹**：新建收藏夹，收藏歌曲到多个文件夹。
- **整专辑 / 歌手 / 歌单收藏**：一键拉取全部歌曲并保存为本地收藏夹。
- **拖拽排序**：支持收藏夹排序与收藏夹内歌曲排序。
- **JSON 歌单导入导出**：导出收藏夹为 JSON 配置，也可从 JSON 文件导入为新收藏夹。
- **类型还原**：JSON 导入时可还原专辑 / 歌手 / 歌单类型与来源 ID，减少重复收藏。
- **旧版兼容**：旧版 JSON 可根据 `bili_` 前缀自动推断 B 站来源。

### 缓存与导出

- **缓存到软件**：支持缓存歌曲并在本地离线播放。
- **缓存管理**：显示缓存进度，支持取消缓存、删除缓存。
- **导出到本地**：导出到 `/Music/GRPlayer/`，自动识别 `.mp3`、`.flac`、`.m4a`、`.mp4` 等扩展名。
- **进度弹窗**：缓存 / 导出均带进度与取消操作。
- **每日限额**：导出默认每日最多 20 个文件。
- **导出冷却**：成功导出后有 60 秒冷却，菜单内显示倒计时。
- **存储权限引导**：适配 Android 11+ 所有文件访问权限与旧版存储权限。

### 歌词系统

- **LRC 解析**：支持 `[mm:ss.xxx]`、`[mm:ss:xxx]`、`[mm:ss]` 等时间戳。
- **YRC 逐字歌词**：同时解析 YRC，并与 LRC 择优使用，避免只显示元数据。
- **翻译歌词**：自动合并翻译歌词，支持“原文 + 翻译”“仅翻译”“仅原文”。
- **实时高亮**：播放进度同步高亮当前行，平滑滚动。
- **点击跳转**：点击任意歌词行可跳转到对应时间。
- **歌词设置**：字号、对齐方式、翻译显示模式均可配置。
- **搜索歌词**：在歌词页内搜索网易云歌曲并替换当前歌词。
- **导出歌词**：支持导出 LRC 歌词文件。
- **桌面歌词**：支持浅色、深色、根据封面渐变三种悬浮歌词样式。
- **自动匹配**：当歌曲标题来自视频类音频时，可自动提取歌名、搜索网易云候选并打分匹配，匹配成功后缓存歌词。

### 音质与网络

- **多档音质**：标准、极高、无损、Hi-Res、高清环绕、沉浸环绕、杜比全景声、臻音全景声、超清母带。
- **沉浸声子类型**：`c51`、`ste`、`aac`。
- **音质兜底策略**：逐个后退、自动兼容、从最差向上、不回退固定。
- **音质学习**：根据播放结果学习可用音质，减少无效请求。
- **音质上限保护**：未解锁时播放 / 缓存 / 导出分别限制在可见上限，可在设置页解锁。
- **网络重试**：可设置重试次数与重试间隔。
- **伪装请求 IP**：默认关闭，可随机生成请求 IP，降低按 IP 限流影响，只用于防止限流目的，并做出一系列守护机制。
- **限流识别**：自动识别接口限流并给出提示；不同服务的限流状态相互独立，避免相互干扰。
- **签名与密钥缓存**：需要签名或临时密钥的接口会自动缓存密钥，并支持内存与磁盘兜底，减少重复请求。

### 频谱可视化

- **实时频谱**：通过 Media3 音频处理器采集 PCM 数据，使用 FFT 计算频谱。
- **三种频谱样式**：柱式、环式、块式。
- **频谱颜色**：支持 MD3 默认色与根据封面渐变取色。
- **显示条件**：仅在播放页、且封面大图为圆形时显示。
- **动画平滑**：带触发阈值、峰值衰减与冷却，避免频谱抖动。

### 图形均衡器

- **15 段图形均衡器**：基于 `DynamicsProcessing`，需 Android 9 及以上。
- **均衡器预设**：平坦、开发者自用、开发者自用 2，并支持自定义增益。
- **精调增益**：每段支持滑块与 +/- 步进按钮。
- **播放控件锁定**：进入均衡器页时暂停并锁定播放控件，退出后恢复。

### 搜索历史

- **最近 15 条记录**：保存关键词、搜索类型与搜索时间。
- **首屏结果缓存**：单曲搜索首屏结果可本地缓存，从历史进入时快速展示。
- **点击回搜**：点击历史记录可重新进入搜索结果页。
- **单条删除 / 清空历史**：长按删除单条，菜单可清空全部，并同步清理结果缓存。

### 界面与体验

- **Material 3**：基于 `Theme.Material3.DayNight.NoActionBar`。
- **深色模式**：支持跟随系统、浅色、深色。
- **播放页背景**：支持 MD3 背景、封面渐变背景、流光背景（根据 BBPlayer 设计灵感）。
- **迷你播放条样式**：默认 / 全播放条。
- **系统栏适配**：渐变与流光模式下状态栏、导航栏颜色与图标跟随背景。
- **封面形状**：支持 MD3 圆角与圆形；圆形时可开启缓慢旋转。
- **电池优化引导**：引导关闭省电优化，提升后台播放稳定性。
- **全局点击防抖**：减少误触与重复点击，并优化滑动后首次点击体验。
- **免责声明**：首次启动展示免责声明，按钮带倒计时确认。
- **悬浮窗权限校验**：启动与恢复时校验悬浮窗权限，避免 UI 状态与实际不一致。

## 技术栈

- **语言**：Java
- **UI**：AndroidX、Material Components for Android、RecyclerView、ConstraintLayout、TabLayout、Material 3
- **播放**：AndroidX Media3 ExoPlayer、MediaSessionService、Media3 OkHttp DataSource
- **音频处理**：Media3 BaseAudioProcessor、FFT、DynamicsProcessing（Android 9+）
- **网络**：OkHttp、自定义 JSON API Client、WBI 签名
- **图片**：自定义 ImageLoader + LruCache + 磁盘缓存，适配不同图片 CDN 的缩略语法与防盗链
- **存储**：SharedPreferences、内部缓存目录、SAF 文件选择器
- **异步**：ExecutorService、Handler、HandlerThread、Choreographer
- **歌词**：自定义 LrcParser，支持 LRC / YRC / 翻译合并
- **构建**：Gradle

## 项目结构

```text
app/src/main/java/com/gascy/grplayer/
├── MainActivity.java
├── SearchActivity.java
├── SearchDetailActivity.java
├── ArtistDetailActivity.java
├── PlaylistDetailActivity.java
├── FolderDetailActivity.java
├── PlayerActivity.java
├── LyricActivity.java
├── SettingsActivity.java
├── SettingsAppearanceActivity.java
├── SettingsPlaybackActivity.java
├── SettingsFloatingActivity.java
├── SettingsLyricActivity.java
├── SettingsNetworkActivity.java
├── SettingsSpectrumActivity.java
├── HistoryActivity.java
├── EqualizerActivity.java
├── BaseActivity.java
├── adapter/
├── data/
├── model/
├── net/
├── playback/
├── ui/
└── util/
```

资源目录：

```text
app/src/main/res/
├── layout/
├── drawable/
├── anim/
└── values/
```

核心模块说明：

- `net/`：API Client、签名工具、IP 伪装拦截器。
- `playback/`：PlayerManager、PlaybackService、频谱音频处理器。
- `ui/`：MiniPlayer、悬浮播放条、桌面歌词、流光背景、频谱 View。
- `data/`：收藏库、缓存、导出、歌词缓存、搜索历史、音质学习、均衡器、设置。
- `util/`：歌词解析、封面渐变、流光取色、歌词匹配、JSON 歌单、导出弹窗等。

## 构建与运行

1. 使用 Android Studio 打开项目。
2. 等待 Gradle 同步完成。
3. 连接 Android 设备或启动模拟器。
4. 运行应用。
5. 首次启动时按需授予通知、存储 / 所有文件访问、悬浮窗等权限。
6. 均衡器功能需要 Android 9 及以上系统。
7. 频谱功能需要在播放页将封面大图形状切换为圆形后开启。

## 配置说明

- 默认 API 地址位于 `ApiClient.BASE_URL`，如需使用自部署服务，修改该地址即可。
- 部分音频来源使用公开 Web API 并依赖签名或临时密钥，密钥会本地缓存，网络请求会携带相应来源所需的 Referer。
- “伪装请求 IP”默认关闭，请根据实际使用场景与相关服务条款谨慎开启，只用于防止限流目的，并做出一系列守护机制。
- 音质、兜底策略、重试次数、歌词、主题、播放页背景、频谱、悬浮窗等均可在设置页调整。
- 未解锁音质时，播放 / 缓存 / 导出会分别限制在可见音质上限，可在播放设置中解锁更多音质。
- 导出到本地默认每日最多 20 个文件，成功导出后有 60 秒冷却。
- 频谱仅圆形封面生效；频谱样式与颜色可在“设置 → 频谱设置”中调整。

## 隐私与数据

- 收藏夹、设置、缓存、搜索历史、歌词缓存、封面缓存等数据默认保存在本地。
- 本项目自身不包含用户画像、广告或主动上传个人数据的逻辑。
- 网络请求会发送至所配置的 API 服务与相关公开 API，请自行确认并是否使用。
- 伪装 IP 仅用于降低按 IP 维度限流影响，默认关闭，请遵守相关服务条款与法律法规。

## 版本历史

- 版本更新记录请查看 [Releases](https://github.com/Gascy37/grplayer-app/releases)。

## 致谢

感谢以下开源项目与生态：

- AndroidX
- Material Components for Android
- OkHttp
- AndroidX Media3
- AndroidIDE
- 以及所有为 Android 开源社区做出贡献的开发者

同时也感谢 [BBPlayer](https://github.com/bbplayer-app/BBPlayer) 同类音乐播放器项目带来的设计灵感。

## 开源许可

本项目采用 MIT 许可。详见 [LICENSE](./LICENSE)。
