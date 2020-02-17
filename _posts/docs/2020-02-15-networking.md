---
layout: post
title: "Bitscout Networking"
date: 2020-02-15
category: docs
author: vitaly
short-description: Network architecture used in Bitscout 
---

-----

# Network Communication #
A running Bitscout instance uses multiple network interfaces and if you are an expert using it, you shall understand how the network communication is designed.

## Network Interfaces ##
![](https://i.ibb.co/R9mHQCW/network-interfaces-20-04.png){: .img-responsive }

### Host Interfaces ###
Physical interfaces on the host system may include but are not limited with Ethernet and Wifi network cards, which are named by default as following:  
* **eth0**  
* **eth1**  
...
* **wlan0**  
...  
  
If VPN connection is established you may see a virtual network interface **tap0** on the host. This interface by default should have IP **10.1.0.2**, which is assigned by the VPN server.  
  
In addition there is a virtual interface that is used to communicate with the expert's container:
* **ve-container** (virtual Ethernet created by container management software)
  
### Container Interfaces ###
Container has just one interface (excluding loopback **lo**): **eth0** with IP **10.0.3.2**. This interface is used to communicate with the host system. In fact the host system uses it to forward SSH connections (TCP port 22) from VPN link to the container. 

## Port Forwarding ##
Default port forwarding is setup via iptables and is located in the following shell script file: **/sbin/host-iptables**. If you want to change it before it is integrated into the root filesystem, change it in your build directory at **./resoruces/sbin/host-iptables**.  
Currently the following ports are forwarded from VPN IP address (10.1.0.2) to the container (10.0.3.2):  
tcp port 22 (VPN) => tcp port 22 (container)  
tcp port 2000 (VPN) => tcp port 2000 (container)  
tcp port 2001 (VPN) => tcp port 2001 (container)  
...  
tcp port 2009 (VPN) => tcp port 2009 (container)  
  
The port 22 is used for SSH service, while ports 2000-2009 are reserved for other services, which the expert may use, such as network block device service or anything else.

