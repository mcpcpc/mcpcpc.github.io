---
layout: post
title: "Netcat: The One True IRC Client"
description: A justification for using netcat as an IRC client, including an example IRC client wrapper script.
---

I am writing this after having spent the past year developing a "more than functional" C-based IRC client, [kirc](http://github.com/mcpcp/kirc), and reflecting on my journey up until this point. The ugly truth is that kirc was never the IRC client I *wanted* to develope. Instead, it became the client I *needed* to develope in order to enhance my understanding of the C-programming language and [RFC1459](https://tools.ietf.org/html/rfc1459) protocol. Now, having grown accustomed to working and manipulating the raw IRC data stream, I can finally revisit the question that started me on this journey, which is *what makes an ideal IRC client*?

## Essential Characteristics

To answer this, I would like to start by listing the attributes that I find essential for any CLI-based client:

1. Persistent session management, via automatic keep-alive response (a.k.a. `PING<>PONG`).
2. Command aliasing, which covers the scope of basic/frequently used commands (e.g. `PRIVMSG`, `JOIN`, `PART`, etc).
3. Ability to pipe/fork and daemonize the application for third-party application development, chat logging, bots or direct TTY manipulation.

Note that this list does not take into account multi-channel support or more advanced features that others might be deemed essential. However, based on this limited list, I think anyone can develope a half-decent client that can be extended to accomodate more advanced features through scripting. If we look at the current Linux tools that ship with a modern OS, there is an arsenal of utilities that we can leverage to create such a tool.  One of particular interest is `netcat`, which is the "swiss army knife" of reading from and writing to network connections using TCP or UDP. Furthermore, it easily checks the third attribute listed above. The question becomes, how do we accomodate for the first two attributes in the list?  We create a wrapper shell script, of course!

## Wrapping It Up

I will save you the headaches of and research that I put into developing a shell wrapper script and just share the one I have created and affectionately named `irc2`. This script is also available on [Github](http://github.com/mcpcpc/irc2) for the community to further refinement. 

<script src="http://gist-it.appspot.com/https://github.com/mcpcpc/irc2/blob/master/irc2"></script>

In ~39 CLOC, we have a script that checks all of the boxes on my list and works on 99% of POSIX-compliant shells.  Nifty, eh?

## Next Steps

So what can we do with this script? Well, that's entirely up to the user. Here are a few to get you started.

### Chat History Logging

There are a couple of ways of going about this, but one that i recently discovered is the built-in `script` function, which is meant for creating transcripts of tty sessions.

```shell
script -a -c irc2 chat_log.txt
```
