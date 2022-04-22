---
layout: post
title: New Major Release (22.04)
date: 2022-04-22
category: news
author: vitaly
short-description: Bitscout 22.04 is ready!
---

-----

# New Bitscout 22.04 Release #  
The new Ubuntu 22.04 (LTS) was released yesterday, so we have upgraded our base system to the latest version. Bitscout 22.04 is avaiable as a dedicated branch on Github. Following the latest Ubuntu releases makes it more compatible with modern hardware, but also includes the latest forensic tools. 

In this release we would like to feature a new type of build: a Bitscout with persistence. Now you can install Bitscout on USB and make preserve filesystem changes even after the system is restarted. The old readonly ISO build is still available should you need to have true readonly media. And if you have access to the Bitscout host system, you may easily revert all the changes by removing all files inside persistence partition (mounted as /persistence on the host system).

To put Bitscout on a USB drive with persistence, make sure you build a raw format image (set GLOBAL_TARGET="raw" in ./config/bitscout-build.conf). After that dd-trasnfer it to your USB drive!

In case you want to use Bitscout on a virtualized environment, you can also build VM disks now in qcow2 (for QEmu) and VMDK for VirtualBox or VMware Workstation (see GLOBAL_TARGET value options in ./config/bitscout-build.conf).

If you need an older Bitscout variant based on Ubuntu 16.04, 18.04, 20.04 - those are still available on Github under respective branches. However, to build them, we recommend to use the corresponding Ubuntu version (Ubuntu 20.04 for the Bitscout 20.04, etc).

If you want to try 22.04 quickly, feel free to use our [pre-build images](/quick-try/prebuilt-images), which we have prepared for you in three variants.



