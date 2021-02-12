---
layout: post
title: "netcat: The Only IRC Client Anyone Needs"
description: Configuring a cpu, auth and fs server on the 9front operating system using Linode virtual machine.
---

I am writing this after having spent the past year developing a more-than-functional C-based IRC client, kirc, and reflecting on my journey up until this point. The ugly truth is that kirc was never the IRC client i *wanted* to develope. Instead, it became the application I *needed* to develope in order to enhance my understanding of the C-programming language and IRC protocol. Having grown accustomed to working and manipulating the raw IRC data stream, I can finally revisit the question that started me on this journey: what is the ideal IRC client?

To answer this, I would like to start by listing the characteristica that i find define essential of any IRC client:

* persistent session , automatic PING response.
* 

Not that this list does not take into account multi-channel support or more advanced features that others might deem "essential". 