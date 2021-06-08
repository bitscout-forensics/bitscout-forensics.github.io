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
* Show IP addresses of existing interfaces:  
**`ip a s`** 
* Show current DNS settings for eth0:  
**`resolvconf status eth0`**  
* List running system containers:  
**`machinectl list`**  
* Check status of expert container:  
**`machinectl status container`**  
Note: Use **q** key to exit the viewer
* Stop/start expert container:  
**`machinectl stop/start container`**  

### Working in Bitscout expert shell ###  
* Create copy-on-write (qcow2) virtual disk based on another device/file:  
**`qemu-img create -f qcow2 -o backing_file=/dev/host/evidence0,backing_fmt=raw ./evidence0.qcow2`** 
* Create qcow2 virtual disk file based on another qcow2 file:  
**`qemu-img create -f qcow2 -o backing_file=./evidence0.qcow2,backing_fmt=qcow2 ./layer2.qcow2`** 
* Start basic VM from a qcow2 file (with VNC and SPICE):  
**`qemu-system-x86_64 -enable-kvm -cpu host -m 512 -boot strict=on -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -vnc :0 -spice port=2001,disable-ticketing -vga cirrus`**  
Note: use a VNC/SPICE client on your host to connect to Bitscout IP on port 2001
Example cmline on Linux:  
  * `remote-viewer spice://192.168.1.1:2001`  
  * `remote-viewer vnc://192.168.1.1:5900`  

* Start Windows10 with 1GB RAM and faster CPU  
**`qemu-system-x86_64 -enable-kvm -cpu host,hv_relaxed,hv_spinlocks=0x1fff,hv_vapic,hv_time -smp 4,sockets=1,cores=4,threads=1 -m 1024 -boot strict=on -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -vnc :0 -spice port=2001,disable-ticketing -vga cirrus`**  

* Start basic VM from a qcow2 file (with SPICE display and SMB file sharing):  
**`qemu-system-x86_64 -enable-kvm -cpu host -m 512 -boot strict=on -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -spice port=2001,disable-ticketing -vga cirrus -net user,net=10.0.2.3/24,smb=/root/smb,smbserver=10.0.2.4,id=usernet,restrict=y`**  
Note: use a VNC client on your host to connect to Bitscout IP on port 2001

* Show qemu process sorted memory map:  
**`cat /proc/$(pgrep qemu)/maps | cut -d' ' -f1 | awk -F- '{print (strtonum("0x" $2)-strtonum("0x" $1))" "$0 }' | sort -n`**  

### Shortcuts and commands for tmux ###  
Super key: **Ctrl+B**  
**\<Super> N** - switch to view N (0-9)  
**\<Super> d** - leave tmux session  
**\<Super> %** - split view into 2 vertical panels  
**\<Super> "** - split view into 2 horizontal panels  
**\<Super> \<ArrowKey>** - move to another panel  

**`tmux ls`** - list existing tmux sessions  
**`tmux a`** - attach to the last tmux session  

### Shortcuts for hexedit ###  
**Tab** - toggle hex/ascii  
**Return** - go to offset  
**Ctrl-C** - exit without saving  
**Ctrl-X** - save and exit  
**Ctrl-S** or **/** - search hex/ascii pattern forward  
**Ctrl-R** - search backward  

### Qemu console commands ###  
**`system_reset`** - force reboot current VM  
**`system_powerdown`** | **`quit`** - dorce shutdown current VM  
**`stop`** - suspend current VM  
**`cont`** - resume current VM  

### Guestfish commands ###  
Start example **`guestfish --ro -a /dev/host/evidence0`**  

Interactive commands:  
**`inspect-os`** - find the OS main parition  
**`mount /dev/sda2 /`** - mount the discovered /dev/sda2 partition  
**`ls win:C:\`** - list system drive C:\ of Windows OS  
**`download win:C:\dir\file ./file`** - get file from guestfs  
**`upload win:C:\dir\file ./file`** - put file to guestfs  

After the session clean up file in a path similar to  
**/var/tmp/.guestfs-0/**  

### Windows memory patterns ###  
Windows 10 64-bit "sethc.exe" pattern:  
**`730065007400680063002E00650078006500200025006C006400000000000000730065007400680063002E006500780065`**  
Replacement pattern with "cmd.exe":  
**`63006D0064002E0065007800650000000000200025006C00640000000000000063006D0064002E00650078006500000000`**  

Windows 10 32-bit "sethc.exe":  
**`730065007400680063002e00650078006500200025006c0064000000730065007400680063002e006500780065`**  
Replacement pattern with "cmd.exe":  
**`63006d0064002e0065007800650000000000200025006c006400000063006d0064002e00650078006500000000`**  

