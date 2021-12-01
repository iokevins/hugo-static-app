---
title: 'vimrc'
date: 2009-03-01T18:41:00.000-08:00
draft: false
---

se nohlsearch  
se ic  
if (&term == 'xterm' || &term =~? '^screen') && hostname() == 'my-machine'  
    " On my machine, I use an old Konsole with 256 color support  
    set t\_Co=256  
    let g:CSApprox\_konsole = 1  
endif  
se nu  
se tabstop=2  
se shiftwidth=2  
se sw=2  
se expandtab  
se nosol  
se showmode  
se autoindent  
se wrapscan  
se wrap  
se nobackup  
se smartindent  
se title  
se ruler  
se scrolloff=2  
se shortmess=at  
se showcmd  
se showmatch  
se paste  
  
syntax on  
  
highlight cComment ctermfg=2  
highlight cCppOut ctermfg=7  
highlight Comment ctermfg=2  
highlight Directory ctermfg=2  
highlight NonText ctermfg=White  
highlight Preproc ctermfg=7  
highlight String ctermfg=6  
highlight Number ctermfg=3  
highlight Character ctermfg=6  
  
highlight tclComment ctermfg=2  
highlight tclLineContinue ctermfg=2  
  
highlight makeComment ctermfg=2  
highlight vimComment ctermfg=6  
highlight shComment ctermfg=2  
highlight idlComment ctermfg=2  
  
colorscheme koehler  
  
map 0i/\* $A \*/  
  
inoremap # X^H#  
  
UPDATE 2013-02-24: added term color wrapper ([via](http://stackoverflow.com/questions/7989866/how-do-i-get-vim-colorschemes-to-work-in-gnome-terminal))