---
layout: default
title: "Netcat: The One True IRC Client"
---

Netcat: The One True IRC Client
===============================

A justification for using netcat as an IRC client, including an example IRC
client wrapper script.

Overview
--------

I am writing this after having spent the past year developing a "more than
functional" C-based IRC client, [kirc](http://github.com/mcpcp/kirc), and
reflecting on my journey up until this point. The ugly truth is that kirc was
never the IRC client I *wanted* to develope. Instead, it became the client I
*needed* to develope in order to enhance my understanding of the C
programming language and [RFC1459](https://tools.ietf.org/html/rfc1459)
protocol. Now, having grown accustomed to working and manipulating the raw
IRC data stream, I can finally revisit the question that started me on this
journey, which is *what makes an ideal IRC client*?

Essential Characteristics
-------------------------

To answer this, I would like to start by listing the attributes that I find
essential for any CLI-based client:

1.  Persistent session management, via automatic keep-alive response (a.k.a.
    `PING<>PONG`).
2.  Command aliasing, which covers the scope of basic/frequently used
    commands (e.g. `PRIVMSG`, `JOIN`, `PART`, etc).
3.  Ability to pipe/fork and daemonize the application for third-party
    application development, chat logging, bots or direct TTY manipulation.

Note that this list does not take into account multi-channel support or more 
advanced features that others might be deemed essential. However, based on
this limited list, I think anyone can develop a half-decent client that can
be extended to accommodate more advanced features through scripting. If we
look at the current Linux tools that ship with a modern OS, there is an
arsenal of utilities that we can leverage to create such a tool.  One of
particular interest is `netcat`, which is the "swiss army knife" for reading
from and writing to network connections using TCP or UDP. Furthermore, it
easily checks the third attribute listed above. The question becomes, how do
we accommodate for the first two attributes in the list?  We create a wrapper
shell script, of course!

Wrapping It Up
--------------

I will save you the headaches and research and just share the wrapper script
I have created and affectionately named `irc2`. This script is also available
on [Github](http://github.com/mcpcpc/irc2) for the community to further
refinement. 

<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fmcpcpc%2Firc2%2Fblob%2Fmaster%2Firc2&style=github"></script>

In ~39 cloc, we have a script that checks all of the boxes on my list and
works on 99% of POSIX-compliant shells.  Nifty, eh?

Chat History Logging
--------------------

There are a couple of ways of going about this, but one that I recently 
discovered is the built-in `script` function, which is meant for creating
transcripts of tty sessions.

    script -a -c irc2 chat_log.txt

Credit
------

Special thanks to aarng (for showing we the ways of `-e`) and all the users
on the *#kisslinux* IRC channel for the continuous feedback and suggestions.
