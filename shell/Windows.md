记录Windwos下，cmd，PowerShell命令
## 包管理：
https://chocolatey.org/install#individual


**查看环境变量：**
powershell 中的变量只存在于 powershell 内部的会话中，一旦 powershell 关闭，这些变量就会自生自灭。但是如果环境变量被更新了，它会继续保存在操作系统中，即使其它程序也可以调用它

```powershell
## 列出所有环境变量
Get-ChildItem -Path Env:\
ls env:
## 读取某个环境变量
$env:windir
## 设置某个环境变量
$env:TestVar1="This is my environment variable"
## 删除某个环境变量
del env:windir
```

查看占用端口：`netstat -ano | findstr 3306`
查看 PID 对应的进程：`tasklist|findstr "12448"`

## win11 右键菜单

```sh
# 经典
reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve

# 默认
reg.exe delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /va /f

# 重启
taskkill /f /im explorer.exe & start explorer.exe
```
