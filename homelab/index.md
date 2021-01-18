---
layout: page
title: Homelab
updated: 2020-23-05 09:00:00 +0200
---
<!--<hr/>
<p>
<h3>Thoughts on building homelabs</h3>
<ul>
{% for post in site.categories.homelab %}
  {% unless post.draft %}
  {% assign currentdate = post.date | date: "%Y" %}
  {% if currentdate != date %}
    {% unless forloop.first %}</ul>{% endunless %}
    {% assign date = currentdate %}
  {% endif %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% if forloop.last %}</ul>{% endif %}
  {% endunless %}
{% endfor %}
</p>
-->
<div align="center">
<a href="{{ site.url }}/images/homelab/ansamblu.jpg"><img src="{{ site.url }}/images/homelab/thumb/ansamblu.jpg" alt="image" /></a>
</div>
<div align="center">
<b><i>A discreet homelab, hidden away from curious toddlers' hands</i></b>
</div>
<br/>

<div align="center">
<a href="{{ site.url }}/images/homelab/homelab-diagram.png"><img src="{{ site.url }}/images/homelab/thumb/homelab-diagram.png" alt="image" /></a>
</div>
<div align="center">
<b><i>Network diagram</i></b>
</div>

**TABLE OF CONTENTS**
* TOC
{:toc}

*There are some photos down below. Don't be afraid to click them in order to view the full sized version*

### Why on Earth would I build a homelab?
<hr/>

Because I really love playing around with various devices, testing out configurations and learning new stuff along the way. The thought of building my own “playground”/homelab occurred to me some years ago, but I’ve only just now got motivated enough to actually go ahead & build it (Thanks COVID-19!).

Since I live in a relatively small 2-bedroom apartment with a 3-year old (wildly curious) kid & another toddler, space constraints are a given (so are child safety “gadgets”). Hence my discreet living room setup.
The weird diagram in an attempt at illustrating how everything is configured at the moment.

### Purpose
<hr/>

+ Have FUN!
+ Learn/Re-learn/Consolidate some networking knowledge (from a Systems Admin’s standpoint)
+ Learn Ansible & Kubernetes
+ Play with & Learn NetBSD’s ATF (Automated Testing Framework)/Kyua(ATF 2.0), which is also available on FreeBSD
+ Revisit & Update knowledge on LDAP (AD & OpenLDAP)
+ Deploy some virtual machines for other software testing/scripting projects
+ Experiment a lot
+ Have MORE FUN!

I’m mainly working as a Software Test Engineer (and have been for 15 years), but I also occasionally take care of test labs/environments. I do have an itch for embedded systems, a bit of programming, obscure operating systems & BSDs. Furthermore, I’m planning to switch my career path towards Systems Administration/Site Reliability Engineering in one to two-years time, therefore this setup is quite useful for learning.

