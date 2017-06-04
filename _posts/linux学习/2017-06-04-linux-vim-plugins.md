---
layout: life
title: linux-vim-plugins
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
" 禁止光标闪烁
set gcr=a:block-blinkon0
" 禁止显示滚动条
set guioptions-=l
set guioptions-=L
set guioptions-=r
set guioptions-=R
" 禁止显示菜单和工具条
set guioptions-=m
set guioptions-=T
" 总是显示状态栏
set laststatus=2
" 显示光标当前位置
set ruler
" 开启行号显示
set number
" 高亮显示当前行/列
set cursorline
set cursorcolumn
" 高亮显示搜索结果
set hlsearch
" 禁止折行
set nowrap
" 基于缩进或语法进行代码折叠
"set foldmethod=indent
set foldmethod=syntax
" 启动 vim 时关闭折叠代码
set nofoldenable
" 操作：za，打开或关闭当前折叠；zM，关闭所有折叠；zR，打开所有折叠
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

### bundle安装

0. 基本信息

```
vim 自身希望通过在 .vim/ 目录中预定义子目录管理所有插件（比如，子目录 doc/ 存放插件帮助文档、plugin/ 存放通用插件脚本），vim 的各插件打包文档中通常也包含上述两个（甚至更多）子目录，用户将插件打包文档中的对应子目录拷贝至 .vim/ 目录即可完成插件的安装。一般情况下这种方式没问题，但我等重度插件用户，.vim/ 将变得混乱不堪，至少存在如下几个问题：
    * 插件名字冲突。所有插件的帮助文档都在 doc/ 子目录、插件脚本都在 plugin/ 子目录，同个名字空间下必然引发名字冲突；
    * 插件卸载易误。你需要先知道 doc/ 和 plugin/ 子目录下哪些文件是属于该插件的，再逐一删除，容易多删/漏删。
我希望每个插件在 .vim/ 下都有各自独立子目录，这样需要升级、卸载插件时，直接找到对应插件目录变更即可；另外，我希望所有插件清单能在某个配置文件中集中罗列，通过某种机制实现批量自动安装/更新/升级所有插件。vundle（https://github.com/VundleVim/Vundle.vim ）为此而生，它让管理插件变得更清晰、智能。
```

1. 安装vundle
```
vundle 会接管 .vim/ 下的所有原生目录，所以先清空该目录，再通过如下命令安装 vundle：
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

2. .vimrc配置
```
" vundle 环境设置
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
" vundle 管理的插件列表必须位于 vundle#begin() 和 vundle#end() 之间
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'altercation/vim-colors-solarized'
Plugin 'tomasr/molokai'
Plugin 'vim-scripts/phd'
Plugin 'Lokaltog/vim-powerline'
Plugin 'octol/vim-cpp-enhanced-highlight'
Plugin 'nathanaelkane/vim-indent-guides'
Plugin 'derekwyatt/vim-fswitch'
Plugin 'kshenoy/vim-signature'
Plugin 'vim-scripts/BOOKMARKS--Mark-and-Highlight-Full-Lines'
Plugin 'majutsushi/tagbar'
Plugin 'vim-scripts/indexer.tar.gz'
Plugin 'vim-scripts/DfrankUtil'
Plugin 'vim-scripts/vimprj'
Plugin 'dyng/ctrlsf.vim'
Plugin 'terryma/vim-multiple-cursors'
Plugin 'scrooloose/nerdcommenter'
Plugin 'vim-scripts/DrawIt'
Plugin 'SirVer/ultisnips'
Plugin 'Valloric/YouCompleteMe'
Plugin 'derekwyatt/vim-protodef'
Plugin 'scrooloose/nerdtree'
Plugin 'fholgado/minibufexpl.vim'
Plugin 'gcmt/wildfire.vim'
Plugin 'sjl/gundo.vim'
Plugin 'Lokaltog/vim-easymotion'
Plugin 'suan/vim-instant-markdown'
Plugin 'lilydjwg/fcitx.vim'
" 插件列表结束
call vundle#end()
filetype plugin indent on
```

3. 安装插件

```
此后，需要安装插件，先找到其在 github.com 的地址，再将配置信息其加入 .vimrc 中的call vundle#begin() 和 call vundle#end() 之间，最后进入 vim 执行
    * :PluginInstall
要卸载插件，先在 .vimrc 中注释或者删除对应插件配置信息，然后在 vim 中执行 
    * :PluginClean
即可删除对应插件。插件更新频率较高，差不多每隔一个月你应该看看哪些插件有推出新版本，批量更新，只需执行
    * :PluginUpdate
查看安装的插件
    * :PluginList
```

### 快捷键

1. 分屏
```
:sv <filename>命令打开一个文件，你可以纵向分割布局（新文件会在当前文件下方界面打开），
:vs <filename>， 你可以得到横向分割布局（新文件会在当前文件右侧界面打开
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
