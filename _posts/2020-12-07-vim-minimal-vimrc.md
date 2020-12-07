---
layout: post
title: A develeoper's minimum vim configuration file
description: A detailed explanation of my current minimal .vimrc file.
---

As a person that uses `vim` on a daily basis, I find it nearly I
impossible to use without some additional configuration (kudos to those
that can). However, I do feel that most `vi`m configuration files are
overly complex and completely defeat the purpose of using a minimalistic
text editor like `vim` in the first place. It's taken me almost a year,
but I think I have refined my config file to the absolute minimum number
of custom settings that I require on a daily basis. Below, I have
provided my raw ~/.vimrc configuration file, along with an explanation
on specific settings that new `vim` users might find confusing (or click
[here](.vimrc) for a complete explanation):

```vimrc
set nocp ai hls ru sc vb wmnu noeb noet nosol nowrap
set fo=cqrt shm=at tw=72 ww=<,>,h,l,[,] com=b:#,:%,n:>
set list lcs=tab:»·,trail:·,extends:^
```

## The breakdown

The above configuration file is nice and short, but what does each
parameter exactly do?


|abbreviation                |parameter    |description               |
|----------------------------|-------------|--------------------------|
|ai                          |autoindent   |Automatic indentation.|
|nocp                        |nocompatible |This changes the values of a LOT of options, enabling features which are not Vi compatible but really really nice.|
|hls                         |hlsearch     |With the defaults, setting this option causes all text matching the current search to be highlighted using the Search highlight group, which adds a yellow background to the current highlighting.|
|ru                          |ruler        |Shows the "ruler" for the cursor (i.e. its current position with line+column and the percentage within the buffer).|
|sc                          |showcmd      |Show the input of an *incomplete* command.|
|vb                          |visualbell   |Chose "visual bell" effect rather than "beeping".|
|wmnu                        |wildmenu     |Make use of the "status line" to show possible completions of command line commands, file names, and more.|
|noeb                        |noerrorbells |Turn off the bell. You do know the "beep" you get when you type ESC in normal mode?|
|noet                        |noexandtab   |When inserting text do not expand TABs to spaces.|
|nosol                       |nostartofline|Prevent the cursor from changing the current column when jumping to other lines within the window.|
|nowrap                      |nowrap       |Turn off automatic wordwrapping.|
|bs=2                        |backspace    |Backspace with this value allows to use the backspace character (aka CTRL-H or "<-") to use for moving the cursor over automatically inserted indentation and over the start/end of line.|
|fo=cqrt                     |fold         |This allows one to add text to a comment and still be within the comment after you start a new line. It also allows to break the line within a comment without breaking the comment.|
|shm=at                      |shortmess    |This shortens about every message to a minimum and thus avoids scrolling within the output of messages and the "press a key" prompt that goes with these.|
|tw=80                       |textwidth    |This explicitly sets the width of text to 72 characters.|
|ww=<,>,h,l,[,]              |whichwrap    |Sets the default cursor behavior when reaching the beginning or end of a line.|
|com=b:#,:%,n:>              |command      |Reformat text and preserve comments.|
|list                        |list         |(coming soon...)|
|lcs=tab:»·,trail:·,extends:^|listchars    |(coming soon...)|
