---
layout: post
title: A few of my favorite bash aliases.
description: A collection of my frequently used utilitiy aliases.
---

When you are an every day Linux user, it's hard not to have a few command
aliases. Aliases make commands shorter and life easier, so and why not take 
advantage of the feature! Here are a few of my favorites...

## My Every Day Commands (EDC)

From file manipulation to just browsing my filesystem, i cannot live without
these.

```shell
alias ..="cd .."
alias ll="ls -al"
alias vi="vim"
```

## Development and Programming

Pastebins are a convenient tool for troubleshooting and sharing large log files.

```shell
alias ix=" | curl -F 'f:1=<-' ix.io"
```

## File Compression

```shell
alias untar="tar -xvf"
```
