---
layout: life
title: linux Vim Tools介绍
category: linux学习
date: 2017-05-16
---

    作者: minus
    时间: 2017-05-23
    版本: V0.0.1
    mail: minus@stu.xjtu.edu.cn


<!-- more -->
### 强大终端工具一：[terminator](http://terminator-gtk3.readthedocs.io/en/latest/)
0. 简介:[官方使用教程](http://terminator-gtk3.readthedocs.io/en/latest/)
```
    Terminator 就可以完美地实现了在 Ubuntu在同一窗口中启动多个终端，并且可以自由的在一个窗口中分割区域建立新终端，还可以通过鼠标拉伸调整每个终端的大小
```

1. 安装／卸载
```sh
sudo apt-get install terminator 
```

2. 快捷键

| 快捷键                      | 作用               | 
| -------------              |:-------------:    |
|  ctrl + shift + x        | 小屏切换全屏               |
|  ctrl + shift + z        | 小屏切换全屏(文字屏幕大小比不变) |
|  ctrl + shift + e        | 水平分屏                  |
|  ctrl + shift + o        | 竖直分屏                  |
|  ctrl + pagedown         | 跳转到下一个tab            |
|  ctrl + pageup           | 跳转到上一个tab             |
|  ctrl + shift + pagedown/pageup   | 移动tab间的顺序    |
|  f11                     | 完全全屏                   |
|  ctrl + shift + w        | 关闭当前屏                 |
|  alt + 上下左右           | tab 之间进行转换            |
|  ctrl + shift + 上下左右  | 对当前窗口上下左右边移动放大   |
|  alt + a                 | Broadall on               |
|  alt + o                 | Broadall off              |
|  Ctrl+Shift+C            | copy                      |
|  Ctrl+Shift+V            | paste                     |
|  Ctrl + Shift + T        | 打开一个新的标签页           |
|  Ctrl + Shift + Q        | 退出该软件                  |
|  Ctrl + Plus(+)          | 增大当前终端字体大小（可能需要同时按Shift)  |
|  Ctrl + Minux(-)         | 减小当前终端字体大小（可能需要同时按Shift)  |
|  Ctrl + zero(0)          | 将字体大小恢复到初始化大小     |
|  Ctrl + tab / ctr+shift+n| 同窗口各小窗口间循环选中       |
|  Ctr+shift+f             | 窗口中搜索                    |
|  Ctrl+Shift+G            | 小窗口重设并清空窗口           | 
|  Ctrl+Shift+I/win+i      | 打开一个新开启的窗口           | 
|  Win + R                 | 一个tab中移动小窗口位置        | 

3. ~/.config/terminator/config配置
```sh
[global_config]                                                                                                                                                                                                     
[keybindings]
[layouts]
  [[default]]
    [[[child0]]]
      position=600
      order = 0 
      parent = window0
      type = VPaned

    [[[child1]]]    
      position=960
      order = 0 
      parent = child0
      profile = default
      type = HPaned 

    [[[child2]]]
      order = 1 
      parent = child0
      profile = default
      type = HPaned

    [[[term1]]]    
      profile = default
      order = 0 
      parent = child1
      type = Terminal 

    [[[term2]]]    
      profile = default
      order = 1 
      parent = child1
      type = Terminal 

    [[[term3]]]    
      profile = default
      order = 0 
      parent = child2
      type = Terminal 

    [[[term4]]]    
      profile = default
      order = 1 
      parent = child2
      type = Terminal 

    [[[window0]]]
      order = 0 
      parent = ""
      position = 1440:0
      size = 1920, 1200
      type = Window
[plugins]
[profiles]
  [[default]]
    background_image = None
    font = Monaco Bold 12
    use_system_font = False
```
显示效果如下图：
![terminator](/res/img/blog/linux学习/terminator-screen.png)

### 强大终端shell工具：[tmux]
0. 简介
```
Tmux(terminal multiplexer) 是一个终端复用器: 可以激活多个终端或窗口, 在每个终端都可以单独访问，每一个终端都可以访问，运行和控制各自的程序.tmux类似于screen，可以关闭窗口将程序放在后台运行，需要的时候再重新连接
```

1. 安装
```sh
sudo apt-get install tmux
```

2. 基本命令

| 快捷键      | 作用                       | 
| ---------- |:-------------:             |
|  tmux      | 启动tmux  　　     |
|  tmux ls   | 列出会话  　　　   |
|  tmux new -s session_name     | 开启一个新的session  　　　 |
|  tmux a    | 进入到第一个可用会话  　　　 |
|  tmux attach/a -t session     | 进入     某个会话  |
|  tmux kill-session -t <会话名>  | 杀死一个session  |
|  tmux rename-session -t <会话名> | 对一个session进行重命名 |
|  Ctrl-b d      | detached a session    |
|  ctrl-b $     | 给session指定名字  |

3. windows命令

