---
title: 'Day Three - Configuring Debian GNU/Linux 6.0.5 "squeeze"'
date: 2012-09-11T21:45:00.000-07:00
draft: false
tags: 
- linux
- debian
---

More pedestrian things, tonight.  
_Configure vim colors_  
Via my 2008 [post](http://schultkl.blogspot.com/2008/03/vim-color-schemes.html):  

*   sudo cp /usr/share/vim/vim72/colors/koehler.vim /usr/share/vim/vim72/colors/koehler.vim.bak
*   I did not actually finish this one...I think I changed it when I edited software....

_Configure vim  .vimrc_

*   From my 2009 [post](http://schultkl.blogspot.com/2009/03/vimrc.html), copied and pasted into ~/.vimrc .
*   Historical note: the "rc" in ".vimrc" [derives](http://superuser.com/questions/144339/sayvimrcor-screenrc-what-does-the-rc-mean) from "runcom", from the MIT CTSS system, ca. 1965. [More](http://www.faqs.org/faqs/unix-faq/faq/part1/section-3.html).

_Configure GNOME Terminal 2.30.2 colors_

Via my 2008 [post](http://schultkl.blogspot.com/2008/01/putty-settings.html):

*   Font: Terminal, 6-point or Monospace Regular 10 pt.
*   Default Foreground Color="0,255,0"
*   Default Bold Foreground="255,255,255"
*   Default Background="0,55,0"
*   Default Bold Background="85,85,85"
*   Lines of scrollback: 9999
*   Rows: 100
*   Columns: 100

Not sure how to resize automatically to 80x43?

*   Using gconf-editor does [not](http://ubuntuforums.org/showpost.php?s=7135b252713fdc284836990e607b7154&p=7690034&postcount=5) seem to work
*   Changed command of Terminal to "gnome-terminal --geometry=80x43"

_Install Eclipse Extensible Tool Platform and Java IDE _  

_via Software Center_

*   Search for Eclipse Extensible Tool Platform and Java IDE
*   Select, then select button Install
*   Done; close Software Center