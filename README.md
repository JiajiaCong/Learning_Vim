Learning_Vim
============

# 设定vim的工作路径
:cd                        改变vim的当前工作路径    
:lcd                       改变当前窗口的工作路径     
:pwd                       查看当前的工作路径     
:set autochdir            自动设当前编辑的文件所在目录为当前工作路径     


# vim中markdown的配置
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
        
        相比较很多之前文章介绍的复杂方式，这个应该是最传统简单的了。只要放置对应目录的文件，不需要在vim用户配置文件中做任何修改即可使用markdown的语法高亮，比单纯的文本明了很多。
