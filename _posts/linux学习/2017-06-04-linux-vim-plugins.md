---
layout: life
title: linux基础操作
category: linux学习
duoshuo: true
date: 2017-05-16
---

    作者: minus
    时间: 2017-05-23
    版本: V0.0.1
    mail: minus@stu.xjtu.edu.cn


<!-- more -->

### 查看ubuntu基本信息


cp ~/.vim/bundle/vim-colors-solarized/colors/solarized.vim ~/.vim/colors/

    * vim 设置　tab 为　4个空格
        1. vimrc 修改
           ```set ts=4```
           ```set expandtab```
        2. 对已保存的文件: tab -> 空格
            ```:set ts=4```
            ```:set expandtab```
            ```:%retab!```
        3. 空格　-> tab
            ```:set ts=4```
            ```:set noexpandtab```
            ```:%retab!```
        * 加!是用于处理非空白字符之后的TAB，即所有的TAB，若不加!，则只处理行首的TAB。
        

离线安装:先在线安装Pathogen插件,然后将其他github安装包放到~/.vim/bundle/下， 进入vim 执行 :PluginInstall 就自动安装了，不用联网，速度很快
