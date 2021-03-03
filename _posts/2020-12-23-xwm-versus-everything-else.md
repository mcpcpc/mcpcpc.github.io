---
layout: default
title: xwm Versus Everything Else
---

xwm Versus Everything Else
==========================

A comparison of xwm to mainstream window manager solutions.

Overview
--------

A question that I am frequently asked is, "how does xwm compare to *X*"? The
reality is that there is no straightforward answer. In most cases, comparing
xwm to any window manger is like comparing *apples* to *oranges*. [0]

Why is that so? Let's a take a look.

The Competition
---------------

Let's begin by comparing high-level features for several actively developed 
(and frequently referred to as "minimal") window manager solutions:

|feature               |cwm     |tinywm  |xwm     |evilwm  |dwm     |bspwm |
|:---------------------|:------:|:------:|:------:|:------:|:------:|:----:|
|cloc                  |6328    |115     |339     |3257    |2505    |11909 |
|protocol              |Xlib    |Xlib    |XCB     |Xlib    |Xlib    |XCB   |
|license               |ISC     |Public  |MIT     |MIT     |MIT     |BSD   |
|language              |C       |C       |C       |C       |C       |C     |
|release year          |2004    |2005    |2020    |2000    |2006    |2013  |
|type                  |stacking|floating|floating|stacking|dynamic |tiling|
|themeable             |yes     |no      |yes     |yes     |yes     |no    |
|virtual desktops      |no      |no      |no      |yes     |yes     |yes   |
|window switching panel|no      |no      |no      |no      |yes     |no    |

This information provided above is pretty generic, but there are some key
takeaways:

*   There are two main X protocols used for window manager development: Xlib
    and XCB. XCB is the faster and (arguably) preferred X protocol for
    developers. Refer to the "The X New Developer's Guide: Xlib and XCB" [1]
    for a more detailed comparison.
*   While choosing one protocol does not necessarily translate to a better
    user experience, choosing the more modern protocol ensures better long-
    term support for the life of the project.
*   There is a pretty big difference in the cloc [2] footprint, so it’s
    difficult to compare these from a feature perspective as xwm is
    considered a “minimum viable solution” and the rest offer a more full-
    featured user experience. However, like dwm, xwm is a framework for
    developers to patch and enhance. So there is nothing stopping users or
    developers from making xwm more like the rest.

The Philosophy Behind xwm
-------------------------

The philosophy behind xwm is fairly straight forward:

**Less Is More**. From a sheer dependency standpoint, xwm has fewer than the
rest. There are obvious drawbacks to this, but I intentionally left xwm as
"barebones" as possible, to allow the community to expand, patch, tweak
andmodify. This is consistent with the Suckless Philosophy of programming.
[3]

**No Configuration File Clutter**. I have opted not to have a run-time
configuration file in xwm. Everyone seems to have a configuration file these
days that is either placed in an obscure directory, "hidden" from plain site
or cluttering the home directory. I hate configuration files (and they hate
me). Not doing so forces the user to glimpse into the source which, to me, is
a habit that all existing and new Unix users should be doing.

**Empower The User To Create Their Own Experience**. I provide no out-of-box
multi-monitor support, no menu bar, no title bars, no tab	focus or or any
other feature that a regular user would find essential. Instead, these
features will be offered as patches, which the user must learn how to apply
themselves.

Conclusions
-----------

xwm is not for everyone. I feel that the target audience is niche and those
of that audience will appreciate what xwm attempts to accomplish. With that
said, I would welcome veterans and newbies alike to try xwm out and let me
know their thoughts. I am always open to suggestions and ideas for improving
xwm or counter arguments to anything I have stated in this article.

[0]: http://github.com/mcpcpc/xwm
[1]: https://www.x.org/wiki/guide/xlib-and-xcb/
[2]: https://github.com/AlDanial/cloc
[3]: https://suckless.org/philosophy
