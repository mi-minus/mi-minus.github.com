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

### [vim 基本配置](https://github.com/mi-minus/use_vim_as_ide)
1. 基本配置一
```
" 让配置变更立即生效
autocmd BufWritePost $MYVIMRC source $MYVIMRC
" 开启文件类型侦测
filetype on
" 根据侦测到的不同类型加载对应的插件
filetype plugin on
" 开启实时搜索功能
set incsearch
" 搜索时大小写不敏感
set ignorecase
" 关闭兼容模式
set nocompatible
" vim 自身命令行模式智能补全
set wildmenu
" 自适应不同语言的智能缩进
filetype indent on
" 将制表符扩展为空格
set expandtab
" 设置编辑时制表符占用空格数
set tabstop=4
" 设置格式化时制表符占用空格数
set shiftwidth=4
" 让vim 把连续数量的空格视为一个制表符
set softtabstop=4
set gcr=a:block-blinkon0
" 总是显示状态栏
set laststatus=2
" 显示光标当前位置
set ruler
" 高亮显示当前行和列
set cursorline
set cursorcolumn
" 高亮显示搜索结果
set hlsearch
" 设置 gvim显示字体
set guifont=YaHei\ Consolas\ Hybrid\ 11.5
" 开启语法高亮功能
syntax enable
" 允许用指定语法高亮配色方案替换默认方案
syntax on
" 开启文件类型检测
filetype on
" 根据侦测到的不同类型加载对应的插件
filetype plugin on
"""""""
set nu                                                                                                                                                                                                              
set encoding=utf-8
set termencoding=utf-8
set fileencoding=utf-8          
set textwidth=79
set autoindent 
set fileformat=unix        
set background=dark
colorscheme solarized
```
2. 基本配置二
```
" ================== vim-indent-guides =============
" 随vim自启动                 
let g:indent_guides_enable_on_vim_startup=1
" 从第二层开始可视化显示缩进  
let g:indent_guides_start_level=2
" 色块宽带                    
let g:indent_guides_guide_size=1
" 快捷键 i 开/关缩进可视化    
:nmap <silent><Leader>i <Plug>IndentGuidesToggle                       
" ===============　代码折叠 =====================
" 基于缩进或语法进行代码折叠  
" set foldmethod=indent       
set foldmethod=syntax         
" 启动vim时关闭折叠代码       
set nofoldenable              
```
3. [配置主题](https://github.com/altercation/vim-colors-solarized)
```
" 设置状态栏主题风格          
let g:Powerline_colorscheme='solarized256'
提示：需要安装主题：
* Download and install Tim Pope's Pathogen.
a. Clone:
    $ cd ~/.vim/bundle
    $ git clone git://github.com/altercation/vim-colors-solarized.git
b. Move:
In the parent directory of vim-colors-solarized:
    $ mv vim-colors-solarized ~/.vim/bundle/
```
### 系统vim后期处理


* vim 设置　tab 为　4个空格
    1. vimrc 修改
     ```
     :set ts=4
     :set expandtab
     ```
    2. 对已保存的文件: tab -> 空格
    ```
    :set ts=4
    :set expandtab
    :%retab!
    ```
    3. 空格　-> tab
    ```
    :set ts=4
    :set noexpandtab
    :%retab!
    ```
    * 加!是用于处理非空白字符之后的TAB，即所有的TAB，若不加!，则只处理行首的TAB。
        
离线安装:先在线安装Pathogen插件,然后将其他github安装包放到~/.vim/bundle/下， 进入vim 执行 :PluginInstall 就自动安装了，不用联网，速度很快
