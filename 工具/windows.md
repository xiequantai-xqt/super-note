# 开机自启动怎么设置

## windows系统

![](https://guiwanzhyq.oss-cn-hangzhou.aliyuncs.com/hc/img/20240821/f3d1beae-f1c6-4547-9421-492767e44c28.png)

使用“启动”文件夹：

- 打开文件资源管理器。
- 在地址栏中输入以下路径（取决于你的Windows版本和用户账户）：
  - `%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup` （适用于大多数情况）
  - `C:\Users\[Username]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup` （如果你需要完整路径）
- 将目标程序的快捷方式或可执行文件拖到这个文件夹里。

## macOS系统

使用“登录项”：

- 打开“系统偏好设置”。
- 选择“用户与群组”。
- 点击“登录项”标签页。
- 选中你的用户账户，点击加号（+），浏览并选择你想在登录时自动启动的应用程序。

注意事项：

- 请确保你有足够的权限来更改这些设置。
- 过多的应用程序设置为开机启动可能会导致系统启动变慢。
- 对于安全起见，在修改任何系统设置之前，最好先备份重要数据。

![](https://front-end-files.oss-cn-shenzhen.aliyuncs.com/node%E5%AD%A6%E4%B9%A0/0a07219e-762a-4865-8e01-0b798db6610d.jpg)