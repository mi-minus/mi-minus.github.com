---
layout: life
title: JetBrain_Tools
category: Tools
duoshuo: true
date: 2017-05-23
---

    作者: mr zhao
    编辑: minus
    日期: 2017-05-23
    邮箱: minus@stu.xjtu.edu.cn


<!-- more -->


### 简述－[JetBrain](https://www.jetbrains.com)
```
JetBrains公司,最好的Java IDE的创造者,特别是IntelliJ Idea这款java工具，其他我们可能会常用的工具有 WebStorm for Js, PyCharm for python,这都是一个系列的，当然还包含其他类似的开发工具，这里就暂时不提了. 本博客主要是讲解 IntelliJ Idea for Java
```

### Idea基本信息-安装

```
1. 分为两个版本：Community（社区版）、Ultimate（旗舰版），我们直接下载旗舰版（相比社区版有更多、更强的功能）
3. 不需要安装，只需要解压运行即可
4. 启动命令：IDEA目录/bin/idea.sh
5. 创建桌面图标:Wevlcome界面-->Configure-->Create Desktop Entry，勾选for all users ,创建后图标位于/use/share/applications目录下，复制到桌面
```

### [内存优化](http://blog.oneapm.com/apm-tech/426.html)
```
* 编辑Idea安装目录下：bin/idea.vmoptions，并添加如下内容：
    -Xms1024m （修改）
    -Xmx4096m	（修改）
    -XX:ReservedCodeCacheSize=1024m	（修改）
    -XX:+UseCompressedOops   （新增） 压缩指针
```

### 操作主界面部分选项分析
```
 * File->Settings : 只对当前的project有效
 * File->OSettings : 只对当前的project有效
 * File->Other Settings -> Default Settings : 全局有效
```
```
 * 设置不折叠空包: Disable "Compact Empty Middle Package" option in the "project view"
 * 显示行数和方法线: "Settings" -> "Editor" -> "General" -> "Appearance"
 * 设置花括号换行: "Settings" -> "Editor" -> "Code Style" -> "Java" -> "Braces placement" -> 三项均改为"Next line"
 * 代码提示不区分大小写: "Settings" -> "Editor" -> "General" -> "Code Completion" -> "Case sensitive completion" 选为 “ALL“
 * 自动导包: "Settings" -> "Editor" -> "General" -> "Auto Import" -> 选中 Optimize imports on the fly/ Add unambiguous imports on the fly 
 * 修改 ctrl+D 为复制所选行数完整内容: "Settings" -> "Keymaps" -> 取消 "Duplicate Line or Selection" / 选中 "Duplicate Entire Lines"为Ctrl+D 
 * 设置Tab多行显示: "Settings" -> "Editor" -> "Greneral" -> "Editor Tabs" -> 取消 "Show tabs in single row" && "Tab limit" 设置为 10等
 * ctrl +e 记录文件的个数: "Settings" -> "Editor" -> "General" ->> "Limits" -> "Recent files limit" 设置为50
 * 设置断点条件: 在断点上点击右键，条件为真的时会启动此断点
 * 对代码进行垂直 和 水平 分组: "Split Vertically"  "Split Horizontally"
 * 设置Ctrl + 滚动缩放字体和图片: "Settings" -> "Editor" -> "General" -> 选中 "Change font size(Zoom) with Ctrl+Mouse Wheel"
 * Rest Client: "Tools" -> "Test Restful Web Service" 
```

### 查询快捷键

| 快捷键                      | 作用               | 
| -------------              |:-------------:    |
|  Double SHIFT              | Search EveryWhere               |
|  Ctrl + N                  | 查找类 |
|  Ctrl + Shift + N          | 查找文件 |
|  Ctrl + Shift + ALT + N    | 查找类中的方法或变量 |
|  Ctrl + B                  | 寻找变量来源        |
|  Ctrl + G                  | 定位行             |
|  Ctrl + R                  | 在当前窗口替换文本   |
|  Ctrl + F                  | 在当前窗口查找文本  |
|  Alt + Shift + C           | 查找修改的文件               |
|  F3                        | 向下查找关键字出现位置        |
|  Shift + F3                | 向上查找关键字出现位置       |
|  F4                        | 查找变量来源  等价于 ctrl+鼠标左键|
|  Ctrl + Shift + F          | 项目中全局查找文本内容|

### Running快捷键

| 快捷键                      | 作用               | 
| -------------              |:-------------:    |
|  ALT + SHIFT + F10         | 选择并运行 |
|  ALT + SHIFT + F9          | 选择并使用Debug模式运行 |
|  Shift + F10               | 运行              |
|  Shift + F9                | Debug模式运行      |
|  Ctrl + Shift + F10        | Run context configuration from editor |
|  Ctrl + Shift + F9         | 编译选中的文件／包／模块           |
|  Ctrl + R                  | 在当前窗口替换文本   |
|  Ctrl + F                  | 在当前窗口查找文本  |
|  Ctrl + Shift + R          | 在指定窗口替换文本   |

### Debugging快捷键

| 快捷键                      | 作用               | 
| -------------              |:-------------:    |
|  F8         | step over不进入函数 |
|  F7         | step into 单步执行 |
|  Shift + F7 | Smart step into 智能单步执行,可选择步入的方法|
|  Shift + F8 | Step out 跳出      |
|  ALT+F9     | Run to cursor 运行到光标处 |
|  ALT+F8     | Evaluate expression 表达计算|
|  F9         | Resume program 恢复程序运行、跳到下个断点   |
|  CTRL+F8    | Toggle breakpoint 添加或取消断点   |
|  CTRL+SHIFT+F8  | View breakpoints 查看断点  |
|  Ctrl + Shift + R          | 在指定窗口替换文本   |]

### 代码 快捷键

| 快捷键                      | 作用               | 
| -------------              |:-------------:    |
|  ALT+回车    | 导入包,自动修正 （最特殊的快捷键，不同情况下弹出的菜单完全不同） |
|  CTRL+ALT+L | 格式化代码 |
|  CTRL+ALT+I | 自动缩进 |
|  CTRL+ALT+O | 优化导入的类和包|
|  ALT+INSERT   | 生成代码(如GET,SET方法,构造函数等) |
|  CTRL+SHIFT+SPACE | 自动补全代码 |
|  CTRL+空格   | 代码提示 |
|  CTRL+ALT+SPACE  | 类 名或接口名提示|
|  CTRL+P      | 方法参数提示|
|  CTRL+J     | 自动代码 |
|  CTRL+ALT+T | 把选中的代码放在 TRY{} IF{} ELSE{} 里 |

### 复制粘贴 快捷键

| 快捷键                      | 作用               | 
| -------------              |:-------------:    |
|  F5         | 拷贝文件 |
|  CTRL+D     | 复制行或所选内容 |
|  CTRL+X     | 剪切 |
|  CTRL+Y     | 删除行或所选行  |
|  CTRL+SHIFT+V | 可以选择复制的历史记录  |

### 常用插件

| 快捷键                      | 作用               | 
| -------------              |:-------------:    |
|  Key promoter| 快捷键提示 |
|  IDETalk     | 一般用于局域网通信，分享代码、错误、代码对比 |
|  SoapUI Intellij Plugin  | 测试WebService |
|  CodeGlance  | 代码右侧显示缩略图|
|  Easy-Translation | 翻译（ALT+A）  |
|  CheckStyle-IDEA  | 代码规范检查  |
|  FindBugs-IDEA    | 静态代码分析  |
|  Statistic        | 代码统计     |
|  Ideavim          | vim编辑模式  |
