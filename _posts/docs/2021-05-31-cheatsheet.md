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
### General Linux tips ###  
* Load a national keyboard layout (not the same as switching locale)  
**`loadkeys us`**  
**`loadkeys fr`**  
**`loadkeys de`**  
...

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
#### Dealing with QEMU/QCOW2 ####  
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

* Start with 2GB RAM and faster CPU (6 cores)  
**`qemu-system-x86_64 -enable-kvm -cpu host,hv_relaxed,hv_spinlocks=0x1fff,hv_vapic,hv_time -smp 6,sockets=1,cores=6,threads=1 -m 2048 -boot strict=on -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -vnc :0 -spice port=2001,disable-ticketing -vga cirrus -device usb-ehci,id=usb,bus=pci.0,addr=0x4 -device usb-tablet`**  

* Boot Bitscout within itself on 1GB RAM, 3 cores, and port 2003 forwarded to port 23 from the outside to the guest:
**`qemu-system-x86_64 -enable-kvm -cpu host,hv_relaxed,hv_spinlocks=0x1fff,hv_vapic,hv_time -smp 3,sockets=1,cores=3,threads=1 -m 1024 -boot d -cdrom /dev/sr0 -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -vnc :0 -spice port=2001,disable-ticketing -vga cirrus -device usb-ehci,id=usb,bus=pci.0,addr=0x4 -device usb-tablet`**  

* Start basic VM from a qcow2 file (with SPICE display and SMB file sharing):  
**`qemu-system-x86_64 -enable-kvm -cpu host -m 512 -boot strict=on -drive file=./evidence0.qcow2,format=qcow2,if=ide,id=drive-virtio-disk0 -monitor stdio -spice port=2001,disable-ticketing -vga cirrus -net user,net=10.0.2.3/24,smb=/root/smb,smbserver=10.0.2.4,id=usernet,restrict=y`**  
Note: use a VNC client on your host to connect to Bitscout IP on port 2001  

* Show qemu process sorted memory map:  
**`cat /proc/$(pgrep qemu)/maps | cut -d' ' -f1 | awk -F- '{print (strtonum("0x" $2)-strtonum("0x" $1))" "$0 }' | sort -n`**  


* Connect a disk in qcow2 format to a local block device  
**`qemu-nbd -c /dev/nbd0 ./evidence0.qcow2`**  
Note: Make sure nbd module is loaded and /dev/nbd* devices are present (run `modprobe nbd` if not)  
Now you can work with the disk via /dev/nbd0 local block device.

* Disconnect qcow2 from a local block device  
**`qemu-nbd -d /dev/nbd0`**  

* Export a qcow2 file over the network via NBD protocol  
**`qemu-nbd -p 2001 ./evidence0.qcow2`**  
Note: the NBD service becomes available over TCP port 2001. Add `-f` to fork (put the service in the background).  

* Connect a remote NBD export on port 2001 to a local NBD device  
**`nbd-client %IP% 2001 /dev/nbd0`**  


### Remapping logical disk ###  
* Transparently strip Bitlocker encryption from one of the partitions (/dev/sda2)  
**`HDD_SIZE=$(blockdev --getsize /dev/sda)`**  
**`PARTITION_OFFSET=$(fdisk -l /dev/sda | awk '/^\/dev\/sda2/{print $2}')`**  
**`PARTITION_SIZE=$(fdisk -l /dev/sda | awk '/^\/dev\/sda2/{print $4}')`**  
**`mkdir /mnt/dislocker`**  
**`dislocker -O $[512*$PARTITION_OFFSET] -pPUT-YOUR-BITLOCKER-RECOVERY-KEY-HERE /dev/sda /mnt/dislocker/`**  
**`losetup -r /dev/loop1 /mnt/dislocker/dislocker-file`**  
**`dmsetup create remapped <<EOF`**  
**`0 $PARTITION_OFFSET linear /dev/sda 0`**  
**`$PARTITION_OFFSET $PARTITION_SIZE linear /dev/loop1 0`**  
**`$[$PARTITION_OFFSET+$PARTITION_SIZE] $[$HDD_SIZE-$PARTITION_OFFSET-$PARTITION_SIZE] linear /dev/sda $[$PARTITION_OFFSET+$PARTITION_SIZE]`**  
**`EOF`**  
Note: Use `partprobe /dev/mapper/remapped` to detect partitions on the new disk


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
Windows 10 64-bit "sethc.exe..." pattern:  
**`730065007400680063002E00650078006500200025006C006400000000000000730065007400680063002E006500780065`**  
Replacement pattern with "cmd.exe":  
**`63006D0064002E0065007800650000000000200025006C00640000000000000063006D0064002E00650078006500000000`**  

Windows 10 32-bit "sethc.exe...":  
**`730065007400680063002e00650078006500200025006c0064000000730065007400680063002e006500780065`**  
Replacement pattern with "cmd.exe":  
**`63006d0064002e0065007800650000000000200025006c006400000063006d0064002e00650078006500000000`**  

Windows Server 2008/Windows 7 32-bit "sethc.exe...":  
**`730065007400680063002E006500780065000000730065007400680063002E00650078006500200025006C0064000000`**  
Replacement pattern with "cmd.exe":  
**`63006D0064002E0065007800650000000000000063006D0064002E0065007800650000000000200025006C0064000000`**  

Other variants to try "sethc.exe...":  
**`730065007400680063002E00650078006500200025006C0064000000`**  
Replacement pattern with "cmd.exe":  
**`63006d0064002e0065007800650000000000200025006C0064000000`**  


