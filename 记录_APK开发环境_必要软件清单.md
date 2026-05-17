# APK 开发环境 · 必要软件清单

> 生成日期：2026-05-16

---

## 安装顺序总览

```
① JDK 21        ──  编译 Java/Kotlin 源码
② Android Studio ──  IDE + SDK Manager
③ Android SDK    ──  平台、构建工具、adb
④ Gradle 8.13   ──  构建系统
⑤ 项目级依赖    ──  AGP / Kotlin / 库（自动下载）
⑥ 网络镜像      ──  仓库加速配置
```

以下按此顺序展开。

---

## ① JDK 21（Java 开发工具包）

**安装顺序：第 1 位**——所有构建工具依赖 JDK，必须先装。

| 项 | 值 |
|---|---|
| **版本** | JDK 21 LTS（Temurin / Adoptium） |
| **本地路径** | `C:\DStui\jdk-21\jdk-21.0.11+10` |
| **gradle.properties 配置** | `org.gradle.java.home=C\:\\DStui\\jdk-21\\jdk-21.0.11+10` |
| **建议** | 锁定 JDK 21 最稳定，Java 25/23/22 与旧版 Gradle ASM 不兼容 |

**下载地址：**

| 来源 | 链接 |
|------|------|
| 官方主页 | https://adoptium.net/temurin/releases/?version=21 |
| ZIP 包（推荐） | https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.11%2B10/OpenJDK21U-jdk_x64_windows_hotspot_21.0.11_10.zip |
| MSI 安装包 | https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.11%2B10/OpenJDK21U-jdk_x64_windows_hotspot_21.0.11_10.msi |

> ZIP 包下载后解压即用，无需安装；配置 `JAVA_HOME` 或直接在 `gradle.properties` 中指定路径。

---

## ② Android Studio（IDE）

**安装顺序：第 2 位**——自带 SDK Manager，安装后即可管理 SDK 组件。

| 项 | 值 |
|---|---|
| **版本** | Android Studio（最新稳定版） |
| **本地安装包** | `C:\DStui\android-studio-panda4-patch1-windows.exe` |

**下载地址：**

| 来源 | 链接 |
|------|------|
| 官方（国际） | https://developer.android.com/studio |
| 官方（国内镜像） | https://developer.android.google.cn/studio |

> 也可不装 IDE，仅安装 Command Line Tools 后用 `sdkmanager` 管理 SDK + 文本编辑器写代码。

---

## ③ Android SDK

**安装顺序：第 3 位**——通过 Android Studio 的 SDK Manager 或 `sdkmanager` 命令行安装。

| 项 | 值 |
|---|---|
| **SDK 路径** | `C:\Users\h1734\AppData\Local\Android\Sdk`（记录于 `local.properties`） |
| **平台版本** | compileSdk / targetSdk = **35** |
| **最低支持** | minSdk = **24** |

**SDK Manager 需安装的组件：**

```
platforms;android-35           # SDK 平台（必须）
build-tools;35.0.0             # 构建工具（必须）
platform-tools                 # adb（必须，安装 APK 用）
cmdline-tools;latest           # sdkmanager 命令行（可选，无 IDE 时用）
```

**安装命令（使用 sdkmanager）：**
```bat
sdkmanager "platforms;android-35" "build-tools;35.0.0" "platform-tools"
```

**安装 APK 命令：**
```bat
adb install app\build\outputs\apk\debug\app-debug.apk
```

---

## ④ Gradle 8.13（构建系统）

**安装顺序：第 4 位**——JDK + SDK 就绪后安装 Gradle。

| 项 | 值 |
|---|---|
| **版本** | **Gradle 8.13** |
| **本地路径** | `C:\DStui\gradle-8.13\gradle-8.13\` |
| **说明** | 项目目录中的 `gradle-8.6` 已废弃（ASM 不支持 Java 25），始终用 8.13 |

**下载地址：**

| 来源 | 链接 |
|------|------|
| 官方主页 | https://gradle.org/releases/ |
| 官方直链 | https://services.gradle.org/distributions/gradle-8.13-bin.zip |
| 腾讯云镜像（国内快） | https://mirrors.cloud.tencent.com/gradle/gradle-8.13-bin.zip |
| Gradle Wrapper 配置 | `gradle/wrapper/gradle-wrapper.properties` 已配置腾讯云镜像 |

> ZIP 包下载后解压即用。也可由 Gradle Wrapper 自动下载（第一次构建时触发）。

**构建命令：**
```bat
C:\DStui\gradle-8.13\gradle-8.13\bin\gradle.bat ^
  -p C:\DStui\BlockRedFruit assembleDebug --no-daemon
```

**输出位置：** `app/build/outputs/apk/debug/app-debug.apk`

---

## ⑤ 项目级依赖（自动下载）

**安装顺序：第 5 位**——Gradle 构建时自动从 Maven 仓库下载，无需手动操作。

| 依赖 | 版本 | 说明 |
|------|------|------|
| **AGP（Android Gradle Plugin）** | **8.13.0** | `com.android.application`，与 Gradle 8.13 配套 |
| **Kotlin 编译器** | **2.0.0** | `org.jetbrains.kotlin.android`，Gradle 插件管理 |
| AndroidX Core KTX | 1.13.1 | Android 核心库 |
| AppCompat | 1.7.0 | 兼容性支持 |
| Material Components | 1.12.0 | Material Design 组件 |
| ConstraintLayout | 2.1.4 | 布局 |
| Lifecycle Runtime KTX | 2.8.3 | 生命周期管理 |
| Lifecycle ViewModel KTX | 2.8.3 | ViewModel 支持 |

---

## ⑥ 网络镜像配置（国内必需）

**安装顺序：第 6 位**——构建前配置好镜像，否则依赖下载会超时失败。

**Gradle 发行版镜像**（编辑 `gradle/wrapper/gradle-wrapper.properties`）：
```properties
distributionUrl=https\://mirrors.cloud.tencent.com/gradle/gradle-8.13-bin.zip
```

**Maven 仓库镜像**（编辑 `settings.gradle.kts`）：
```kotlin
maven { url = uri("https://maven.aliyun.com/repository/google") }
maven { url = uri("https://maven.aliyun.com/repository/public") }
maven { url = uri("https://maven.aliyun.com/repository/gradle-plugin") }
```

---

## 附录：文件与配置索引

| 用途 | 文件路径 |
|------|----------|
| JDK 路径 | `gradle.properties` → `org.gradle.java.home` |
| SDK 路径 | `local.properties` → `sdk.dir` |
| Gradle 仓库镜像 | `settings.gradle.kts` → `pluginManagement.repositories` |
| Gradle 分发镜像 | `gradle/wrapper/gradle-wrapper.properties` → `distributionUrl` |
| 依赖版本声明 | `app/build.gradle.kts` → `dependencies` |
| AGP 版本声明 | `build.gradle.kts`（根）→ `plugins` |
| Kotlin 版本声明 | `build.gradle.kts`（根）→ `plugins` |
