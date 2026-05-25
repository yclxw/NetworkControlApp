# 红果断网 (BlockRedFruit)

基于 Android VPN Service API 的应用网络拦截工具。自动识别并阻断指定应用
的网络访问，适用于家长控制、应用管理、数字健康等场景。

## 功能特性

- 自动扫描设备中名称包含关键字的第三方应用
- 一键启用/停止 VPN 拦截，操作简单
- 前台服务常驻通知，拦截状态一目了然
- 实时监听应用安装/卸载，拦截规则自动更新
- 轻量架构，无第三方联网依赖

## 快速开始

### 环境要求

- **Android Studio** Meerkat (2024.3.1) 或更高版本
- **JDK** 21 (JetBrains Runtime jbr-21)
- **Android SDK** API 35
- **Gradle** 8.13
- **Kotlin** 2.0.0

### 克隆仓库

```sh
git clone <repo-url>
cd BlockRedFruit
```

### 构建与安装

**方式一：Android Studio**

1. 用 Android Studio 打开项目根目录。
2. 等待 Gradle 同步完成。
3. 连接 Android 设备或启动模拟器（API ≥ 24）。
4. 点击 `Run 'app'`。

**方式二：命令行**

```sh
# Debug 构建
./gradlew assembleDebug

# Release 构建（已启用混淆优化）
./gradlew assembleRelease
```

APK 输出路径：`app/build/outputs/apk/`

### 使用说明

1. 安装 APK 后启动「红果断网」。
2. 应用自动扫描并列出名称中包含「红果」的应用。
3. 点击 **启用断网** 开关。
4. 首次使用需授予通知权限（Android 13+）和 VPN 权限。
5. 开关打开后，目标应用的所有网络流量被阻断。
6. 关闭开关即可恢复网络。

## 目录结构

```
BlockRedFruit/
├── app/                          # 应用模块
│   ├── build.gradle.kts          # 应用构建配置
│   ├── proguard-rules.pro        # 混淆规则
│   └── src/main/
│       ├── AndroidManifest.xml   # 清单文件
│       ├── java/.../
│       │   ├── MainActivity.kt       # 主界面
│       │   ├── BlockVpnService.kt    # VPN 拦截服务
│       │   ├── AppScanner.kt         # 应用扫描器
│       │   └── AppListAdapter.kt     # 列表适配器
│       └── res/                  # 资源文件
├── bak/                          # 备份归档
├── docs/                         # 项目文档
│   ├── BACKUP.md                 # 备份规范
│   ├── VERSION.md                # 版本规范
│   └── CHANGELOG.md              # 更新日志
├── gradle/                       # Gradle Wrapper
├── build.gradle.kts              # 根构建脚本
├── settings.gradle.kts           # 项目设置
└── gradle.properties             # Gradle 属性
```

## 开发环境

### 开发软件

| 工具 | 版本 | 用途 |
|------|------|------|
| Android Studio | Meerkat 2024.3.1 | IDE |
| JDK (JetBrains Runtime) | 21 (jbr-21) | 编译与运行 |
| Gradle | 8.13 | 构建系统 |
| Android Gradle Plugin | 8.13.0 | Android 构建 |
| Kotlin | 2.0.0 | 开发语言 |
| Android SDK | API 35 | 目标平台 |

### Maven 镜像

项目配置了阿里云 Maven 镜像以加速依赖下载：

- `https://maven.aliyun.com/repository/google`
- `https://maven.aliyun.com/repository/public`
- `https://maven.aliyun.com/repository/gradle-plugin`

### AI 辅助开发

本项目在开发过程中使用了以下大语言模型（LLM）辅助编码：

| 模型 | 用途 |
|------|------|
| Claude Code (DeepSeek-V4-Pro) | 代码生成、架构设计、文档编写 |
| Claude Opus 4.7 / Sonnet 4.6 | 需求分析、代码审查、问题排查 |

## 许可证

本项目仅供学习与个人使用。使用者应遵守所在地法律法规，不得将本工具
用于非法目的。

## 贡献

欢迎提交 Issue 与 Pull Request。请确保：

1. 代码风格与现有代码保持一致（Kotlin 官方风格）
2. 新功能须在 Android 7.0 ~ 15 设备上测试通过
3. 文档同步更新（CHANGELOG、README 等）

## 相关文档

- [备份规范](docs/BACKUP.md)
- [版本规范](docs/VERSION.md)
- [更新日志](docs/CHANGELOG.md)
