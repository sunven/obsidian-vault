## 环境

https://reactnative.dev/docs/environment-setup

AGP Android Gradle Plugin

NDK
### Gradle

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

## 问题

Exception in thread "main" java.io.IOException: Downloading from https://services.gradle.org/distributions/gradle-8.3-all.zip failed: timeout (10000ms)

解决： https://blog.csdn.net/weixin_39278265/article/details/114001472

Unrecognized VM option 'MaxPermSize=1024m'
jdk版本

Major Versio
https://mkyong.com/java/list-of-java-class-file-major-version-numbers/