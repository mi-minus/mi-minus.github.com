---
layout: life
title: linux-vim-plugins
category: linux学习
duoshuo: true
date: 2017-06-04
---

    作者: minus
    时间: 2017-06-04
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
set foldmethod=indent  " 适合用于python
set foldmethod=syntax  " 适合用于java等语言
" 启动 vim 时关闭折叠代码
set nofoldenable
" 操作：za，打开或关闭当前折叠；zM，关闭所有折叠；zR，打开所有折叠
" 实现鼠标移动/定位/点击等
set mouse=a
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

4. 配置主题风格

```
一套好的配色方案绝对会影响你的编码效率，vim 内置了 10 多种配色方案供你选择，GUI 下，可以通过菜单（Edit -> Color Scheme）试用不同方案，字符模式下，需要你手工调整配置信息，再重启 vim 查看效果（csExplorer 插件，可在字符模式下不用重启即可查看效果）。不满意，可以去 http://vimcolorschemetest.googlecode.com/svn/html/index-c.html 慢慢选。我自认为“阅美无数”，目前最夯三甲：
    * 素雅 solarized（https://github.com/altercation/vim-colors-solarized ）
    * 多彩 molokai（https://github.com/tomasr/molokai ）
    * 复古 phd（http://www.vim.org/scripts/script.php?script_id=3139 ）
注意：
    * 上面三种主题文件 xxx.vim[molokai.vim/ phd.vim/ solarized.vim] 均放到 ~/.vim/colors/　下面
    * 在~/.vimrc中 填写 colorscheme molokai / colorscheme solarized ,通过这种方式实现 主题的应用
    " 配色方案如下：
    set background=dark
    colorscheme solarized
    "colorscheme molokai
    "colorscheme phd
```

5. 配置光标
```
* vim 十字光标
"height ligth cusor
set t_Co=256
set cursorline
set cursorcolumn
highlight CursorLine cterm=none ctermbg=236
highlight CursorColumn cterm=none ctermbg=236
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
Plugin 'scrooloose/syntastic'
Plugin 'kien/ctrlp.vim'
Plugin 'scrooloose/nerdcommenter'
Plugin 'vim-scripts/tComment'
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

4. plugin离线安装
```
离线安装:先在线安装Pathogen插件,然后将其他github安装包放到~/.vim/bundle/下， 进入vim 执行 :PluginInstall 就自动安装了，不用联网，速度很快
```

5. [安装 YouCompleteMe](http://www.mamicode.com/info-detail-1596462.html)
```
* 先编辑.vimrc和运行 :PluginInstall 命令实现安装YouCompleteMe (这时候还不能用)
* 1 cd ~/.vim/bundle/YouCompleteMe
* 2 ./install.py --clang-completer   //该步骤需要花点时间安装ycm
* 3. ./install.py --clang-completer --system-libclang
* 4. 安装博客（very nice）：https://valloric.github.io/YouCompleteMe/#ubuntu-linux-x64
```
6. vim中运行python
```
"===========  F5 run python ====================
autocmd BufRead *.py set makeprg=python\ -c\ \"import\ py_compile,sys;\sys.stderr=sys.stdout;\ py_compile.compile(r'%'')\"
autocmd BufRead *.py set efm=%C\ %.%#,%A\ \ File\ \"%f\"\\,\ line\ %l%.%#,%Z%[%^\ ]%\\@=%m
autocmd BufRead *.py nmap <F5> :!python %<CR>
autocmd BufRead *.py set tabstop=4
autocmd BufRead *.py set nowrap
autocmd BufRead *.py set go+=b
nnoremap <buffer> <F9> :exec '!python' shellescape(@%, 1)<cr>
```

7. vim python头信息配置
```
" ==================== python header file ==============="
function HeaderPython()
    call setline(1, "#!/usr/bin/env python")
    call append(1, "#-*- coding:utf8 -*-")
    call append(2, "# Power by MINUS" . strftime('%Y-%m-%d %T', localtime()))
    normal G
    normal o
    normal o
endf
autocmd bufnewfile *.py call HeaderPython()
" ======================================================="
```

8. 

### 快捷键

1. 分屏
```
:sv <filename>命令打开一个文件，你可以纵向分割布局（新文件会在当前文件下方界面打开），
:vs <filename>， 你可以得到横向分割布局（新文件会在当前文件右侧界面打开
```

2. vim屏幕切换
```
"split navigations
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>
组合快捷键： - Ctrl-j 切换到下方的分割窗口 - Ctrl-k 切换到上方的分割窗口 - Ctrl-l 切换到右侧的分割窗口 - Ctrl-h 切换到左侧的分割窗口
```

### 系统vim后期处理
* vim 以非root权限编辑root文件后强制保存方法
```
:w !sudo tee %
然后输入密码并进行保存
```

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
    
* vim 字符串替换
    ```
    s 命令来替换字符串
    :1,$s/old/new/g```  替换第一行到最后一行
    :s/old/new/g```  只替换当前行所有old
    :n，$s/vivian/sky/g 替换第 n 行开始到最后一行中每一行所有 vivian 为 sky 
    可以使用 # 作为分隔符，此时中间出现的 / 不会作为分隔符 
    ：s#vivian/#sky/# 替换当前行第一个 vivian/ 为 sky/ 
    
    ```
    
### 展示界面
1. ![vim界面](/res/download/linux/vim_background.png)

### VIM样例文件下载（仅供参考）
1. [.vimrc](/res/download/linux/vimrc)
