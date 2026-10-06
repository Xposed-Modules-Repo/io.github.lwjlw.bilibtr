# BiliBTR

**Multi-CDN playback accelerator for the official Bilibili Android client.**
**为哔哩哔哩官方安卓客户端提供多 CDN 并发加速的 LSPosed 模块。**

[Download](https://github.com/Xposed-Modules-Repo/io.github.lwjlw.bilibtr/releases) · [Source](https://github.com/lwjlw/io.github.lwjlw.bilibtr) · [Issues](https://github.com/lwjlw/io.github.lwjlw.bilibtr/issues)

This repository is the **release repository** for the module. APKs are published under
[Releases](https://github.com/Xposed-Modules-Repo/io.github.lwjlw.bilibtr/releases).

---

## English

BiliBTR routes the media byte requests issued by the player through a local proxy, which
**picks faster CDN nodes, downloads in parallel and reads ahead**, then hands the bytes to
the player — **optimising only the bytes the user already has the right to access**. It
**cannot unlock any content**.

### Features

| Feature | Description |
| --- | --- |
| Multi-CDN node selection | Speed-tests every candidate node and uses the fastest measured |
| Concurrent connections | Splits one range request into parallel segments; concurrency adapts to the bitrate |
| Stream-as-you-fetch | Returns data as soon as upstream headers arrive, noticeably improving startup |
| Read-ahead cache | Prefetches ahead in the background so later requests hit memory directly |
| Connection pooling | Reuses CDN connections to cut per-request round-trip cost |
| Graceful degradation | Falls back to a single connection after consecutive failures, then recovers |

The bundled app provides a **speed panel**, **manual node pinning**,
**buffer size / duration tuning**, and a **floating 3x / 4x speed ball** on the player page.

### Requirements

| Item | Requirement |
| --- | --- |
| Android | 12 or newer (`minSdk 31`) |
| Framework | LSPosed (API 102) |
| Host app | Official Bilibili client (`tv.danmaku.bili`), verified on 9.8.0 |

### Installation

1. Download the APK from [Releases](https://github.com/Xposed-Modules-Repo/io.github.lwjlw.bilibtr/releases) and install it;
2. Enable **BiliBTR** in LSPosed Manager and tick the **Bilibili** scope;
3. Force-stop Bilibili and reopen it;
4. Open the **BiliBTR** app to configure.

> Applies to **on-demand playback only**; live streaming is untouched.
> 4K playback overseas is limited by **bandwidth**, not by the concurrency strategy.

---

## 中文

BiliBTR 把播放器发起的媒体字节请求接管到本机代理，由代理**挑选更快的 CDN 节点、并发拉取、
提前预读**，再把数据交给播放器 —— **只优化用户本来就有权访问的字节**，**不能解锁任何内容**。

### 功能

| 功能 | 说明 |
| --- | --- |
| 多 CDN 节点优选 | 测速全部候选节点，使用实测最快的 |
| 多连接并发 | 一个 Range 请求切成多段并行拉取，并发数按码率自动调整 |
| 边收边发 | 拿到上游响应头立刻回给播放器，显著加快起播 |
| 预读缓存 | 后台向前预读，后续请求直接命中内存 |
| 连接复用 | 到 CDN 的连接池复用，降低每个请求的往返开销 |
| 失败降级 | 连续失败自动暂停并发、走单连接，适时自动恢复 |

自带界面提供**测速面板**、**节点手动锁定**、**缓冲大小 / 缓冲时长调节**，
以及播放页的 **3x / 4x 倍速悬浮球**。

### 环境要求

| 项目 | 要求 |
| --- | --- |
| Android | 12 及以上（`minSdk 31`） |
| 框架 | LSPosed（API 102） |
| 宿主 | 哔哩哔哩官方客户端（`tv.danmaku.bili`），已验证 9.8.0 |

### 安装

1. 从 [Releases](https://github.com/Xposed-Modules-Repo/io.github.lwjlw.bilibtr/releases) 下载 APK 并安装；
2. 在 LSPosed 管理器中启用 **BiliBTR**，作用域勾选**哔哩哔哩**；
3. 强制停止哔哩哔哩后重新打开；
4. 打开 **BiliBTR** App 进行配置。

> 只作用于**点播**，直播未改；4K 在海外受**带宽**限制，并发策略只能缓解、不能突破。

---

## License / 开源与致谢

Released under the **GNU GPL v3**. Source and full documentation:
[lwjlw/io.github.lwjlw.bilibtr](https://github.com/lwjlw/io.github.lwjlw.bilibtr).

The concurrent range downloading principle and default parameters come from
[Bilibili-thread-ripper](https://github.com/MrTangLuyao/Bilibili-thread-ripper) (MIT);
the local-proxy architecture references
[PiliPlus, `btr` branch](https://github.com/nishuodedui1145-del/PiliPlus) (GPL-3.0).
Full third-party attributions:
[NOTICE.md](https://github.com/lwjlw/io.github.lwjlw.bilibtr/blob/main/NOTICE.md).

本项目采用 **GNU GPL v3**。并发下载的原理与默认参数参考
[Bilibili-thread-ripper](https://github.com/MrTangLuyao/Bilibili-thread-ripper)（MIT），
本地代理架构参考 [PiliPlus `btr` 分支](https://github.com/nishuodedui1145-del/PiliPlus)（GPL-3.0）。
第三方署名详见 [NOTICE.md](https://github.com/lwjlw/io.github.lwjlw.bilibtr/blob/main/NOTICE.md)。
