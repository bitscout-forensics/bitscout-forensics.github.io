---
layout: post
title: Custom Kernel Build is Back
date: 2020-02-15
category: news
author: vitaly
short-description: Major fix enabled applying your own kernel patches
---

-----

# Custom Kernel Build #  
We figured that one rarely used, but yet very important feature got broken with appearance of new kernel versions. That is the feature linked to the following question during the first run of Bitscout build:
<p class="terminal">
<br/>
If you are going to deal with badly unmounted filesystems, software RAID or LVM, it is recommended to apply kernel write-blocker patch for extra care of the evidence. However, please note that this is eperimental feature and may take 3-4 hours to rebuild the kernel on a single-core CPU.
Would you like to build and use kernel with write-blocker? [y/N]:
<br/> 
</p>

By default it is set to 'No', which skips building custom kernel and proceeds with binary kernel provided by the upstream. But if you want to turn on certain kernel option, extend or even reduce support for some hardware, you may need to use this option. Currently, we use it only to apply one small patch for the kernel: write-protection patch. The patch, based on amazing [Linux write blocker research](https://github.com/msuhanov/Linux-write-blocker) by [Maxim Suhanov](https://github.com/msuhanov), makes sure that certain filesystem, software RAID, LVM and potentially other pieces of code cannot modify read-only protected evidence drives. As Maxim previously demonstrated, filesystem and LVM error-fixing routines may change metadata on the disk, causing disk write operations. If you have to deal with real evidence drive and make sure that not a single bit is flipped on it, even if the software fails, you should be using the patch we provide with Bitscout. 
However, you may also want to supply your kernel config or apply some additional patch. If you have done this before and you know what you are doing, take a look in `./scripts/chroot_install_kernel.sh` script inside Bitscout build directory to automatically apply your patches during Bitscout custom kernel build.

Switching from standard kernel to custom kernel build after you initialized build directory is easy, simply set GLOBAL_CUSTOMKERNEL variable to 1 in `./config/bitscout-build.conf` file.

Happy kernel hacking!

