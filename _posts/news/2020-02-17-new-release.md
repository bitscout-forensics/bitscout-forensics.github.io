---
layout: post
title: New Major Relase
date: 2020-02-15
category: news
author: vitaly
short-description: Bitscout 20.04 is ready!
---

-----

# New Bitscout Release #  
We are glad to announce that the first version of Bitscout 20.04 is ready. Based on Ubuntu 20.04 (Focal Fossa) available for developers since January 2020 new Bitscout is even more compatible with variety of hardware, and includes updated forensic tools. In this release we have moved away from LXD container management which used to be an overhead in the past versions. The new container is based on systemd-nspawn feature which is already part of OS anyway.

To build Bitscout 20.04 you may use Ubuntu 20.04, but it also works fine on older Ubuntu 18.04 too.

Some of the recently implemented features we added include memory watchdog. The watchdog service runs on the host system and every 5 seconds checks available free RAM. If the available RAM goes lower than the threshold value (10% by default) it gently suspends all container processes. The processes will be automatically resumed once the RAM level is restored above 10%. This is currently experimental feature and we yet to find the best way to free leaked or overused memory with the help of system owner, but currently the owner is expected to follow the expert guidance.

In case of emergency or to give expert a chance to free some memory within container a `container-resume.sh` command started on the host system may forcedly resume container. Likewise, the container may be suspended manually with `container-suspend.sh` command from the host.

The watchdog service is implemented as a shell script located in `/sbin/memwatchdog.sh`.
