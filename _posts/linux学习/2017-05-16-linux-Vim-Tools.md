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
|  alt + o                 | Broadall off              |
|  alt + o                 | Broadall off              |


### 强大终端编辑工具：vim
1. vim配置文件

2. 编辑快捷键

| 快捷键      | 作用               | 
| ---------- |:-------------:    |
|  fx        | 往右移动到x字符上    |
|  Fx        | 往左移动到x字符上    |
|  tx        | 往右移动到x字符前    |
|  Tx        | 往左移动到x字符后    |
|  L         | 当前屏幕的末行       |
|  H         | 当前屏幕的首行       |
|  M         | 当前屏幕的中间行     |
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

3. 下标快捷键
```sh
:set fileencoding       :   查看当前文件的编码
:set fenc=编码           :   转换当前编码为制定的编码
:set enc=编码            :   以指定的编码显示当前文本，但是不保存
:set ff?                :   查看当前文本的模式类型，一般为dos,unix
:set ff=dos/unix         :  设置为dos/ unix
:1,$s/old_str/new_str/g  :  替换第一行到最后一行
:s/old_str/new_str/g     :  只替换当前行
```

