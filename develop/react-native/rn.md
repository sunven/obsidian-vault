## 环境

https://reactnative.dev/docs/environment-setup

## AGP（Android Gradle Plugin）

AGP 在 Android 开发中，通常指的是 Android Gradle 插件。这是一个用于 Android 项目的 Gradle 插件，它提供了一系列功能，使得 Android 开发者可以使用 Gradle 来自动化和管理他们的构建过程。
Android Gradle 插件提供了许多功能，包括自动化项目构建、依赖管理、APK包的生成、多渠道打包、编译和测试等。同时，AGP 还支持自定义的构建类型和产品风味，允许开发者很方便地管理和控制他们的项目。
在你的 Android 项目的 `build.gradle` 文件中，你通常会看到这样的代码：`apply plugin: 'com.android.application'`，这就是在应用 Android Gradle 插件。并且，在项目的根 `build.gradle` 文件中，通常会包含对 AGP 版本的定义，例如：`classpath 'com.android.tools.build:gradle:4.0.1'`。

## NDK (Native Development Kit)
它是一种工具集，使得 Android 开发者能够使用 C 和 C++ 对部分应用进行 native (即运行在底层的) 编程，这样可以提高应用的性能，特别是对计算密集型应用来说，使用 NDK 开发可以提高运行效率。

```bash
ndk {
  abiFilters 'armeabi-v7a', 'arm64-v8a', 'x86_64', 'x86' 
}
```
```
## ABI (Application Binary Interface)
这是一种规定了二进制应用如何使用系统资源和调用系统服务的标准或者协议。每种 CPU 或架构类型都有对应的 ABI。在 Android NDK 开发中，ABI 决定了你的应用在哪种类型的设备上运行。比如 'armeabi' 表示你的应用可以在使用 ARM v7 架构的设备上运行，'x86' 则表示你的应用可以在使用 x86 架构的设备上运行

## ADB（Android Debug Bridge）

```text
%ANDROID_HOME%\tools
%ANDROID_HOME%\platform-tools
```
## Gradle

https://docs.gradle.org/current/userguide/compatibility.html

构建工具，处理 Android 端的构建系统

1. 编译打包：Gradle 能根据项目配置编译打包 Android 应用，生成 APK（Android 应用包）或 AAB（Android App Bundle）文件供发布。
2. 依赖管理：使用 Gradle 可以自动化地管理项目的库依赖，例如从 Maven 中心库自动下载和引入依赖库。
3. 多渠道打包：Gradle 可以配置文件进行多渠道打包，比如可以生成不同版本的 APK 文件，以适应不同的发布渠道。
4. 自定义构建行为：Gradle 支持开发者通过编写自定义脚本去控制构建过程中的每一步，使得构建更加亲和个性化需求

**代理：**

android/gradle.properties
https://docs.gradle.org/current/userguide/build_environment.html#sec:gradle_system_properties

```
# proxy
systemProp.http.proxyHost=127.0.0.1
systemProp.http.proxyPort=7890
systemProp.https.proxyHost=127.0.0.1
systemProp.https.proxyPort=7890
```

- amd 虚拟化 hyper-v
- 运行起来报错，可以尝试用android studio打开，会装一些依赖，环境。。。
- 查看环境变量：`Get-ChildItem -Path Env:\`

## Kotli

- 是一个基于JVM 的新的编程语言，由 JetBrains 开发
- 可以编译成Java字节码，也可以编译成JavaScript，方便在没有JVM的设备上运行
- 已正式成为Android官方支持开发语言

kotlin jvm compatibility

https://kotlinlang.org/docs/faq.html#which-versions-of-jvm-does-kotlin-target

## 问题

Exception in thread "main" java.io.IOException: Downloading from https://services.gradle.org/distributions/gradle-8.3-all.zip failed: timeout (10000ms)

解决： https://blog.csdn.net/weixin_39278265/article/details/114001472

Unrecognized VM option 'MaxPermSize=1024m'
jdk版本

Major Versio
https://mkyong.com/java/list-of-java-class-file-major-version-numbers/

Build Output 乱码

Android Studio的Help–>Edit Custom VM Options
-Dfile.encoding=UTF-8


自动链接不生效

https://github.com/react-native-community/cli/blob/main/docs/autolinking.md#example-1
https://github.com/facebook/react-native/issues/25787

yarn react-native run-android 自动生成PackageList

## enable reload

Ctrl + M
**adb shell input keyevent 82**