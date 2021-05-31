---
layout: post
title: "Bitscout Cheatsheet"
date: 2021-05-31
category: docs
author: vitaly
short-description: Quick reference to useful commands for Bitscout
---
-----

# Useful commands #  
### Working in Bitscout host shell ###  
* Show IP addresses of existing interfaces: **`ip a s`** 
* Show current DNS settings for eth0: **`resolvconf status eth0`**  
* List running system containers: **`machinectl list`**  
* Check status of expert container: **`machinectl status container`**  
  Note: Use **q** key to exit the viewer
* Stop/start expert container: **`machinectl stop/start container`**  

### Working in Bitscout expert shell ###  
* Create copy-on-write (qcow2) virtual disk based on another device/file:  
  **`qemu-img create -f qcow2 -o backing_file=/dev/host/evidence0,backing_fmt=raw ./evidence0.qcow2`** 
* Create qcow2 virtual disk file based on another qcow2 file:  
  **`qemu-img create -f qcow2 -o backing_file=./evidence0.qcow2,backing_fmt=qcow2 ./layer2.qcow2`** 
* Start basic VM from a qcow2 file (with VNC display):  
  **`qemu-system-x86_64 -enable-kvm -cpu host -m 512 -boot strict=on -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -vnc :0 -vga cirrus`**  
  Note: use a VNC client on your host to connect to Bitscout IP on port 5900
* Start basic VM from a qcow2 file (with SPICE display and SMB file sharing):  
  **`qemu-system-x86_64 -enable-kvm -cpu host -m 512 -boot strict=on -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -spice port=2001,disable-ticketing -vga cirrus -net user,net=10.0.2.3/24,smb=/root/smb,smbserver=10.0.2.4,id=usernet,restrict=y`**  
  Note: use a VNC client on your host to connect to Bitscout IP on port 2001

