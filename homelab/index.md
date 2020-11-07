---
layout: page
title: Homelab
updated: 2020-11-05 09:00:00 +0200
---

## 
Why?
Because I really love playing around with various devices, testing out configurations and learning new stuff along the way. The thought of building my own “playground”/homelab occurred to me some years ago, but I’ve only just now got motivated enough to actually go ahead & build it (Thanks COVID-19!).

Since I live in a relatively small 2-bedroom apartment with a 3-year old (wildly curious) kid & another toddler, space constraints are a given (so are child safety “gadgets”). Hence my discreet living room desk setup.
The weird diagram in an attempt at illustrating how everything is configured at the moment.

## Purpose

+ Have FUN!
+ Learn/Re-learn/Consolidate some networking knowledge (from a Systems Admin’s standpoint)
+ Learn Ansible & Kubernetes
+ Play with & Learn NetBSD’s ATF (Automated Testing Framework)/Kyua(ATF 2.0), which is also available on FreeBSD
+ Revisit & Update knowledge on LDAP (AD & OpenLDAP)
+ Deploy some virtual machines for other software testing/scripting projects
+ Experiment a lot
+ Have MORE FUN!

I’m mainly working as a Software Test Engineer (and have been for 15 years), but I also occasionally take care of test labs/environments. I do have an itch for embedded systems, a bit of programming, obscure operating systems & BSDs. Furthermore, I’m planning to switch my career path towards Systems Administration/Site Reliability Engineering in one to two-years time, therefore this setup is quite useful for learning.

## Hardware
+ 2 x Raspberry Pi 2 v1.1 (These run NetBSD & FreeBSD)
+ 1 x Raspberry Pi 4 4GB (running Raspbian for now)
+ 1 x Atrust Intel-based thin client (an older machine running FreeBSD)
+ 1 x SuperMicro mini-server based on the A1SRi-2358F motherboard (https://www.supermicro.com/en/products/motherboard/A1SRi-2358F), running pfSense
+ 1 x Hyper-V 2019 Core Server (this is my former desktop that got converted to a server), based on an AMD Ryzen 5 CPU with 32 GB DDR4 & almost 1 TB SSD storage
+ 1 x Dell OptiPlex 3050 Micro (7th gen i5, 8 GB DDR4, Windows 10 Pro) acting as a media & file server (it’s linked to the TV and it also runs a Syncthing server to which our mobile phones upload photos - instead of relying on Google Photos, OneDrive, etc.)
+ 1 x TP-Link TL-WR841N/ND v7 (my 10-year old WiFi router, now running OpenWRT)
+ 1 x TP-Link 8-port unmanaged switch
+ 1 x TP-Link x-port unmanaged switch

## Additional hardware
+ 1 x Raspberry Pi Zero W
+ 1 x Texas Instruments Launchpad MSP-EXP430F5529LP (because I’m into some embedded C programming and learning a few things in this area)

*These two are not (yet) actively used in the “lab setup”, but they will be at some point. Until then, I use them for learning purposes, connecting them to my laptop when needed. In the future, I might add an Arduino board.*

## Planned aquisitions
+ 1 x ROCKPro64 4GB SoC (https://www.pine64.org/rockpro64/), mainly for more ARM-related explorations, like running the Xen hypervisor.

The setup itself is not pretentious. In fact, many would say it’s quite awful, but I have space constraints. The whole thing resides in two shelves & a part of my desk, in my living room.