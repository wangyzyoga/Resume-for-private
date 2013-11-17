---
category: Tools
layout: post
title: Vim中常用三个插件（nerdtree/ctrlp/ack）
---

###1、The NERDTree 树型结构显示文件

* 下载[NERDTree](http://www.vim.org/scripts/script.php?script_id=1658)

* 把下载的压缩包解压到~/.vim目录中

* 用vim打开工程，就出现树型结构

此处需要特别注意的是，在树型结构选中需要打开的文件，如果按Enter键，树型结构就会消失，全屏显示你刚才想打开的文件。

有三个办法可以既打开想要显示的文件，还保持树型结构存在，这才是我们希望实现功能：

* 在树型结构选中需要打开的文件，按i键，此时屏幕左边是树型结构，右边是需要显示的文件

* 在树型结构选中需要打开的文件，按Enter键，再输入 :NERDTree

* 现在~/.vimrc中增加如下设置，然后在树型结构选中需要打开的文件，按Enter键，再按F8

      let NERDTreeShowBookmarks = 1
	  let NERDChristmasTree = 1
	  let NERDTreeWinPos = "left"
      map <F8> :NERDTree<CR> 
<br />
###2、CtrlP 快速搜索文件

* 下载[CtrlP](http://kien.github.io/ctrlp.vim/)

* 把下载的压缩包解压到~/.vim目录中

* 在～/.vimrc中增加如下设置

      set runtimepath^=~/.vim/ctrlp.vim
<br />
###3、Ack 全项目文件搜索含有关键字的位置

* Ubuntu中使用如下命令进行安装

      sudo apt-get install ack-grep

* 在～/.vimrc中增加如下设置
      
      function! Ack(args)
	    let grepprg_bak=&grepprg
	    set grepprg=ack\ -H\ --nocolor\ --nogroup
	    execute "silent! grep " . a:args
		botright copen
	    let &grepprg=grepprg_bak
		endfunction

	    command! -nargs=* -complete=file Ack call Ack(<q-args>)

* Ack仍然不好使用时，需要执行如下命令

      sudo ln -s /usr/bin/ack-grep /usr/local/ack