Learning_Vim
============




# 1. 设定vim的工作路径
:cd                        改变vim的当前工作路径    
:lcd                       改变当前窗口的工作路径     
:pwd                       查看当前的工作路径     
:set autochdir            自动设当前编辑的文件所在目录为当前工作路径     






# 2. 一篇很全面的vim的入门介绍
[很全面的vim入门介绍]（http://blog.interlinked.org/tutorials/vim_tutorial.html ）






# 3. vim & markdown


## 3.1 vim中markdown的设置
参考这个网页中的内容，（http://calefy.org/2012/03/01/set-vim-markdown-syntax-highlight.html ），摘录下来。这个博主使用的也是vim markdown这个插件。
        
        在vim中设置markdown语法高亮是一个不错的选择，但是在google中搜索到的很多都是比较老的设置方式，甚至vim插件下载页面都是一个旧的版本。这里总结下我的修改过程，以帮助像我一样纠结的人。
        
        安装插件
        
        这个插件的安装和其他vim插件一样，都是拷贝相应文件到对应的目录。
        
        github下载：https://github.com/plasticboy/vim-markdown
        
        plasticboy下载：http://plasticboy.com/dox/vim-markdown.zip
        
        推荐使用github下载，plasticboy.com 版本中 ftdetect/mkd.vim 不如github上的更新，github上的版本能够支持多种后缀名称的文件。
        
        将下载的zip文件解压后，会得到下面的目录结构：
        
         .
         |-- syntax
         |   |-- mkd.vim
         |-- ftdetect
         |   |-- mkd.vim
        将两个 mkd.vim 分别复制到 $VIM 下对应的 syntax 和 ftdetect 文件夹中。
        
        $VIM 对应的目录在windows和Linux系统上是不同的，相信你在安装使用vim的时候应该已经注意到了。
        
        Mac和Linux下一般是 ~/.vim/，如果没有对应的文件夹，用mkdir创建
        
          cp ./syntax/mkd.vim ~/.vim/syntax/
          cp ./ftdetect/mkd.vim ~/.vim/ftdetect/
        Windows一般就是vim的安装目录下了。
        一切就是这么简单，复制到对应目录，然后重启你的vim就ok了。
        
        
        插件内容
        
        尽管名字相同，两个文件夹中的文件是不同的。
        
        syntax中的 mkd.vim 是关键的语法解析文件，里面是关于语法高亮的详细定义。
        ftdetect中的 mkd.vim 定义的是自动解析哪些文件。
        
        下面是github最新版本中的定义方式，支持的后缀名包括花括号中的内容，如果有新的定义，可以自己添加
        
          au BufRead,BufNewFile *.{md,mdown,mkd,mkdn,markdown,mdwn}   set filetype=mkd
        结论
        
        相比较很多之前文章介绍的复杂方式，这个应该是最传统简单的了。只要放置对应目录的文件，不需要在vim用户配置文件中做
        任何修改即可使用markdown的语法高亮，比单纯的文本明了很多。




## 3.2 vim写markdown的实时预览

        使用chrome插件Markdown Preview Plus。在插件管理界面选中”Allow access to file URLs”，在插件自身的选项里选中
        “Enable auto-reload”,还以选择内置的CSS或者自定义CSS，这插件还挺靠谱。
        
        然后用vim写Markdown,用chrome浏览器打开markdown文件预览html,修改了markdown文件之后，刷新一下chrome的预览，就会看到更新的markdown文件。




## 3.3 vim中直接运行pandoc
吐槽一下那个vim pandoc包，奶奶的，一点都好不用！更简单的方法如下。

比如我们要把test.md在vim中直接转成pdf，并且直接通过vim命令来打开。可以通过下面的命令来实现。

    :!pandoc test.md -s -o test.pdf  --latex-engine=xelatex --template=template.tex
    :!.\test.pdf
 这个！的意思是要在vim中运行cmd的命令，所以必须要加，不能省去。
 
 同样的方法可以将md转为其他的格式，语法和一般的pandoc语法是一样的，只是要在vim中加上:!这样一个表示vim命令状态（:），一个表示运行cmd的命令（！）。
 
 
 
 
