---
layout: post
title: Creating a Minimal Desktop From Scratch
description: A beginners guide to creating a minimal custom desktop.
---

For the purpose of this guide, I will try to create a minimal desktop
environment that can be adapted to suite the end-user's purpose and
desired "look-and-feel". In order to get started, I would recommend
installing the following applications:

*   [xwm](https://github.com/mcpcpc/xwm) - A tiny XCB window manager.  
*   [imagemagick](https://imagemagick.org) - A free and open-source 
    cross-platform software suite for displaying, creating, converting, 
    modifying, and editing raster images. In this tutorial, we will be
    using it to set the root window background image, control it's 
    placement and scaling.
*   [lemonbar](https://github.com/LemonBoy/bar) - A lightweight status 
    bar that we will use to display important metrics, such as battery 
    level, volume and time.
    
I will also assume that you already have a working X server installed
and have some familiarity with shell scripting.  

## Creating a Status Bar

```bash
#!/bin/bash

DELAY=0.2

while true; do
    output="";

    # Center Align
    output="${output}%{c}"

    # Right Align
    output="${output}%{r} "

    # Left Align
    output="${output}%{l} "

    # Wifi
    essid=$(iwgetid | cut -d \" -f 2)
    if [[ "$essid" != "" ]]; then
    output="${output}net %{F#505050}$(iwconfig wlp2s0 | grep Quality | cut -d = -f 2 | cut -d / -f 1)%"
    fi


    # Center Align
    output="${output}%{c}"

    # Volume
    master="$(amixer | head -1 | cut -d "'" -f 2)"
    output="${output}%{A4:amixer -q sset ${master} 1%+:}%{A5:amixer -q sset ${master} 1%-:}"
    output="${output}%{F#888888}vol %{F#505050}$(amixer get ${master} | tail -1 | cut -d \[ -f 2 | cut -d \] -f 1)"
    output="${output}"

    # Padding between Volume and Battery life
    output="${output} "

    # Battery
    output="${output}%{F#888888}batt%{F#505050} $(acpi | cut -d , -f 2 | cut -d " " -f 2)"


    # Right Align
    output="${output}%{r} "
    # Time
    #12 hour time
    #time=$(date | cut -d " " -f 5)
    #time=$(date + "%r")
    #24 hour time
    time=$(date +"%T")
    output="${output}%{F#888888}%{F#505050}${time//:/%\{F\#888888\}:%\{F\#505050\}}"

    echo " ${output} ";sleep $DELAY;
done | lemonbar -f "DejaVu Sans Mono:size=8" -d -g 225x20+845+1052 -B \#ffffff -F \#888888 | /bin/zsh
```
