---
layout: post
title: Minimum vim Configuration
description: A developer's minimal .vimrc configuration.
---

As a person that uses `vim` and `vi` on a daily basis, I find a custom .vimrc 
absolutely essential to my workflow (kudos to those that survive without it). 
I do feel, however, that most ~/.vimrc files are bloated and overly complex, 
defeating the purpose of using a minimalistic text editor like `vim` in the 
first place. It has taken me almost a year, but I think I have refined my 
configuration file to the "absolute minimum" number of custom settings that I 
can comfortably live with:

{% gist c6a62e3313df2618e1be62884ce9e677 .vimrc %}

Deciphering Each Parameter
--------------------------

The above .vimrc file is nice and short, but incredibly cryptic. Let's try to
decipher the meaning of each parameter.

|abbreviation                |parameter    |description               |
|----------------------------|-------------|--------------------------|
|`nocp`|`nocompatible`|This changes the values of a LOT of options, enabling features which are not Vi compatible but really really nice.|
|`ai`|`autoindent`|Automatic indentation.|
|`ru`|`ruler`|Shows the "ruler" for the cursor (i.e. its current position with line+column and the percentage within the buffer).|
|`sc`|`showcmd`|Show the input of an *incomplete* command.|
|`wmnu`|`wildmenu`|Make use of the "status line" to show possible completions of command line commands, file names, and more.|
|`noet`|`noexandtab`|When inserting text do not expand TABs to spaces. While I try to avoid all control characters in text I can make good use of TABs when typing a table. And I know I can always make Vim expand the TABs later (using the `:retab` command).|
|`nosol`|`nostartofline`|Prevent the cursor from changing the current column when jumping to other lines within the window.|
|`nowrap`|`nowrap`|Turn off automatic wordwrapping.|
|`bs=2`|`backspace`|Backspace with this value allows to use the backspace character (aka CTRL-H or "<-") to use for moving the cursor over automatically inserted indentation and over the start/end of line.|
|`fo=cqrt`|`fold`|This allows one to add text to a comment and still be within the comment after you start a new line. It also allows to break the line within a comment without breaking the comment.|
|`shm=at`|`shortmess`|This shortens about every message to a minimum and thus avoids scrolling within the output of messages and the "press a key" prompt that goes with these.|
|`tw=72`|`textwidth`|This explicitly sets the width of text to 72 characters.|
|`ww=<,>,h,l,[,]`|`whichwrap`|Sets the default cursor behavior when reaching the beginning or end of a line.|
|`com=b:#,:%,n:>`|`command`|Reformat text and preserve comments.|
|`list`|`list`|Enables the lists feature, which is a neat way to visualise tabs, spaces, and line endings.|
|`lcs=tab:>-,trail:~,extends:^`|`listchars`|Determines the strings that will be used when list mode is active.|
