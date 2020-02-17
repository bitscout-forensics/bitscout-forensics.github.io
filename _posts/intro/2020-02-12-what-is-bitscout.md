---
layout: post
title: "Welcome to Bitscout"
date: 2020-02-12
category: intro
author: vitaly
short-description: A quick overview of Bitscout to get you started
---

-----
# Intro #  
Bitscout is a customizable Live OS constructor tool almost entirely written in Bash. It's main purpose is to help you quickly create own remote forensics bootable disk image. Bitscout is free and open-source.  

![](../assets/bitscout_boot_menu.jpg){: .img-responsive .col-6 .col-mx-auto}

The graphical bootsplash above is a welcome and goodbye to graphical interface in Bitscout. Bitscout is non-GUI oriented project, because we believe we need to actually *talk* to our computers, not *touch* them with a finger extended via mouse or a touch surface. No, seriously, the speed of text-based interaction in these tasks can surpass GUI experience. Not only that, but text-based interaction is compact, easy to store, read, interpret, as well as trasfer over the network.

# Modus Operandi #  
To understand overall procedure, look at the diagram below. 
![](../assets/remote_operation.png){: .img-responsive .col-6 .col-mx-auto}

Note, that remote expert gets a terminal shell access to the target container (an isolated environment). Actual system owner needs to map selected drive for analysis and optionally attach an external disk for output. This way the expert can do heavy-lifting on behalf of the system owner, such as do forensically sound disk image acquisition, and while it is being copied, start analyzing it and extract some interesting artefacts and clues to the same drive. All expert's actions in the remote session are visible to the system owner and logged into dedicated files. If the system owner finds that the expert is not looking where expected or does something unrelated, the session can be terminated or suspended until cleared.

Coming from infosec defenders, we from the very beginning wanted this remote mode of operation to be as transparent as possible, so that the owners stays in control of the whole process. We believe this is crucial for the success of remote collaboration, which most of people are not used to yet.

# Bitscout promise #  
Bitscout will remain transparent and open-source project with architecture focused on protecting the interests of subject system owner during remote cyber investigations. First of all, we follow the Hypocratic Oath ("First do no harm") along the development of all features. This shows our care for the subject system owner by preventing accidental harm. Second, we follow best practice of digital forensics by creating zero footprint environment that cannot change the evidence data. Last but not the least we record all actions and conversations during remote examination to be used as proof in the chain of custody.


# Is it your silver bullet? #  
This project was created by security researchers for cyber investigators and threat hunters. Although, we love to automate things and save our time through scripting, if you are looking for one click shiny solution that does routinous task over and over again, Bitscout may not suit your needs. Bitscout is a toolkit for non-conventional in-depth investigation, based on deep field experience accumulated over years of investigations.

Given there is no fancy GUI, no bells, no whistles, if you are not familiar with Linux commandline, it's good time to learn it. And believe us, once you down on that path you will understand how much had you missed. 

![](../assets/nbnw.jpg){: .img-responsive .col-xs .col-mx-auto}

# If you want to do it right - do it yourself! #  
Once you make your own Bitscout image, it's fully yours. You are in control: it will use your certificates, your keys, your configs, your tools, your signatures. Bitscout is a tool to help you make your own sharp blade. Make it light, make it heavy-stuffed with all possible tools. Make it manual, make it automated and scripted. Use it in default isolation mode fair to the remote system owner, or give yourself full permissions on the host if you are the system owner. The choice is yours and is just about modifying few text lines to get what you need. You are to make it right for you, we only show you the direction.


# Found it useful? Share your experience! #  
If you manage to find some application of Bitscout that you founf useful, drop us an email and we may be posting your cool tricks and scenarios on this website to share with others. 

As of right now, we found Bitscout very useful for the following non-forensics tasks: 
* Extracting data from a laptop with broken screen
* Helping friends and parents to recover broken system
* Disabling malware that starts on boot and prevents AV from being installed
* Resetting forgotten system passwords remotely
* Running a red teaming exercise, simulating cold boot attacks
* Monitoring subject system traffic without extra hardware


