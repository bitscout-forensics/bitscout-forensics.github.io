---
layout: post
title: "How Bitscout is different from other tools"
date: 2020-02-14
category: intro
author: nicolas
short-description: Why you should consider switching to Bitscout from your commercial tools
---

-----

### WHY SHOULD YOU EVEN THINK OF SWITCHING TO BITSCOUT? ###  
Good question. If you are experienced digital forensics examiner then you probably are familiar with a number of commercial and free tools. Probably you already own licenses for expensive forensic tools out there. Here is a short answer why you should consider:
1. Bitscout is FREE => Save your money  
1. Bitscout is remote => Save your time for travelling, process more cases  
1. Advanced Bitscout usage requires solid technical knowledge => Grow your expertise even further  
1. Bitscout comes with tools that you might have missed => Try something different and find even better clues  
1. Bitscout records shell sessions => You can train your juniors, or prove findings with your recording  
1. Want to add a feature or fix a bug => You don't need to wait for the vendor to respond  

After all, you may simply do some common good for all of us: support Bitscout community. This way, Bitscout will get some traction, and one day analysis with Bitscout will be admitted in court equal to other comemrcial expensive tools. Think of how many people in developping coutries have to buy expensive tools, pay for license renewal, trainings, etc just to be able to use it.


### SOUNDS GOOD? HERE IS MORE ###  
Bitscout is similar to many other forensic tools but fundamentally different in a few ways described below:

#### Remote by design ####  
Bitscout was built because we had no other way than remote access. It was an experiment, a test aimed to check if we can do everything in commandline that GUI tools can do. And it worked. Worked so well, that we decided to keep using and developing this method. 

Where can it help you or others? Just imagine doing forensics for a victims located in a country that is in the middle of war. Or working on a computer that is located in environment potentially contaminated by dangerous bilogical virus, or analysing a system on post-nuclear fallout land. Well, those are rare scenarios, but maybe your employer simply has dozens of offices in remote locations? Perhaps you have a customer running oil&gas mining platforms, a logistics business, a remote farm?

#### Scale up and analyze things LIVE without waiting ####  
Traditional forensic methodology typically requires a step to "Duplicate and verify integrity of 'Forensic Data'" [1], commonly referred to as "acquisition". This usually involves copying to another media the content containing potential evidence or clues to investigate the cases. This process may take a significant amount of time depending on data volumes. Add potential need to decrypt copied large drive to yet another media and you will have significant time overhead.

When a forensic expert cannot travel to the subject system, the drive typically has to be sent to the expert. It also means that there must be sufficient expertise locally to "Duplicate and verify integrity of 'Forensic Data'", without any error that may damage the data or tamper with the original media. Lastly, depending on the geographic differences between the compromised system and the expert, it may take several hours or days before the expert finally can get access to the systems and start working on it. Some suspected systems might require the original hardware too (special RAID configurations, cryptographic chips, rare bus cables, etc).

When you use Bitscout, you boot on the subject system using original hardware. The system starts from Live OS on a bootable media (CD/DVD, USB thumb drive, or even ISO image attached over network to virtual CD-ROM). Once the system starts, it autoconfigures network (if DHCP is available) and instantly provides basic shell to the expert. If there are multiple subject systems the owner can simultaneously start virtually unlimited number of suspected systems. Once each system is booted of Bitscout, simultaneous analysis of all of them can then take place.


#### STAY HUNGRY, STAY FOOLISH ####  
Bitscout was designed with frugality in mind too, with reduced size of the live OS, minimal use of RAM, optimisrf access to resources such as only acquiring just the necessary evidence (as opposed to the whole disks over the network), or leveraging the original hardware locally. It allows the expert to run virtual machines off the LiveOS and start the suspected OS and perform “live interaction” with potentially infected system, dump or modify the VM's memory (i.e. disable logon password check). Interaction with the infected system opens a whole new world of opportunities to narrow down the search and increase your efficiency, take screenshots (as if they come from the real system), and more. And if you network connection is unstable or slow, Bitscout's text based interaction is perfect for such conditions, requiring minimal bandwidth.

#### Foolproof design ####   
Bitscout was built with security in mind so the forensics experts could perform their analysis based on the rights the owner grant to the experts. The expert inherits a virtual environment with full control over the session but can’t override the owner’s permissions to access devices and resources that were now explicitly allowed.

This is achieved through an unprivileged container-based isolation. Basically, the expert operates in an unprivileged container. Default permissions are restrictive by default to prevent the owner, potentially lacking technical expertise, from making mistakes and accidentally modifying precious evidence disks. The expert operates as pseudo-root in the container. While the expert cannot load kernel modules, reconfigure network or mount filesystems, the expert may however mount the available disks using userspace drivers, run custom tools or even install new tools not provided by default. Because the system is booted from Bitscout and the disks mounted as read-only, the owner plays a role in the chain-of-custody. 


#### Agentless ####   
Bitscout is agentless and, unlike all existing EDR and remote forensic software solutions, will not leave any footprint on the suspected system. This is important not only for forensically sound procedure, but also for silent analysis that doesn't even potentiall alarm the attackers of security response initiative. 

#### Free, open-source and fully customisable ####   
Bitscout is open-source and FREE to use. Hundreds of developers, security reseachers and forensics specialist have developped an overwhelming number of various tools. Many of them reliably worked for years and decades. This treasure trove of knowledge and expertise is jsut out there, lying around and available to anyone at any moment. Instead, people pay thousands and thousands dollars for their forensics software, hardware, cables, flight tickets, visas, etc to something that can be done for free and much faster.

In fact, you don't even need Bitscout to do remote forensics, if you have remote Linux shell on the system with subject drive attached. Bitscout simply makes it easier for you to build an ISO file and send where required, using your VPN certificates, SSH keys, passwords, etc. It takes about 5 minutes to assemble a new LiveOS on a modern computer. You try it, and if you found something missing, you may modify, patch, extend without rebuilding everything from scratch. So that new image can be prepared in a matter of seconds/minutes. This makes your life as the LiveOS author so much easier.

We hope you find the tool useful. Happy hunting!

* [Duplicate and verify integrity of 'Forensic Data'](https://www.justice.gov/sites/default/files/criminal-ccips/legacy/2015/03/26/forensics_chart.pdf)
* [Full Disk Encryption](https://www.esecurityplanet.com/network-security/7-full-disk-encryption-solutions-to-check-out.html) 
* [PXE](https://en.wikipedia.org/wiki/Preboot_Execution_Environment)

 

