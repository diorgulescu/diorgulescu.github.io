---
layout: post
title:  "Deploying Hyper-V Server Core 2019 (without a domain controller)"
date:   2020-11-01 09:00:00 +0200
category: tutorials
---

# Deploying Microsoft Hyper-V 2019 without using a Domain

## Prerequisites 

+ For fully managing the Hyper-V server remotely, you need to install Remote Server Admnistration Tools ([https://www.microsoft.com/en-us/download/details.aspx?id=45520])
+ Download the Hyper-V 2019 ISO from Microsoft: [https://www.microsoft.com/en-us/evalcenter/evaluate-hyper-v-server-2019]
+ Rufus USB flashing tool: [https://rufus.ie/]
+ A decent PC LOL

## Installation 

Well, not much to say here. Pretty straightforward, just like a normal Windows installation.

Once the ISO is downloaded, stick an USB stick into your PC and launch Rufus. Select the ISO file you've just downloaded, make sure the USB stick is selected and check that GPT is used.

{{ :rufus.png?direct&400 |}}

Reboot your server-to-be and select the USB drive as a boot option. Then, carry on as usual.

Easy-peasy lemon-squeezy!
## Enable Remote Hyper-V Management 

*This is strictly in regards to Hyper-V and it's settings. For "full" remote server management, please see the section about using Remote Administration Tools/Server Manager.

On The Server:
<code>
PS C:\Windows\system32> Enable-PSRemoting
PS C:\Windows\system32> Enable-WSManCredSSP -Role server
</code>

On the client (my laptop in this case):
<code>
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "WIN-2ABIHGL7VAD"
Enable-WSManCredSSP -Role "Client" -DelegateComputer "WIN-2ABIHGL7VAD"
</code>

Now, for me this did not seem to work at all, so I reissued the commands above, but with the IP address replacing the FQDN of the Hyper-V server:
<code>
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "192.168.1.6"
Enable-WSManCredSSP -Role "Client" -DelegateComputer "192.168.1.6"
</code>

After that, it was required for me edit the Group Policies. 

===== Edit Group Policies =====

Again, following the official instructions from Microsoft proved to be insufficient, so I once again need to praise Taylord Tech, because he did encounter all these issues and pointed to a valuable tip.

Open ''gpedit.msc'' and go to **"Computer Configuration > Administrative Templates > System > Credentials Delegation"**. Double click **"Allow delegating fresh credentials with NTLM-only server authentication"** and select **"Enable"**. Then, Click **"Show"**, next to **"Add servers to the list"** and add "''WSMAN\*''". The official docs say one should add the FQDN of the server ("''WSMAN\WIN-2ABIHGL7VAD''" in my case), but that didn't work at all for me. 

{{ :gpedit-1.png?direct&600 |}}

{{ :gpedit-2.png?direct&600 |}}

{{ :gpedit-3.png?direct&600 |}}

===== Enable Remote Disk Management =====

FIXME
I did not succeed in setting up remote disk management, even though I did follow some how-to's/tutorials/links in the MS Docs. I issued the following PowerShell commands on both the server & the client, but with no luck:
<code>
Set-NetFirewallRule –Name “RVM-VDS-In-TCP” –Enabled True -Profile Any
Set-NetFirewallRule –Name “RVM-VDSLDR-In-TCP” –Enabled True -Profile Any
Set-NetFirewallRule –Name “RVM-RPCSS-In-TCP” –Enabled True -Profile Any
</code>

After installing **Remote Server Administration Tools** on my Windows 10 laptop, I couldn't get the Server Manager to properly connect to the Hyper-V host. I have some things to learn, that's true. The errors were in regards to HTTPS access, since my laptop & server are not part of a domain (I guess that has something to do with it). 

But, for my needs, a simple Remote Desktop Connection was enough.

===== Adding a new disk =====

I ran the ''diskpart.exe'' tool from a command prompt and formatted the second SSD drive on my server (~500GB) and assigned it a drive letter:
<code>
c:\diskpart

DISKPART> list disk

  Disk ###  Status         Size     Free     Dyn  Gpt
  --------  -------------  -------  -------  ---  ---
  Disk 0    Online          120 GB     0 B
  Disk 1    Online          500 GB   200 GB

DISKPART> select disk 1

Disk 1 is now the selected disk.

DISKPART> create partition primary

DISKPART> list partition

DISKPART> select partition 1

DISKPART> format fs=NTFS quick

DISKPART> assign letter=D
</code>

===== Copying files to the Hyper-V host =====

Now, I just needed a way to actually copy some ISO's over to the server so that I could install various operating systems. Being in the context of a homelab, I resorted to file sharing (I even mapped the drive on which I keep my "ISO store"). For that, I issued the following from a Powershell instance on the Server:
<code>
netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes
</code>

Then, I mapped the **C:** drive on my server to **Z:** on my laptop. This way, I was able to copy all ISO files I would ever need (and not only that).

Right after that, I began installing my first VMs on my first homelab Hyper-V Server.

Yay me!

===== References & Resources =====

  * [[https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/manage/remotely-manage-hyper-v-hosts]]
  * [[https://www.youtube.com/watch?v=57Ijn7re8X8]]
  * [[https://social.technet.microsoft.com/Forums/office/en-US/cbdbcf92-d697-41d1-aa7a-bacf34bd48a5/remote-disk-management-rpc-server-unavailable]]
  * [[https://serverfault.com/questions/449192/server-2012-core-no-gui-how-to-manage-disks]]
  * [[http://technet.microsoft.com/en-us/library/cc770877.aspx]]
  * [[https://www.nakivo.com/blog/copy-iso-file-hyper-v-host/]]
Want to start a blog? Visit [https://github.com/sebbas/plain-html-blog][source-code] and learn how to set up your own *plain-html-blog*! Enjoy!

[source-code]: https://github.com/sebbas/plain-html-blog
