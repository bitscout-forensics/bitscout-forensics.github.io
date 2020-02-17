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

[Bitscout 20.04 MINIMAL](https://mega.nz/#!X5Am2KaS!sMFReC7gUVvmwCuKxmdxPZulhHnfnS5uqRQjS0VHZHQ){: .btn .btn-red }  
**Size:** 522MB  
**Description:** This image includes bare minimum of linux kernel, modules, firmware and contain almost no tools. The minimal build is used when you need to transfer the image fast and install the tools in the RAM after Bitscout is booted. Note that the tools will need to be re-installed every time Bitscout is rebooted.  
**SHA256:** fde7b63089dafb7b8c0ecc4f07e6a033713e639215b4f1943ab5bc81b4751a05

[Bitscout 20.04 BALANCED](https://mega.nz/#!2xJQxKDa!zWlLVr3SKFdsSv1cLFds6rAXmfNWmk-kaIAolNzVkvI){: .btn .btn-red }  
**Size:** 614MB  
**Description:** This image includes some of the most essential forensic tools on top of minimal build. If it doesn't contain your tools, you may add them manually to keep the ISO size relatively small or go for the largest build below.  
**SHA256:** c305464c5ea7b009e309c34900faa581790a5490925c8a9fadb6203c09b19943

[Bitscout 20.04 FULL](https://mega.nz/#!75Qm1axC!yJXjE9xKwT8TG3SDmLhPHZoGRtn9l_tFUcVnoQNBbrU){: .btn .btn-red }  
**Size:** 1.5GB  
**Description:** This image contains forensics-all meta-package from Ubuntu, which contains merely all command-line forensics tools available from official repositories. In addition, it is extended with few other open-source tools which didn't make it to the OS repositories, such as Loki, RegParser, and more.  
**SHA256:** cf1b1391a8ef9797b21b039d48157f1d48451337d1e62488ee608f485a67101b


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
