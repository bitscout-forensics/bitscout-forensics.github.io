---
layout: post
title: Quick Try Bitscout 22.04
date: 2022-04-22
category: quick-try
author: vitaly
short-description: Where to download the newest Bitscout disk images
---

-----

### PRE-BUILT IMAGES ###   
Note: We do not recommend to use pre-built images for any of your real operations. But you may quickly fetch one of those and try Bitscout on a test VM without building the ISO yourself. If you find it useful and manage to do some basic things, make sure you learn some advanced techniques and then move to building your own custom image.

Here is the list of the latest medium-sized pre-built images for various scenarios  

[Bitscout 22.04 ISO](https://mega.nz/file/PtRlSAiT#-TCLPCv0PS6xpbhDwWjXkZ3Ea8sZbDeGi-hYBUn64Z8){: .btn .btn-red }  
**Size:** 980MB  
**Description:** This image includes some of the most essential forensic tools on top of minimal build. If it doesn't contain your tools, you may add them manually to keep the ISO size relatively small or make your own larger build. THis is perfect for quick investigation. It is suitable for being burnt to a CD-ROM disc or used from a USB drive. But if you want to use data persistence (preserve changes after Bitscout restart), checkout other images below.  
**SHA256:** 0d9d3dbbe0ee7d96e70a5028a0b6433f556f47ae867b1019260462d105f1009c

[Bitscout 22.04 RAW](https://mega.nz/file/X8BwHTjL#Kpk-hOswMpy98MYAKFynCp2Ew_zsR8Er4yaj204s5y0){: .btn .btn-red }  
**Size:** 3.3GB  
**Description:** This image includes all the files from the medium size ISO build, but is larger in size, because it contains uncompressed root filesystem and a persistence partiion size. It can be transferred directly to a USB drive using dd tool, or maybe even mounted as a remote disk over HTTP. You may use this image and convert to any other disk format to play in a VM, but if you use VirtualBox, VMware, or QEmu, check out special build below.
**SHA256:** b5f4af064dfe17e7119474b021a76449163001f5265bcaaac2efa722f7ba88c9

[Bitscout 22.04 VMDK](https://mega.nz/file/i1xChTzb#N5XxwG75EeoFfx95NS8CvhatfVWfD1qLhrSMb4jXjXo){: .btn .btn-red }  
**Size:** 2.4GB  
**Description:** This disk image is identical in contents to the RAW disk image build above, but it's more compact due to more optimal way to store unused disk space on a virtual disk. This image should work if you use VirtualBox or VMware Workstation or your VM software supports VMDK disk format.  
**SHA256:** 8d85564030d97cd60ba5dee54ca458436b6f17f530f2464755d73c45f55aedb1

[Bitscout 22.04 QCOW2](https://mega.nz/file/O1ARgIJL#Hk4UyR5yKK9-KELUu5FrKA7cbrBzDiSc1ZXp9LGSkM8){: .btn .btn-red }  
**Size:** 2.4GB  
**Description:** This disk image is identical to the others in contents, but it comes in QCOW2 format for QEmu-based virtualization software. If you are familiar with virsh/virt-manager/libvirt, this is the droid you are looking for!  
**SHA256:** ea2b26256efecceec8950ab19fe9929007d3f9506d0b289b25e0f9b969fc0ee7



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
