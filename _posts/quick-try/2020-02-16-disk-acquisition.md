---
layout: post
title: "Trying Basic Procedure"
date: 2020-02-17
category: quick-try
author: vitaly
short-description: Try Disk Acquisition
---

-----
# Try Basic Procedure #  
## Disk Acquisition ##  
Below is the description of a remote disk image acquisition process using Bitscout, where the system owner is non-experienced commandline user (relies on Bitscout management tool only).
### The owner ###  
1. Maps the evidence drive from host to the experts container using Bitscout management tool (see Disk Operations above).
Let's assume that it was mapped as evidence0.
1. Attaches output storage device (can be removable USB hdd) to the host system.
1. Maps the attached output storage partition to writable device on the container. Lets assume it is mapped as storage0.
### The expert ###  
1. Mounts the attached output drive filesystem on local directory (i.e. /mnt/storage0).
1. Acquires disk image using dd or it's clone. For example:
`# dc3dd if=/dev/host/evidence0 of=/mnt/storage0/image.dd bs=4k hash=md5 log=/mnt/storage0/image.dd.log progress=on`
1. Unmounts the output filesystem.
### The owner ###  
1. Unmaps evidence0 and storage0.
1. Disconnects the output storage device.
