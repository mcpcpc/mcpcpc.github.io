---
layout: default
title: Why Use Small Window Managers
description: A brief argument for xwm as a primary window manager.
---

When I first started looking at window managers ~2 years ago, I noticed a 
consistent trend amongst the ones that came recommended to me. Let's begin by 
first comparing a few of the more "popular" minimal X server window managers:

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

From a protocol perspective, most are still using the Xlib protocol, which is 
archaic in comparison to other protocols such as X Protocol C Binding (XCB). The
X.org Foundation even wrote an article explaining the differences and why XCB
should be preferred (seen [here](https://www.x.org/wiki/guide/xlib-and-xcb/)).

The second issue being that most appear to have fairly large code-bases and yet 
offer arguably no advantage over the smaller projects. Instead, they offer only 
cosmetic features that do little to enhance the user experience or usability. So
why choose `bspwm` over `dwm`?  Why `cwm` over `tinywm` or `xwm`? I see no 
reasonable argument other than user preferences or conventions that some users 
have grown accustomed to. 

The truth is `xwm`, `tinywm` and even `evilwm` are entirely usable on their own
and investing in anything larger is a waste of time and resources, not to 
mention deviates further from the Unix philosophical ideal.

