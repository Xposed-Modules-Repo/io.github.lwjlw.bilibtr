# BiliBTR

为哔哩哔哩官方安卓客户端提供多 CDN 并发加速的 LSPosed 模块。

[下载](https://github.com/Xposed-Modules-Repo/io.github.lwjlw.bilibtr/releases) · [源码](https://github.com/lwjlw/io.github.lwjlw.bilibtr) · [问题反馈](https://github.com/lwjlw/io.github.lwjlw.bilibtr/issues)

本仓库为模块的**发布仓库**，APK 见 [Releases](https://github.com/Xposed-Modules-Repo/io.github.lwjlw.bilibtr/releases)。

## 功能

**网络加速**

| 功能 | 说明 |
| --- | --- |
| 多 CDN 节点优选 | 测速全部候选节点，使用实测最快的 |
| 多连接并发 | 一个 Range 请求切成多段并行拉取，并发数按码率自动调整 |
| 边收边发 | 拿到上游响应头立刻回给播放器，显著加快起播 |
| 预读缓存 | 后台向前预读，后续请求直接命中内存 |
| 连接复用 | 到 CDN 的连接池复用，降低每个请求的往返开销 |
| 失败降级 | 连续失败自动暂停并发、走单连接，适时自动恢复 |

**设置界面**

- **测速面板**：实时显示吞吐、卡顿次数、并发数、首字节时间、各节点实际用量
- **节点管理**：一键对全部候选节点测速，可点击切换或保持自动
- **缓冲调节**：缓冲大小 / 缓冲时长手动调节
- **播放页悬浮球**：3x / 4x 倍速（官方客户端没有），无操作自动隐藏

## 环境要求

| 项目 | 要求 |
| --- | --- |
| Android | 12 及以上（`minSdk 31`） |
| 框架 | LSPosed（API 102） |
| 宿主 | 哔哩哔哩官方客户端（`tv.danmaku.bili`），已验证 9.8.0 |

模块**不会**申请悬浮窗权限。

## 安装

1. 从 [Releases](https://github.com/Xposed-Modules-Repo/io.github.lwjlw.bilibtr/releases) 下载 APK 并安装；
2. 在 LSPosed 管理器中启用 **BiliBTR**，作用域勾选**哔哩哔哩**；
3. 强制停止哔哩哔哩后重新打开；
4. 打开 **BiliBTR** App 进行配置。

## 说明

- 本模块**不能解锁任何内容**，只是优化用户本来就有权访问的字节传输；
- 只作用于**点播**，直播未改；
- 4K 等高位率在海外受**带宽**限制，并发策略只能缓解、不能突破。

完整文档见[源码仓库](https://github.com/lwjlw/io.github.lwjlw.bilibtr)。

## 开源与致谢

BiliBTR 使用 [GNU GPL v3 许可证](https://github.com/lwjlw/io.github.lwjlw.bilibtr/blob/main/LICENSE)。

并发下载的原理与默认参数参考 [Bilibili-thread-ripper](https://github.com/MrTangLuyao/Bilibili-thread-ripper)（MIT），
本地代理架构参考 [PiliPlus `btr` 分支](https://github.com/nishuodedui1145-del/PiliPlus)（GPL-3.0）。
第三方署名详见[源码仓库的 NOTICE](https://github.com/lwjlw/io.github.lwjlw.bilibtr/blob/main/NOTICE.md)。
