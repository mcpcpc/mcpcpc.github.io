---
layout: default
title: Bash Command Aliases
---

Bash Command Aliases
====================

A collection of my frequently used utilitiy aliases.

Overview
--------

SHELL aliases are fun. SHELL aliases are easy! So here are a few to get you
started.

Navigation and Editting
-----------------------

From file manipulation to just browsing my filesystem, i cannot live without
these.

    alias ..="cd .."
    alias ll="ls -al"
    alias vi="vim"

Development and Programming
---------------------------

Pastebins are a convenient tool for troubleshooting and sharing large log
files.

    alias ix=" | curl -F 'f:1=<-' ix.io"

File Compression
----------------

    alias untar="tar -xvf"
