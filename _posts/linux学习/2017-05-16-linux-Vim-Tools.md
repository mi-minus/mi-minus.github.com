---
layout: life
title: linux Vim Tools介绍
category: linux学习
date: 2017-05-16
---

    作者: minus
    时间: 2016-5-23
    版本: V0.0.1
    mail: minus@stu.xjtu.edu.cn


<!-- more -->
### 强大终端工具一：terminator
0. 简介
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

4.vim中需要权限保存
```sh
:w !sudo tee %
```
