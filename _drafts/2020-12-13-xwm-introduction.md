---
layout: default
title: Why Use Small Window Managers
description: A brief argument for xwm as a primary window manager.
---

When I first started looking at window managers (WM) ~2 years ago, I noticed a
consistent trend amongst the ones that came recommended to me. First, most used
the Xlib protocol, which is archaic in comparison to other protocols such as X 
Protocol C Binding (XCB). The second issue being that most appeared to have 
fairly large code-bases and yet offered arguably no advantage over the smaller 
projects. For comparison sake, let's take a look at a few of the more "popular" 
minimal X Server window managers:

|feature               |cwm     |tinywm  |xwm     |evilwm  |dwm     |bspwm   |
|----------------------|--------|--------|--------|--------|--------|--------|
|cloc                  |6328    |115     |357     |3257    |2505    |11909   |
|protocol              |Xlib    |Xlib    |XCB     |Xlib    |Xlib    |XCB     |
|license               |ISC     |Public  |MIT     |MIT     |MIT     |BSD     |
|language              |C       |C       |C       |C       |C       |C       |
|release year          |2004    |2005    |2020    |2000    |2006    |2013    |
|type                  |stacking|floating|floating|stacking|dynamic |tiling  |
|themeable             |yes     |no      |no      |yes     |yes     |no      |
|virtual desktops      |no      |no      |no      |yes     |yes     |yes     |
|window switching panel|no      |no      |no      |no      |yes     |no      |

