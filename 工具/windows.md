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

# 实现在资源管理器空白处添加.md文件

可以通过修改注册表的免费方式在资源管理器中右键添加.md 文件，以下是具体步骤：

1. **打开注册表编辑器**：按下`Win + R`组合键，在弹出的 “运行” 对话框中输入`regedit`，然后回车，打开 “注册表编辑器”。
2. **创建`.md`项**：在注册表编辑器中，定位到`HKEY_CLASSES_ROOT`。右键点击`HKEY_CLASSES_ROOT`，选择 “新建”-“项”，命名为`.md`。
3. **设置默认值**：选中新建的`.md`项，在右侧窗口中，双击`(默认)`，将 “数值数据” 设置为`MarkdownFile`（名称可自定义，但后续步骤需保持一致）。
4. **创建`ShellNew`子项**：右键点击`.md`项，选择 “新建”-“项”，命名为`ShellNew`。
5. **添加`NullFile`值**：选中`ShellNew`项，在右侧窗口中，右键点击空白处，选择 “新建”-“字符串值”，命名为`NullFile`，其 “数值数据” 保持为空。
6. **关联 Markdown 编辑器（可选）**：若要指定特定的 Markdown 编辑器打开新建的 Markdown 文件，需进一步修改注册表。在`HKEY_CLASSES_ROOT`下创建`MarkdownFile`项（与第 3 步设置的默认值一致），然后在右侧窗口中，双击`(默认)`，将 “数值数据” 设置为你想要的 Markdown 编辑器的描述。接着在`MarkdownFile`项下创建`shell`子项，再在`shell`项下创建`open`子项，最后在`open`项下创建`command`子项。选中`command`项，在右侧窗口将`(默认)`的 “数值数据” 设置为 Markdown 编辑器的完整路径加上`%1`（例如`C:\Program Files\Typora\Typora.exe %1`，路径需根据实际安装情况修改）。
7. **应用更改**：更改完成后，可能需要重启资源管理器或重新启动计算机以使更改生效。

主要注意的是第六步，先写一个不常用的md编辑器，然后打开文件的时候默认Typora。这样就可以解决文件名有特殊符号无法打开的问题。

> 下面是几张参考图片，图片有可能会丢失，不过不重要

![](https://educt-files.oss-cn-shenzhen.aliyuncs.com/09fb8770-37a7-4a8e-b4d7-b6757977f7b5.png)

![](https://educt-files.oss-cn-shenzhen.aliyuncs.com/698e5b4b-5a0d-4ac4-b801-0dbbb3adc209.png)

![](https://educt-files.oss-cn-shenzhen.aliyuncs.com/bf6aa4bc-ddc5-4a5a-a931-36a4e2fca07b.png)