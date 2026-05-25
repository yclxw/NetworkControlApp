# 更新日志

本项目遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 规范。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，
版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/) 与项目 [版本规范](VERSION.md)。

## [v1.0.20260524] — 2026-05-24

### 新增

- 首次正式发布：**红果断网** Android 应用。
- 基于 Android VPN Service API 实现应用网络拦截。
- 自动扫描设备上名称包含「红果」的已安装应用。
- 主界面展示目标应用列表（应用名 + 包名）。
- Switch 开关一键启用/停止 VPN 拦截服务。
- 前台通知常驻，实时显示当前拦截的应用数量。
- 动态监听应用安装/卸载/更新，自动刷新 VPN 规则。
- 红色主题 Material Design 界面。
- 自适应图标（Adaptive Icon）。

### 技术栈

- **语言：** Kotlin 2.0.0
- **构建：** Gradle 8.13 + Android Gradle Plugin 8.13.0
- **最低支持：** Android 7.0 (API 24)
- **目标平台：** Android 15 (API 35)
- **UI 框架：** Android Views + ViewBinding
- **架构：** 单 Activity + VPN Service + RecyclerView

### 已知限制

- 仅拦截名称精确包含「红果」二字的应用（区分大小写）。
- VPN 开启期间不转发流量，仅丢弃，目标应用完全断网。
- 不支持按包名自定义黑白名单。
