---
layout: life
title: Linux-Python-Pyenv
category: Python学习
duoshuo: true
date: 2017-06-02
---

    作者: minus
    时间: 2017-06-02
    版本: V0.0.1
    mail: minus@stu.xjtu.edu.cn


<!-- more -->

### 简述
```
pyenv可以帮助你在一台开发机上建立多个版本的python环境
virtualenv可以搭建虚拟且独立的python环境，可以使每个项目环境与其他项目独立开来，保持环境的干净，解决包冲突问题。
```

### pyenv install for ubuntu
1. 安装博客：http://blog.csdn.net/databatman/article/details/53955828
            http://blog.codylab.com/python-pyenv-management/
            https://github.com/pyenv/pyenv-installer [官网]
2. 安装步骤：
    1. 安装curl / git
        ```
        sudo apt-get install curl git-core
        ```
    2. 安装pyenv
        ```
        curl -L https://raw.github.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
        ```
        pyenv 安装到当前用户的~/.pyenv目录下
    3. 安装后将安装完成后给的提示写入到.bashrc,注意路径与自己机器保持一致
        ```
        export PATH="/home/minus/.pyenv/bin:$PATH"
        eval "$(pyenv init -)"
        eval "$(pyenv virtualenv-init -)"
        ```
        ```
        source ~/.bashrc
        ```
    4. 查看可以安装的所有版本
        ```
        pyenv install --list
        ```
    5. 安装具体版本号的python
        ```
        pyenv install 2.7.11
        pyenv rehash
        ```
        
    6. 查看已安装的版本
        ```
        pyenv versions
        ```
    7. 切换版本
        ```
        pyenv global 2.7.11
        pyenv local 2.7.11
        ```
    8. 卸载某个版本
        ```
        pyenv uninstall 2.7.11
        ```
    9. 创建虚拟python环境: pyenv 自带 virtualenv
        ```
        pyenv virtualenv 2.7.11(已安装的版本号) env271(name)
        ```
        可通过 ```pyenv versions```　查看得到当前所有的版本
    10. 切换到新的虚拟环境
        ```
        pyenv activate en271
        ```
    11. 退出虚拟环境
        ```
        pyenv deactivate
        ```
    12. 删除虚拟环境
        ```
        rm -rf ~/.pyenv/versions/env271   -  简单而且粗暴
        ```
    13. 解释
        ```
        pyenv global  : 修改系统python版本
        pyenv local   : 在当前目录创建一个.python-version，以后进入该目录自动切换到该版本
        pyenv shell   : 在当前shell的session中使用某个python版本，优先级高于 global, local
        ```