| 快捷键      | 作用                      | 
| ----------   |:-------------:          |
|  ctrl-b c      | 新建窗口  　　         |
|  ctrl-b &      | 关闭窗口  　　　       |
|  ctrl-b num    | 指定到某个窗口         |
|  ctrl-b p/n    | 切换到上/下窗口        |
|  ctrl-b l      | 在两个窗口之间互相切换  |
|  ctrl-b w      | 通过窗口列表切换窗口    |
|  ctrl-b f      | 在所有窗口中查找指定文本 |

4. panel命令

| 快捷键      | 作用                       | 
| ---------- |:-------------:             |
|  Ctrl-b t      | 很酷的一个时钟  　　   |
|  ctrl-b x    | 关闭一个panel  　　　 |
|  ctrl-b "     | 在下边分割出来一个pane  |
|  Ctrl-b %     | 在右边分割出来一个pane     |
|  tmux -r     | 连接上次断开的session  |
|  Ctrl-b o[方向键]     | 在多个panes中切换，下一个  |
|  ctrl-b q     | 显示各panel编号  |
|  ctrl-b c     | 创建一个新的window  |
|  ctrl-b num     | 直接跳到你按的数字所在的window  |

5. tmux结构示意图

![tmux](/res/img/blog/linux学习/tmux.jpg)

### 强大终端编辑工具：vim
1. vim配置文件

2. 编辑快捷键

| 快捷键      | 作用                       | 
| ---------- |:-------------:             |
|  a / i     | 光标后／光标处插入           |
|  o / O     | 当前行下／上插入新空行       |
|  o / O     | 当前行下／上插入新空行       |
|  dd        | 删除当前行                  |
|  gg        | 光标到第一行行首             |
|  yw        | 复制从光标开始到词尾的字符    |
|  yy / nyy  | 拷贝光标所在行/下面几行      |
|  daw       | 删除 光标所处在那个单词      |
|  G         | 光标到最后一行行首          |
|  n         | 在同一方向重复上一次搜索命令 |
|  N         | 在反方向上重复上一次搜索命令
|  r         | 替换光标处字符              |
|  x         | 删除光标处字符              |
|  u         | 撤销上一步操作              |
|  U         | 撤销对当前行的所有操作       |
|  ctrl + r  | 恢复上一步操作              |
|  d0        | 删至行首                    |
|  d$        | 删至行尾                   |
|  h/j/k/l   | 光标左／下／上／右移动      |
|  p / P     | 拷贝到当前位置之后／前       |
|  fx        | 往右移动到x字符上           |
|  Fx        | 往左移动到x字符上          |
|  tx        | 往右移动到x字符前          | 
|  Tx        | 往左移动到x字符后          |
|  L         | 当前屏幕的末行             |
|  H         | 当前屏幕的首行             |
|  M         | 当前屏幕的中间行           |
|  w         | 将光标右移一个字(字首位置)   |
|  W         | 将光标右移连续字段首位置     |
|  e         | 将光标右移一个字(字末位置)   |
|  E         | 将光标右移连续字段末位置     |
|  b         | 将光标左移一个字(字首位置)   |
|  B         | 将光标左移连续字段首位置     |
|  ctrl + o  | 返回到上次光标的位置        |
|  ctrl + i  | 返回到最后一次光标的位置     |
|  { / }     | 跳到上一段的开头 ／ 跳到下一段的的开头    |
|  ( / )     | 移到这个句子的开头 / 移到下一个句子的开头 |
|  ctrl + e  | 屏幕向上滚动               |
|  ctrl + y  | 屏幕向下滚动               |
|  ctrl + v  | 块选择                    |
|  shift + v | 行选择                    |
|  Ctrl+u    | 向文件首翻半屏             |
|  Ctrl+d    | 向文件尾翻半屏             |
|  Ctrl+f    | 向文件尾翻一屏             |
|  Ctrl＋b   | 向文件首翻一屏             |
|  shift + v | 行选择                    |

3. 下标快捷键
```sh
:w                      : 保存，不退出
:w  xxx                 : 保存至xxx文件，不退出
:wq                      : 保存并退出
:q!                      : 不保存，强制退出
:set fileencoding       :   查看当前文件的编码
:set fenc=编码           :   转换当前编码为制定的编码
:set enc=编码            :   以指定的编码显示当前文本，但是不保存
:set ff?                :   查看当前文本的模式类型，一般为dos,unix
:set ff=dos/unix         :  设置为dos/ unix
:set nu                 :  显示行号
:set nonu
:set hlsearch           : 设置选中词汇均高亮
:list                   : 显示制表位(Ctrl+I)和行尾标志（$)
:1,$s/old_str/new_str/g  :  替换第一行到最后一行
:s/old_str/new_str/g     :  只替换当前行
/pattern                : 从光标开始处向文件尾搜索pattern
?pattern                : 从光标开始处向文件首搜索pattern
:n1,n2 d                : 将n1行到n2行之间的内容删除
:n1,n2 co n3            : 将n1行到n2行之间的内容拷贝到第n3行下
:n1,n2 m n3             : 将n1行到n2行之间的内容移至到第n3行下
:!command               : 执行shell命令command
```

4. vim中需要权限保存
```sh
:w !sudo tee %
```

5. vim命令示意图

![vim-命令](/res/img/blog/linux学习/vi-vim-cheat-sheet.gif)
