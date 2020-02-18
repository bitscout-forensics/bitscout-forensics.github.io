---
layout: post
title: Download Pre-Built Images
date: 2020-02-16
category: quick-try
author: vitaly
short-description: Where to download sample Bitscout ISO image
---

-----

### PRE-BUILT IMAGES ###   
Note: We do not recommend to use pre-built images for any of your real operations. But you may quickly fetch one of those and try Bitscout on a test VM without building the ISO yourself. If you find it useful and manage to do some basic things, make sure you learn some advanced techniques and then move to building your own custom image.

Here is the list of pre-build images for your convenience  

[Bitscout 20.04 MINIMAL](https://mega.nz/#!P1hRwYDC!3UayKZ2Owqwt7T6uYvQ_VF4-wm2Rsi9OQFJxdMjotf4){: .btn .btn-red }  
**Size:** 522MB  
**Description:** This image includes bare minimum of linux kernel, modules, firmware and contain almost no tools. The minimal build is used when you need to transfer the image fast and install the tools in the RAM after Bitscout is booted. Note that the tools will need to be re-installed every time Bitscout is rebooted.  
**SHA256:** 9aed3e0a7e8b8516b8b7d508f8e02e1dc7a53fb328cffe8959a41dc3ab71b2d7

[Bitscout 20.04 BALANCED](https://mega.nz/#!3ohHxaqR!oqqEHeh3LNthRhUkLzJl1rY8_BgXDkg1sspaMbQjWz4){: .btn .btn-red }  
**Size:** 614MB  
**Description:** This image includes some of the most essential forensic tools on top of minimal build. If it doesn't contain your tools, you may add them manually to keep the ISO size relatively small or go for the largest build below.  
**SHA256:** 55517cda8819bc77a4659daa4d5463041d38629e5b22701e629190399fd9ef98

[Bitscout 20.04 FULL](https://mega.nz/#!3swnAYRS!3UjkrpSMUd-sovwiSm0Ooh4RduFt-PDbpKKzh3PeauM){: .btn .btn-red }  
**Size:** 1.5GB  
**Description:** This image contains forensics-all meta-package from Ubuntu, which contains merely all command-line forensics tools available from official repositories. In addition, it is extended with few other open-source tools which didn't make it to the OS repositories, such as Loki, RegParser, and more.  
**SHA256:** 1f51a8b66c64cee36f4eeb65d5df7065653053892d2b4d6f8d31e2f932403e3c


### GETTING ACCESS ###   
Once the demo system is started you should be able to connect to Bitscout over SSH. All you need to know is the IP address of the booted system. You may find it in the settings of eth0 interface as outputed by the Bitscout management tool on VM screen: go to STATUS menu to find the network interfaces status.

Connecting to Bitscout (i.e. VM IP: 192.168.0.2):  
`$ ssh user@192.168.0.2`

Once you connected, you may become 'root' (pseudo-root, in fact):  
`$ sudo -i`  
Enter empty password (just press ENTER).

To connect to host system of Bitscout, simply use port 23:  
`$ ssh -p23 user@192.168.0.2`   
Similarly, there is no password required for 'user' account, which can run superuser commands using sudo.