# 4. vim中安装vundle

- 首先从github中下载vundle包，vundle在github中的网址是(https://github.com/gmarik/Vundle.vim )。我window7中安装了gitbash,在gitbash中输入以下的命令

        git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
- 从github中clone下来的vundle包在C:\Users\ms-off1\.vim中，会出现一个名为bundle的文件夹，这个文件夹下面会有一个Vundle.vim的文件夹。**非常重要的一点事是将这个文件夹重命名为vundle**。
- 将重命名后的bundle文件夹复制一份，放入到vim安装目录下的vimfiles中，在我的电脑里是放在C:\Program Files (x86)\Vim\vimfiles下。这个目录下会有一份bundle文件夹，这个文件夹下有一个vundle文件夹。
- 安装curl脚本
  - google curl，curl的官方下载网站是（http://curl.haxx.se/download.html ）。从这个网页上找到对应自己电脑的安装包，下载zip文件包。
  - 将此下载的zip包解压，里面有一个curl.exe文件，双击安装，一下子就安装好了。
  - 在电脑里的一个地方防止curl.exe文件，比如我在C:\Program Files (x86)下新建了一个curl文件夹，把curl.exe放在这个文件夹下。
  - 非常重要的一步是把C:\Program Files (x86)\curl这个curl.exe所在的路径放入到电脑的系统路径path中。
  - 新建一个空的txt文件，把下面的命令粘贴进这个txt空文件中，保存之后，将此空文本文件重命名为curl.cmd
                
        @rem Do not use "echo off" to not affect any child calls.
        @setlocal
        
        @rem Get the abolute path to the parent directory, which is assumed to be the
        @rem Git installation root.  
        @for /F "delims=" %%I in ("%~dp0..") do @set git_install_root=%%~fI  
        @set PATH=%git_install_root%\bin;%git_install_root%\mingw\bin;%PATH%  
      
        @if not exist "%HOME%" @set HOME=%HOMEDRIVE%%HOMEPATH%  
        @if not exist "%HOME%" @set HOME=%USERPROFILE%  
  
        @curl.exe %*  
  - 将curl.cmd文件放入到git的安装路径中，我的电脑中git的路径是C:\Program Files (x86)\Git，就把curl.cmd放入到这个路径下。
  - 在cmd中输入curl --version来检测curl是否已经安装成功。
  
- 配置_vimrc文件
  在_vimrc文件中加入以下的命令，这个命令来自这个网站（http://www.haiyun.me/archives/vim-vundle.html ）

        set nocompatible "与vi不一致
        filetype off
        set rtp+=~/.vim/bundle/vundle/ "载入特定目录插件
        "set rtp+=$HOME/.vim/bundle/vundle/ "Windows下
        call vundle#rc()
        "plugin 
        "vimscripts账号下的项目直接填写名称即可
        Bundle 'snipMate'
        "其它需填写用户/资源名称
        Bundle 'gmarik/vundle'
        "非github上资源
        Bundle 'git://git.wincent.com/command-t.git'
        "indent
        Bundle 'php.vim-html-enhanced'
        "color
        Bundle 'Lucius'
        filetype plugin indent on
   
- 至此，vim中vundle就安装成功了。但是在使用BundleInstall这样的命令式经常回出现如下的报错

        E303: Unable to open swap file for "[No Name]", recovery impossible
中文gvim中的报错大概是这样
        
        E303：无法打开“[Vundle] List”的交换文件，恢复将不可能。
具体为什么会出现这个报错，请看这个网站的说明（http://blog.csdn.net/tms_li/article/details/16369235 ）。这个网站顺带也提供了解决方法。

        A good location would be the directory pointed to by the %TEMP% environment variable. On Windows 7, this points to C:\Users\AverageJoe\AppData\Local\Temp
就是将C:\Users\AverageJoe\AppData\Local\Temp命名为%TEMP%的环境变量，并且将%TEMP%加入到系统路径中。然后在_vimrc中加入下面的语句
        
        set dir=$TEMP
这样这个报错的问题就会解决了。

- Vundle的使用
 :BundleInstall 就可以自动安装上述配置文件中的 vim 插件    
 :BundleInstall!   更新全部插件
 :BundleUpdate  更新某一个插件
 如果要删除插件，则从 .vimrc 文件中删除或注释掉相应行，然后运行 :BundleClean 即可       
 :BundleSearch+插件名称，就是搜索这个插件    
 :BundleList 显示所有已经安装的插件   


# 5.Vim中Python的配置

## 5.1 pydiction自动补全的安装
自动补全用的是pydiction这个包。可以在（http://www.vim.org/scripts/script.php?script_id=850 ）下载，也可以用vundle安装。
官网给的安装方法如下

        cd ~/.vim/bundle 
        git clone https://github.com/rkulla/pydiction.git 
可以看到是先进入到C:\Users \ms-off1\.vim\bundle下，然后通过git把pydiction克隆到这个目录下。

然后配置_vimrc
        
        filetype plugin on
        let g:pydiction_location = 'C:\Users \ms-off1\.vim\bundle\complete-dict' (Users之后一定要有一个空格，不知道是为什么！！)
        let g:pydiction_menu_height = 3 
这里的3的意思是补全时有多少个选项。
        

__重要的是ctrl+n和ctrl+p进行补全__



## 5.2 Python_fode的安装

简介：将Python代码折叠，Python的class，function，以及在{{{,}}}标记的内容将被折叠。

　　下载：http://vim.sourceforge.net/scripts/script.php?script_id=515

　　安装：将下载的python_fold.vim拷贝到C:\Users \ms-off1\\.vim\plugin 目录下(Users之后一定要有一个空格，不知道是为什么！！)。如果没有plugin这个文件夹，就新建一个。

　　　　关闭开启时默认折叠命令，在.vimrc写入：

        set foldmethod=indent
　　　　zo: 展开单个折叠区。

　　　　zc: 聚合单个折叠区。

　　　　zn: 展开全部折叠区。

　　　　zN: 聚合全部折叠区。

        zo: 打开光标位置的折叠代码；       
        zc: 折叠光标位置的代码；     
        zr: 将文件中所有折叠的代码打开；    
        zm: 将文件中所有打开的代码折叠；    
        zR: 作用和 zr 类似，但会打开子折叠（折叠中的折叠）；     
        zM: 作用和 zm 类似，但会关闭子折叠；    
        zi: 折叠与打开操作之间的切换命令；    

# 6.Vim小技巧
- 在Vim中你可以把两行合并为一行，也就是说两行之间的换行符被删除了：命令是"J"。
- ctrl+p和ctrl+n是vim中的自动补齐


- 光标移动
        - :行号，光标移动到对应航。:3光标移动到第3行     
        - '. (是”所在的键，不要shift，加上英文的句号)，表示回到上次修改的行     
        - `. （是~所在的键，不要shift,加上英文的句号），表示回到上次修改的点     
        - H 移动光标到屏幕的首行     
        - L 移动光标到屏幕的末行    
        - gg 移动光标到文档的首行    
        - G 移动光标到文档的末行    
        - M 移动光标到屏幕的中间    
        - 还有其他常见的命令，参考[很全面的vim入门介绍]（http://blog.interlinked.org/tutorials/vim_tutorial.html ）   


- 复制（http://blog.sina.com.cn/s/blog_5caa94a00100codi.html ）
    - yw:表示拷贝从当前光标到光标所在单词结尾的内容.            在英语中可以用来复制一个单词。如果是中文的话，表示拷贝到从光标处到不同状态处（包括英文，标点等），但是如果比如，你好啊     哈哈哈，光标在你字时，按yw,会把中间的三个空格也拷贝上。
    - ynw：复制n个单词，在中文中，比如“国企的CEO hahaha”，y1w表示复制国企的，y2w表示复制国企的CEO，y3w表示复制国企的CEO hahaha    
    - yy：复制一行      
    - ynl:复制n个字符，在中文中，y2l就表示复制两个汉字。      
    - y$:复制当前光标至行尾处     
    - nyy:拷贝n行 
    - yn:拷贝n行
    - yfa:表示拷贝从当前光标到光标后面的第一个a字符之间的内容.
    - 单行复制   
    在命令模式下，将光标移动到将要复制的行处，按“yy”进行复制；   
    - 多行复制   
    在命令模式下，将光标移动到将要复制的首行处，按“nyy”复制n行；其中n为1、2、3……   
    - 粘贴  
    在命令模式下，将光标移动到将要粘贴的行处，按“p”进行粘贴


- 删除（http://www.study-area.org/tips/vim/Vim-3.html ）
        
        x  刪除游標所在處之字元。在 vim 及 elvis 亦可用 Del 鍵。
        X  刪除游標前之字元。不可使用 Backspace 鍵。
        vim 可以正確使用以上兩個指令於中文，會刪去一個中文字。elvis 則不行，一個中文字要刪兩次，即使用 xx。
        dd 刪除一整行(delete line)。
        dw 刪除一個字(delete word)。不能適用於中文。
        dG 刪至檔尾。
        d1G 刪至檔首。或 dgg(只能用於 vim)。
        D  刪至行尾，或 d$（含游標所在處字元）。
        d0 刪至行首，或 d^（不含游標所在處字元）。
        dfa  表示删除从当前光标到光标后面的第一个a字符之间的内容.

- 多窗口操作时关闭的命令
^代表Ctrl键     
^Wq，离开当前窗口      
^Wc，关闭当前的窗口     
^Wo，关闭当前窗口以外的所有窗口   

- 多行缩进和前进
   - :30>>,第30行缩进
   - :30>>,第30行前进
   - :10,100>，第10行至第100行缩进
   - :20,80<，第20行至第80行反缩进
   - 在insert状态下，ctrl+t，当前行缩进
   - 在insert状态下，ctrl+d，当前航反缩进
   - 在normal状态下，shift+>>，当前行缩进
   - 在normal状态下，shift+<<，当前行反缩进
   - :nj，这个命令如果n是一个空格行，那么输入:nj这个空格行就会消失，并且，空格上下的行会对其；如果n是一个有文字的行，那么这一行行下面的空格行（n+1行）就会消失，n+2行的文字就会上来和第n行文字对齐。
   - 在vim里，粘贴代码之前最好进入粘贴模式，这样就会关闭自动缩进，即在normal模式下，输入:set paste，在进入insert模型进行粘贴；代码粘贴进去之后再关闭粘贴模式，:set nopaste
   

- 编辑命令 
   - cc:删除整行，并进入插入模式
   - cw:删除当前光标处至另一种状态处（如文字到空格，文字到标点，标点至文字），并且进入插入模式，比如 Thank you very much！Really!，如果光标在T处，按cw，thank这个单词就会被删除；如果光标在h处，那么hank就会被删除；如果光标在Thank后面的空格，按cw，那么这个空格会被删除。比如，你好啊！最近怎么样呢？如果光标在你处，按cw，你好啊三个字会被删除；如果光标在！处，按cw，只有！会被删掉。
   - r:然后输入的字母将替换当前字母并保持命令模式,R则是不停的替换(一个挨着一个)。**个人觉得R这个命令特有用**



- 多窗口命令
   - :split 文件名，会把“文件名”所代表的文件会开一个新窗口打开
   - ：f   切分显示光标在处的文件名，VIM 会在 path 中搜索该文件名，比如常用它打开 #include 语句中的文件
   - :close，会关闭光标所在的分窗口，剩下只有一个窗口的话就不能关了。
   -  用Ctrl-W命令指定光标移动： 
      
- 数字与命令

        在 vi 中数字与命令结合往往表示重复进行此命令, 若在扩展模式的开头出现则表示行号定位. 如:
        5fx              表示查找光标后第 5 个 x 字符.
        5w(e)            移动光标到下五个单词.
        5yy              表示拷贝光标以下 5 行.
        5dd              表示删除光标以下 5 行.
        y2fa             表示拷贝从当前光标到光标后面的第二个a字符之间的内容.
        :12,24y          表示拷贝第12行到第24行之间的内容.
        :12,y            表示拷贝第12行到光标所在行之间的内容.
        :,24y            表示拷贝光标所在行到第24行之间的内容. 删除类似.


- 替换

        替换是 vi 的强项, 因为可以用正规表达式来匹配字符串.以下提供几个例子.
        :s/aa/bb/g       将光标所在行出现的所有包含 aa 的字符串中的 aa 替换为 bb
        :s/\/bb/g   将光标所在行出现的所有 aa 替换为 bb, 仅替换 aa 这个单词
        :%s/aa/bb/g      将文档中出现的所有包含 aa 的字符串中的 aa 替换为 bb
        :12,23s/aa/bb/g 将从12行到23行中出现的所有包含 aa 的字符串中的 aa 替换为 bb
        :12,23s/^/#/     将从12行到23行的行首加入 # 字符
        :%s= *$==        将所有行尾多余的空格删除
        :g/^\s*$/d        将所有不包含字符(空格也不包含)的空行删除.

- 全文替换

        语法为 :[addr]s/源字符串/目的字符串/[option]
        全局替换命令为：:%s/源字符串/目的字符串/g
        [addr] 表示检索范围，省略时表示当前行。
        如：“1，20” ：表示从第1行到20行；
        “%” ：表示整个文件，同“1,$”；
        “. ,$” ：从当前行到文件尾；
        s : 表示替换操作
        [option] : 表示操作类型
        如：g 表示全局替换; 
        c 表示进行确认
        p 表示替代结果逐行显示（Ctrl + L恢复屏幕）；
        省略option时仅对每行第一个匹配串进行替换；
        如果在源字符串和目的字符串中出现特殊字符，需要用”\”转义
        下面是一些例子：
        #将That or this 换成 This or that
        :%s/\(That\) or \(this\)/\u\2 or \l\1/
        —- 
        #将句尾的child换成children
        :%s/child\([ ,.;!:?]\)/children\1/g
        —-
        #将mgi/r/abox换成mgi/r/asquare
        :g/mg\([ira]\)box/s//mg//my\1square/g    <=>  :g/mg[ira]box/s/box/square/g
        —-
        #将多个空格换成一个空格
        :%s/  */ /g
        —-
        #使用空格替换句号或者冒号后面的一个或者多个空格
        :%s/\([:.]\)  */\1 /g
        —-
        #删除所有空行
        :g/^$/d
        —-
        #删除所有的空白行和空行
        :g/^[  ][  ]*$/d
        —-
        #在每行的开始插入两个空白
        :%s/^/>  /
        —-
        #在接下来的6行末尾加入.
        :.,5/$/./
        —-
        #颠倒文件的行序
        :g/.*/m0O  <=> :g/^/m0O
        —-
        #寻找不是数字的开始行,并将其移到文件尾部
        :g!/^[0-9]/m$ <=> g/^[^0-9]/m$
        —-
        #将文件的第12到17行内容复制10词放到当前文件的尾部
        :1,10g/^/12,17t$
        ~~~~重复次数的作用
        —-
        #将chapter开始行下面的第二行的内容写道begin文件中
        :g/^chapter/.+2w>>begin
        —-
        :/^part2/,/^part3/g/^chapter/.+2w>>begin
        —-
        :/^part2/,/^part3/g/^chapter/.+2w>>begin|+t$
        
- 分屏和关闭当前屏幕
        :new，新建文件并分屏， 快捷键，Ctrl+W，然后马上按n键 

        :spilt 水平分屏，将当前屏分为两个，水平的。   Ctrl + w, s
        
        :vsplit 垂直分屏，将当前屏分为两个，垂直的。  Ctrl + w, v
        
        :only 取消分屏，取消当前的屏，当前屏指的是光标所在屏。
