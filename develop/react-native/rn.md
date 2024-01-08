## 环境

https://reactnative.dev/docs/environment-setup

gradle代理：

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
