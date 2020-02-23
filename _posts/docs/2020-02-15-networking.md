---
layout: post
title: "Bitscout Networking"
date: 2020-02-15
category: docs
author: vitaly
short-description: Network architecture used in Bitscout 
---

-----
<link rel="stylesheet" type="text/css" href="/assets/asciinema-player.css" />
<script src="/assets/asciinema-player.js"></script>

# Network Communication #
A running Bitscout instance uses multiple network interfaces and if you are an expert using it, you shall understand how the network communication is designed.

By default Bitscout exposes no ports to the local network. It will attempt to connect to the VPN server specified in the OpenVPN configuration (see `config/openvpn/scout.conf.client` in the build directory). Once the VPN connection is established, TCP port 22 becomes available over the VPN link. 

## Connecting from LAN ##  
If you are using Bitscout inside your LAN or trying on a VM, you (in the role of system owner) may enable connections from the LAN using Bitscout management tool menu (Network -> Enable Access from LAN) like shown below:  
<asciinema-player cols="112" preload src="/assets/casts/bitscout20.04_net_enable_lan.cast"></asciinema-player>

## Connecting to the LiveOS Host ##  
If you are the owner or have absolute trust of the remote user, you may want to connect outside of the container via SSH. In this case you should enable connections to the Host via Bitscout management tool (Network -> Enable Host Control).
<asciinema-player cols="112" preload src="/assets/casts/bitscout20.04_net_enable_hostcontrol.cast"></asciinema-player>

## Networks in Bitscout ##
Unmodified Bitscout uses the following subnets by default:
* 10.0.3.0/24 for host to container network on LiveOS (ve-container interface)
* 10.1.0.0/24 for the VPN link (tap0 interface)
* Your local subnet (wlan0 for WiFi, eth0 for cable LAN or VM network interface)

For the expert's convenience, Bitscout by default forwards a number of TCP ports via VPN link to the container. To better understand this scheme look at the diagram below:  

![](/assets/network_interfaces_20.04.png){: .img-responsive }

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
Inside container you should see just one interface (excluding loopback **lo**): **eth0** with IP **10.0.3.2**. This interface is used to communicate with the host system. In fact the host system uses it to forward SSH connections (TCP port 22) from VPN link to the container, as well as few other reserved ports. 

## Port Forwarding ##
Default port forwarding is setup via iptables and is located in the following shell script file: **/sbin/host-iptables**. If you want to change it before it is integrated into the root filesystem, change it in your build directory at **./resources/sbin/host-iptables**.  
Currently the following ports are forwarded from VPN IP address (10.1.0.2) to the container (10.0.3.2):  
tcp port 22 (VPN) => tcp port 22 (container)  
tcp port 2000 (VPN) => tcp port 2000 (container)  
tcp port 2001 (VPN) => tcp port 2001 (container)  
...  
tcp port 2009 (VPN) => tcp port 2009 (container)  
  
The port 22 is used for SSH service, while ports 2000-2009 are reserved for other services, which the expert may use, such as network block device service or anything else.

## Customizing the Firewall ##
Bitscout is mainly relying on iptables, which is setup during system startup via `/sbin/host-iptables` script (`./resources/sbin/host-iptables` in the Bitscout build directory.) Feel free to modify the file to your needs.
