---
layout: default
title: home
---

mcpcpc's buffer
===============

My name is Michael Czigler and I create minimum viable solutions written in the C
programming language. This site is intended to be a "buffer", a temporary medium
for sharing my thoughts and ideas, with the hope that someone may one day finds 
these musings helpful.

Projects
--------

All source files for my projects are hosted on GitHub. You can support them if you
like by donating [here](https://www.paypal.me/mcpcpc/usd5).

*   [xwm](https://github.com/mcpcpc/xwm) ~ XCB floating window manager</li>
*   [xbar](https://github.com/mcpcpc/xbar) ~ XCB information bar</li>
*   [kirc](https://github.com/mcpcpc/kirc) ~ POSIX C99 IRC client</li>

Contact
-------

Send mail to <a href="mailto:%69%6e%66%6f%40%6d%63%70%63%70%63%2e%63%6f%6d">me</a>
or any one of the following:
[hackernews](https://news.ycombinator.com/user?id=mcpcpc) 
[reddit](https://www.reddit.com/user/mcpcpc), or 
[github](https://github.com/mcpcpc).

Latest Posts
------------

{% for post in site.posts %}*   {{ post.date | date_to_string }} [{{ post.title }}]({{ post.url }}){% endfor %}