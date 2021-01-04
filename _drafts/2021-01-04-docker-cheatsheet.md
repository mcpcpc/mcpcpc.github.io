---
layout: post
title: My Docker Cheatsheet
description: A quick reference sheet for frequently used Docker commands.
---

I use Docker infrequently and, when I do, I find myself having to re-learn how to use it. 
The following is a summary of my more frequent commands:

|Command|Description|
|`docker pull archlinux`|Download a docker image (e.g. Arch Linux).|
|`docker ps -a`|Check running processes, including ones exited.|
|`docker run -t -d --name myarch arclinux`|Run a detachhed process with a name.|
|`docker exec -it myarch bash`|Jump into interactive mode.|
|`docker stop myarch`|Stop a running container/process.|
|`docker rm myarch`|Remove an existing container.|
