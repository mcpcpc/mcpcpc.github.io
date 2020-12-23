---
layout: post
title: xwm vs The World
description: A comparison of xwm to mainstream window manager solutions.
---

A question that I am frequently asked is "How does xwm compare to X". The
reality is that there is no straightforward answer. In most cases, comparing xwm
to any window manger is like comparing *apples to oranges*. You might be asking
yourself, why is that so? Let's begin by looking at a high-level feature 
comparison for some of the mainstream solutions that are actively developed and
frequently referenced as "minimal" window manager solutions:

|feature               |cwm     |tinywm  |xwm     |evilwm  |dwm     |bspwm   |
|----------------------|--------|--------|--------|--------|--------|--------|
|cloc                  |6328    |115     |349     |3257    |2505    |11909   |
|protocol              |Xlib    |Xlib    |XCB     |Xlib    |Xlib    |XCB     |
|license               |ISC     |Public  |MIT     |MIT     |MIT     |BSD     |
|language              |C       |C       |C       |C       |C       |C       |
|release year          |2004    |2005    |2020    |2000    |2006    |2013    |
|type                  |stacking|floating|floating|stacking|dynamic |tiling  |
|themeable             |yes     |no      |yes     |yes     |yes     |no      |
|virtual desktops      |no      |no      |no      |yes     |yes     |yes     |
|window switching panel|no      |no      |no      |no      |yes     |no      |

Some key takeaways from this table:

*   There are two main X protocols used for window manager development: Xlib
    and XCB. However, XCB is the more modern and (arguably) preferred X protocol.
	Refer to [The X New Developer's Guide: Xlib and 
	XCB](https://www.x.org/wiki/guide/xlib-and-xcb/) for a more in-depth 
	comparison.
*   There is a pretty big difference in the cloc footprint, so it’s difficult to
    compare these from a feature perspective as xwm is considered a “minimum
    viable solution” and the rest offer a more full-featured user experience.
	However, like dwm, xwm is a framework for developers to patch and enhance.
	So there is nothing stopping users or developers from making xwm more like
	the rest.

## The Philosophy Behind xwm

The philosophy behind xwm is fairly straight forward.

### Less Is More

From a sheer dependency standpoint, xwm has fewer than the rest. There are
obvious drawbacks to this, but I intentionally left xwm as "barebones" as
possible, to allow the community to expand, patch, tweak and modify. This is
consistent with the Suckless Philosophy of programming
(https://suckless.org/philosophy/), which is based on the Unix Philosophy of
programming.

### No Configuration File Clutter

I have opted not to have a run-time config file in xwm. Everyone seems to
have a config file these days that is either placed in an obscure directory,
"hidden" from plain site or cluttering my home directory. I hate config files
(and they hate me). Not doing so forces the user to glimpse into the source
which, to me, is a habit that all existing and new Unix users should be doing.

### Empower The User To Create Their Own Experience

I provide no out-of-box multi-monitor support, no menu bar, no title bars, no tab
focus or or any other feature that a regular user would find essential. Instead, 
these features will be offered as patches, which the user must learn how to apply
themselves.

## Conclusions

xwm is not for everyone. I feel that the target audience is niche and those of
that audience will appreciate what xwm attempts to accomplish. With that said, I would welcome veterans and newbies alike to try xwm out and let me know their thoughts. I am always open to suggestions and ideas for improving xwm or counter arguments to anything I have stated in this article. 
