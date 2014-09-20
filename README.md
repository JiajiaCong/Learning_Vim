Learning_Vim
============

# 设定vim的工作路径
:cd                        改变vim的当前工作路径    
:lcd                       改变当前窗口的工作路径     
:pwd                       查看当前的工作路径     
:set autochdir            自动设当前编辑的文件所在目录为当前工作路径     

# 一篇很全面的vim的入门介绍
[很全面的vim入门介绍]（http://blog.interlinked.org/tutorials/vim_tutorial.html ）

# vim & markdown

## vim中markdown的配置

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

## vim写markdown的实时预览

        使用chrome插件Markdown Preview Plus。在插件管理界面选中”Allow access to file URLs”，在插件自身的选项里选中
        “Enable auto-reload”,还以选择内置的CSS或者自定义CSS，这插件还挺靠谱。
        
        然后用vim写Markdown,用chrome浏览器打开markdown文件预览html,修改了markdown文件之后，刷新一下chrome的预览，就会看到更新的markdown文件。

## vim中直接运行pandoc
吐槽一下那个vim pandoc包，奶奶的，一点都好不用！更简单的方法如下。

比如我们要把test.md在vim中直接转成pdf，并且直接通过vim命令来打开。可以通过下面的命令来实现。

    :!pandoc test.md -s -o test.pdf  --latex-engine=xelatex --template=template.tex
    :!.\test.pdf
 这个！的意思是要在vim中运行cmd的命令，所以必须要加，不能省去。
 
 同样的方法可以将md转为其他的格式，语法和一般的pandoc语法是一样的，只是要在vim中加上:!这样一个表示vim命令状态（:），一个表示运行cmd的命令（！）。
 
 
## vim中安装vundle

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


# Vim小技巧
- 在Vim中你可以把两行合并为一行，也就是说两行之间的换行符被删除了：命令是"J"。
- 复制（http://blog.sina.com.cn/s/blog_5caa94a00100codi.html ）
    - yw	将光标所在之处到字尾的字符复制到缓冲区中，可以用来复制一个单词
    - ynw：复制n个单词     
    - yy：复制一行      
    - ynl:复制n个字符      
    - y$:复制当前光标至行尾处     
    - nyy:拷贝n行     
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
