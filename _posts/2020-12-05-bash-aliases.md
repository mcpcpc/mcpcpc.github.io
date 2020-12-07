---
layout: post
title: Bash Command Aliases
description: A collection of my frequently used utilitiy aliases.
---

When you are an every day Linux user, it is hard not to have a few Bash
command aliases. Aliases make commands shorter and life easier, so and why not
take advantage of the feature! Here are a few of my favorites...

## Navigation and Editting

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
