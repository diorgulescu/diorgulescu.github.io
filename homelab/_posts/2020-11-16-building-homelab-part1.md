---
layout: post
title:  "Building A Homelab, Part 1 - Checklists"
date:   2020-09-22 09:00:00 +0200
updated: 2020-09-22 09:00:00 +0200
category: homelab
---

### Context

So, you've reached the conclusion that a homelab is best to increase your IT knowledge. True that! If one wants to learn more about networking, systems administration, distributed computing or if you just plan on having some good ol' geeky fun, I don't think there's a better option out there.

Maybe you have already snooped around r/homelab and glanced in awe at some of the monster configurations those guys post there. Truly spectacular, indeed. Made out of scrap or retired hardware, those monster racks could heat up an entire household in some cases. If you are a network or system engineer that knows exactly what to do with that and you're truly confident you need it, good for you. Just mind the long term costs, because a single rack server can be quite a loud and power-hungry beast, so your bills might skyrocket.

However, you don't need all that in order to build or start a homelab. Thankfully, nowadays we have virtualization and that saves a lot of headaches (while inducing others, of course, but we're in a better spot now, nonetheless). If you live in an apartment and you just want some hardware that would allow you to host your own media server, your own cloud sharing solution (like NextCloud or OwnCloud) or a Network Attached Storage (NAS) for everyone in your household, you don't need racks (unless you insist on going that route, obviously). Throw in a bunch of routers and/or managed switches and you've got yourself a networking lab that's most probably capable of running a variety of systems and services.

Also, if you like playing in the ARM-realm, why not go ahead and get a few Raspberry Pi boards? You can easily find second-hand older models that run just fine. Stack them in a cluster and learn Cluster Computing, Kubernetes, Docker or data processing & statistics with Kibana, Grafana, Prometheus, and so on. 

As you might know, the possibilities are truly endless. But first, let's make a plan.

### Your aim

You must have at least some idea of what you're going to try out or want to learn. At least in broad terms, be it networking, containers, programming, server administration or anything else. Orienting yourself (even vaguely) will help you in planning what hardware you need to start with. Don't worry, you may change anything along the way, at any time. 

Maybe you're into software development and you need some hosts to build code, or you want to get into DevOps or Network Administration. This will give you some direction when it comes to choosing hardware later on.

### Budget

This is really important. The best piece of advice I can give is to try and look for second-hand/used/scrap hardware & computer parts that are functional. You don't need all your equipment to be new, because hardware can get pretty pricey. If you or someone in your family has an old desktop computer or a laptop with a broken screen, tell them not to throw it away and give it to you (even "headless" laptops can become useful Linux servers). Most probably you'll do them a favor and you'll win new lab hardware.

Make sure you evaluate your expenses well. If you also have a family and/or children, make sure your plan does not hinder the overall family's wellbeing. Food needs to be on the table, monthly expenses need to be covered and leave comfortable room for all the needs your family members have (school taxes, books, subscriptions, clothing, etc.). If the budget is tight, try to plan ahead and buy one thing a month, something that will not severely impact your finances.

If you're in a really tight spot (like a student or a young fella that wants to switch jobs), consider using what you have at hand, be that your laptop or desktop. Yes, your desktop can easily become a virtualization server. You just need to install a hypervisor onto it (these are free and you have quite a lot of choices: VMWare ESXi, Microsoft Hyper-V Core, Proxmox VE, Xen, KVM/QEMU, etc.). That will instantly unlock two paths: learning virtualization & being able to run multiple operating systems simultaneously on a single host. 

### Convince your family that you do need a homelab

Well, this is optional, of course. If you live alone, no worries there! Otherwise, since this is a decision that involves adding new things around the house, some purchases & a slightly increased electrical bill, it's at least honest to express what you want to do in detail (well, in layman terms if your spouse is not a technical person, obviously). 

You need to make clear how this will help you on the long term:
+ By learning more (take into account the option of enrolling in a couple of online courses) using hands-on equipment, you will be able o switch jobs, thus helping you evolve as an individual both personally & professionally. Of course, increased income is a plus for everyone
+ It may (or should?) also be a hobby you truly enjoy spending your spare time on, which is absolutely great. Having a mind-stimulating hobby helps your general wellbeing and a happy, more relaxed & fullfiled family member is always desirable
+ Assure everyone you are going to take all required measures to guarantee household safety. No bizzare improvizations that could start a fire, no exposed high-voltage equipment that could harm you children, no noisy equipment placed in areas that need to be kept peaceful & quiet (think bedrooms, living rooms, dining rooms, etc.)

Once everything is explained thoroughly, you'll get full support from the ones closest to your heart. And that's really important.

### What to start with? 

This is the hardest part. It may take quite a while until you make your final decisions, but keep in mind that you should have some sort of a router & firewall solution. There are a lot of networking devices out there that combine these functionalities. You may go for a dedicated device like the ones made by Netgear of Ubiquity, or you may choose to setup a low-powered mini-server that has at least two NICs (Network Interface Cards) on it and install something like pfSense. It's really up to you and what you want to learn. If you're more inclined towards networking & systems administration, pfSense may be a good choice. If you just want something that sticks to those functionalities, go for dedicated equipment instead. 

