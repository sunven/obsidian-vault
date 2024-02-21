# intro

## Install

https://docs.flutter.dev/get-started/install

mirror: https://flutter.cn/community/china

- `D:\flutter`

## env

```ps1
[System.Environment]::SetEnvironmentVariable('PUB_HOSTED_URL', 'https://pub.flutter-io.cn', [System.EnvironmentVariableTarget]::User)
[System.Environment]::SetEnvironmentVariable('FLUTTER_STORAGE_BASE_URL', 'https://storage.flutter-io.cn', [System.EnvironmentVariableTarget]::User)
```

const String kMaven = 'https://maven.aliyun.com/repository/public/';
## Troubleshooting

代理：
https://blog.csdn.net/qianxiamuxin/article/details/134322224
```text
distributionUrl=https\://mirrors.cloud.tencent.com/gradle/gradle-7.5-all.zip
```
https://mirrors.cloud.tencent.com/gradle/

```
maven { url 'https://maven.aliyun.com/repository/google' }
maven { url 'https://maven.aliyun.com/repository/jcenter' }
maven { url 'https://maven.aliyun.com/nexus/content/groups/public' }
```

**Exception in thread "main" java.util.zip.ZipException: zip END header not found**
删除 ~ 目录下 .gradle 文件夹
https://github.com/flutter/flutter/issues/73852

## FVM

https://fvm.app/

```ps
choco install fvm

# 全局执行，相当于缓存
fvm install 2.5.0
# 项目根目录执行。创建.fvm文件夹
fvm use 2.2.3
# 全局flutter版本
fvm global 2.5.0
```

flutter xxx 使用 fvm flutter xxx 代替

### vs code

在 vscode 控制面板中执行 Flutter: Change SDK 切换 Flutter SDK 版本，
将同步记录到当前项目的 vscode 配置文件 .vscode/settings.json 中（dart.flutterSdkPath）