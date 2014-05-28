---
layout: post
title: "Vim for Writing"
date: 2014-05-08
comments: true
categories: []
---
Vim is an amazing piece of software for editing text, and that isn't limited to just programming. Here are some bits from my `.vimrc` that make writing in Vim easier.

```vim
" Enable the mouse
set mouse=a

" Turn on soft wraping and only break between words
set wrap
set linebreak

" Use the arrow keys to move through soft wrapped lines
imap <Down> <C-o>gj
imap <Up> <C-o>gk

" Move to next line when using left and right
set whichwrap+=<,>

" Turn on spell checking for all .txt, .md, and .markdown files
au BufNewFile,BufRead,BufEnter *.txt,*.md,*.markdown setlocal spell spelllang=en_us

" Highlight .md files as markdown
au BufRead,BufNewFile *.md set filetype=markdown

" Make space toggle folds
" This is useful if you use https://github.com/nelstrom/vim-markdown-folding
nnoremap <Space> za
```

If you really want to get serious about using Vim for writing check out [Vim for Writers](http://naperwrimo.org/wiki/index.php?title=Vim_for_Writers).