### Hardware checklist
<hr/>
+ 2 x Raspberry Pi 2 v1.1
+ 3 x Raspberry Pi 4 4GB
+ 1 x Raspberry Pi 4 8GB (for running VMWare ESXi Fling for ARM)
+ 1 x [Anker PowerPort 60W Desktop USB power source](https://www.amazon.co.uk/gp/product/B00PK1IIJY/) (with 6 ports, each getting 2.4 Amps)
+ 2 x [GeekPi Acrylic cluster cases for Raspberry Pi](https://www.amazon.co.uk/gp/product/B07J9VMNBL/) (needed two sets for building a larger stack)
+ 1 x Western Digital 250 GB SSD USB3.1 (used as a datastore for VMWare ESXi, on the Pi)
+ 1 x Atrust Intel-based thin client (an older, refurbished and fanless machine)
+ 1 x SuperMicro A1SAi mini-server based on the A1SRi-2358F motherboard, running VMWare ESXi (hosting an instance of pfSense that takes care of routing and LAN segments)
+ 1 x Proxmox VE Server (this is my former desktop that got converted to a server), based on an AMD Ryzen 5 CPU with 32 GB DDR4 & almost 1 TB SSD storage
+ 1 x Dell OptiPlex 3050 Micro (7th gen i5, 8 GB DDR4, Windows 10 Pro) acting as a media & file server (it’s linked to the TV and it also runs a Syncthing server to which our mobile phones upload photos - instead of relying on Google Photos, OneDrive, etc.)
+ 1 x TP-Link TL-WR841N/ND v7 (my 10-year old WiFi router, now running OpenWRT and taking care of the wireless network associated with the lab)
+ 1 x [8-port Netgear GS308E Gigabit managed switch](https://www.amazon.co.uk/gp/product/B07QHD134G/)
+ 2 x [UK-to-EU power plug adapters](https://www.amazon.co.uk/gp/product/B079NT1RMG/) 
+ 1 x Zyxel 5-port Gigabit managed switch
+ Cables

#### Additional hardware
+ 1 x Raspberry Pi Zero W
+ 1 x Texas Instruments Launchpad MSP-EXP430F5529LP (because I’m into some embedded C programming and learning a few things in this area)

*These two are not (yet) actively used in the “lab setup”, but they will be at some point. Until then, I use them for learning purposes, connecting them to my laptop when needed. In the future, I might add an Arduino board.*

### Building the lab
<hr/>

I first took the Supermicro server, cleaned it up and placed it in the bottom drawer of a simple IKEA living room organizer. I actually dismantled the back of the drawer (made of pretty solid plastic) in order to have access to all ports and help with ventilation.

<div align="center">
<table>
<tr align="center">
<td>
<a href="{{ site.url }}/images/homelab/supermicro1.jpg"><img src="{{ site.url }}/images/homelab/thumb/supermicro1.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/supermicro2.jpg"><img src="{{ site.url }}/images/homelab/thumb/supermicro2.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/supermicro3.jpg"><img src="{{ site.url }}/images/homelab/thumb/supermicro3.jpg" alt="image" /></a>
</td>
</tr>
</table>
</div>
I placed the power sockets on top of it in a manner that doesn't cover the server's fans. I use two separate multiple socket thingies, each with an ON/OFF button. One of them is for the Raspberry Pi cluster, because I want to be able to shut that thing off when I'm not actively working with it.

<div align="center">
<table>
<tr align="center">
<td>
<a href="{{ site.url }}/images/homelab/supermicro4.jpg"><img src="{{ site.url }}/images/homelab/thumb/supermicro4.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/supermicro5.jpg"><img src="{{ site.url }}/images/homelab/thumb/supermicro5.jpg" alt="image" /></a>
</td>
</tr>
</table>
</div>

#### Assembling the Raspberry Pi cluster

I did this in two consecutive evenings, with children-induced chaos & stress. Just kidding, I just used a few small chunks of spare time to put it together.
The GeekPi cluster case is built to house 4 boards. Since I wanted to have 7, I had to purchase two sets. No biggie, they're quite cheap. Nothing much to say here, just playing around with minuscule screws and pins. The GeekPi comes with a lot of heatsinks and one fan for each of the devices you want to add to it.

<div align="center">
<table align="center">
<tr align="center">
<td>
<a href="{{ site.url }}/images/homelab/cluster1.jpg"><img src="{{ site.url }}/images/homelab/thumb/cluster1.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/cluster2.jpg"><img src="{{ site.url }}/images/homelab/thumb/cluster2.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/cluster3.jpg"><img src="{{ site.url }}/images/homelab/thumb/cluster3.jpg" alt="image" /></a>
</td>
</tr>
<tr align="center">
<td>
<a href="{{ site.url }}/images/homelab/cluster4.jpg"><img src="{{ site.url }}/images/homelab/thumb/cluster4.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/cluster5.jpg"><img src="{{ site.url }}/images/homelab/thumb/cluster5.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/clusterpads.jpg"><img src="{{ site.url }}/images/homelab/thumb/clusterpads.jpg" alt="image" /></a>
</td>
</tr>
</table>
</div>

#### Putting it all together

Now, on to the top drawer, which will host the Atrust thin client, Netgear switch, Raspberry Pi cluster along with the Anker power supply and the good ol' TP-Link WiFi router. In order to keep things a bit spaced, I've used a "Variera" kitchen cupboard organizer. Naturally, all equipment has "rubber feet". 
First, place the USB power source, the thin client and the router, along with their cables. Then, fit in the organizer and insert the Netgear switch and the RPi cluster on top of it (again, using some glued rubber pads just to keep things safe).

<div align="center">
<table>
<tr align="center">
<td>
<a href="{{ site.url }}/images/homelab/drawer.jpg"><img src="{{ site.url }}/images/homelab/thumb/drawer.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/organizer.jpg"><img src="{{ site.url }}/images/homelab/thumb/organizer.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/arrangement1.jpg"><img src="{{ site.url }}/images/homelab/thumb/arrangement1.jpg" alt="image" /></a>
</td>
</tr>
<tr>
<td>
<a href="{{ site.url }}/images/homelab/clusterready.jpg"><img src="{{ site.url }}/images/homelab/thumb/clusterready.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/arrangement2.jpg"><img src="{{ site.url }}/images/homelab/thumb/arrangement2.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/arrangement3.jpg"><img src="{{ site.url }}/images/homelab/thumb/arrangement3.jpg" alt="image" /></a>
</td>
</tr>
</table>
</div>

Time to get down on my knees and make the cable mess less messy.

<div align="center">
<table>
<tr align="center">
<td>
<a href="{{ site.url }}/images/homelab/cablemess.jpg"><img src="{{ site.url }}/images/homelab/thumb/cablemess.jpg" alt="image" /></a>
</td>
</tr>
</table></div>

Insert all cables and give it a go. Boy, that does sound good!

<div align="center">
<table>
<tr align="center">
<td>
<a href="{{ site.url }}/images/homelab/IMG_20201122_061516.jpg"><img src="{{ site.url }}/images/homelab/thumb/IMG_20201122_061516.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/IMG_20201122_061536.jpg"><img src="{{ site.url }}/images/homelab/thumb/IMG_20201122_061536.jpg" alt="image" /></a>
</td>
<td>
<a href="{{ site.url }}/images/homelab/IMG_20201010_145707.jpg"><img src="{{ site.url }}/images/homelab/thumb/IMG_20201010_145707.jpg" alt="image" /></a>
</td>
</tr>
</table></div>

*The ex-desktop (now server) running Proxmox VE can be seen in the third photo*


### What do I use it for?

Well, the Supermicro server has VMWare ESXi installed on it. pfSense runs in a VM and is binded to three physical NICs on the server (named WAN, LAB & CLUSTER). This VM handles Internet traffic coming through from the crappy router provided by my ISP. I also run a few other lightweight VMs on this server, like Pi-hole & Alpine Linux.

The Raspberry Pis are used for learning Kubernetes, Docker, Ansible, k3s/Rancher and toying around with NetBSD's Kyua/ATF (an automated testing framework for Net & FreeBSD - this is done on the RPi 2s). One of the RPis VMWare ESXi for ARM on it, for testing & more (lighter) virtualization. The Atrust thin client is linked to the cluster and it's mainly used as a machine for coordinating the boards (Ansible & the like).

Dell OptiPlex 3050 Micro is a great mini-PC that's used as a media center (on Windows 10 Pro) for streaming services. It also runs Syncthing, with which our smartphones sync daily for backing up photos.

Finally, the Proxmox VE server is used for more hardcore virtualization, mainly for studying/learning Windows & UNIX servers at a more "business-like" level (Directory Services in mixed environments, unattended Windows deployments, Hyper-V administration, etc.). 

So, it's an environment that gives me quite some flexibility in learning the topics I'm interested in, while still being fairly discreet and far from the reach of curios children (for now).

That's mainly all I have to say about how I started my journey in this whole "homelab" universe.

