
All accounts currently come with these features:

SSH (command-line access) - [Connecting with Putty on Windows](https://www.feralhosting.com/faq/view?question=12) - [SSH guide basics - OS X](https://www.feralhosting.com/faq/view?question=217)
SFTP (secure file transfer) - [SFTP using Filezilla](https://www.feralhosting.com/faq/view?question=187)
FTP (insecure file transfer) - [FTP using Filezilla](https://www.feralhosting.com/faq/view?question=187)
HTTP / PHP / APACHE / NGINX / A Valid SSL Domain - [Putting Your WWW Folder to Use](https://www.feralhosting.com/faq/view?question=20)

Available to install via the `Install Software` link in your [Account Manager](https://www.feralhosting.com/manager/) - [more info](https://www.feralhosting.com/faq/view?question=6)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/install_software_link.png)

rutorrent/rTorrent - [Selecting an rtorrent version](https://www.feralhosting.com/faq/view?question=202)
wTorrent/rTorrent - [wTorrent - Usage and Troubleshooting](https://www.feralhosting.com/faq/view?question=3)
Deluge / Deluge Web Ui + Deluge Thin Client - [Deluge Daemon - Remote control with the local Thin client](https://www.feralhosting.com/faq/view?question=76)
Transmission / Transmission Web Ui + Transmission remote GUI - [Transmission and Transmission Remote GUI](https://www.feralhosting.com/faq/view?question=4)
MYSQL - [Using Mysql](https://www.feralhosting.com/faq/view?question=9)
OpenVPN - [Using Openvpn](https://www.feralhosting.com/faq/view?question=5)

**Q:** What is account credit and how does it work?
---

A: Account credit is applied on a case by case basis by Staff. It is not something that is done automatically and we ask for a little patience during the process. When credit has bee applied to your account you will see it in your Account Manager and you may then use it against the cost of your services at renewal time or when purchasing additional services.

**Q:** I want more disk space, how do I get it?
---

A: There is no way to provide a slot with increased storage capacity once it has been set up. In order to increase storage capacity or to take advantage of offers related to storage capacity you will be required to purchase an new slot. You can start the upgrade process yourself at any time by following this procedure - [ Slot Upgrades - Additional Disk Space or Speed Requirements](https://www.feralhosting.com/faq/view?question=33).

**Q:** My plan end with `-3` but the new plans have `-4`, what does that mean?
---

A: All plans ending with `-4` are the current Cogent based offerings. If your plan ends with `-3` you are most likely still on and OVH based server awaiting to be transitioned over to Cogent. You can start the upgrade process yourself at any time by following this procedure - [ Slot Upgrades - Additional Disk Space or Speed Requirements](https://www.feralhosting.com/faq/view?question=33).

**Q:** Can I send emails from my slot?
---

A: Email has been blocked due to abuse from people attempting to spam. If you need to send email from your programs or Web Apps you can usually configure them to use an external smtp service like `Google Apps`. Here is an example of the configuration settings - [Google smtp settings](https://www.digitalocean.com/community/articles/how-to-use-google-s-smtp-server)

**Q:** Does my slot have a dedicated IP? 
---

A: You server has a dedicated IP that is shared by all the users on your server. So while you slot does have a dedicated IP, this IP is not unique to you.

**Q:** Is my server a dedicated server?
---

A: No, Feral does not provide any dedicated servers. You slot will on a server that is shared by other users.

**Q:** Where is my slot located? Where are the the servers hosted.
---

A: The servers are hosted at the [Interxion](http://www.interxion.com) carrier-neutral data centre in the [Netherlands](http://en.wikipedia.org/wiki/Netherlands).

**Q:** What software is installed on my slot?
---

A: You can check this yourself by using these command in [SSH](https://www.feralhosting.com/faq/view?question=12)

To see if a specific programs is installed you can do this, where `program-name` is the name of the program you want information about:

~~~
aptitude show program-name | grep State
~~~

To see every installed program use this commands to create a new file in your server root called `software.txt` that will list all installed programs:

~~~
dpkg --get-selections > ~/software.txt
~~~

**Q:** Can I install Deluge,rTorrent/rutorrent, rtorrent/wuTorrent and transmission or can I only use one?
---

A: You can install and use all four applications if you want. All software on the Install Software page can be installed at the same time and actively used. You can also run more than one instance of certain applications, like Deluge and rTorrent as well. Staff might not support or troubleshoot your second running instances though, but if they do it is at their discretion.

**Q:** Can I have my Slot IP changed?
---

A: If you can provide sufficient evidence to show that you justifiably need this, then you can open a ticket and provide the details of your case there.

**Q:** What OS is running on my slot / What version of Linux us running on my slot?
---

A: Your slot is running on Debian 7 Stable (wheezy)

This SSH command will show you your current Debian version

~~~
lsb_release -d
~~~

**Q:** OpenVPN - How many open and active connections can I have?
---

A: You can only have **1** active connection per OpenVPN server at any one time. This would usually mean one connected device at a time.

You can use [SSH tunnels](https://www.feralhosting.com/faq/view?question=37), as there is no limit on how many tunnels you can open and create.

**Q:** Disk quota - How can I check mine?
---

A: [Check your disk quota in SSH](https://www.feralhosting.com/faq/view?question=221) or use the provided Usage analyser in the manager [Usage](https://www.feralhosting.com/manager/slot/usage?) (note this URL might not take you to the right slot if you have more than one)

**Q:** What software or programs will Staff install on request for me, via tickets?
---

A: Feral do not support external or third party applications that they do not provide as part of their set-up. Though some things can be installed upon request.

1: [Packages Debian 7 stable (wheezy)](http://packages.debian.org/stable/) - You can make a request for versions of applications in this repository. You should provide your reasoning in the ticket (at the Staff's discretion).
 
2: Required dependencies of applications, such as Python libs. You should provide your reasoning in the ticket (at the Staff's discretion).

3: You can always raise a ticket and ask if you are unsure. This does not cover them installing or configuring applications for you. It is only for installing things that are part of the Debian stable repo, that are required for you to run your application.

**Q:** Can I share my account?
---

A: Feral only supports one user account. This means they will only provide and support one set of user credentials (your account username and password). If you wish to share these credentials you can, but you do so at your own risk. Anyone you share you SSH/SFTP/FTP pass with will have as much control/access to and over the slot as you do.

**1:** Recommended - Create limited and jailed users using this FAQ - [Installing an FTP daemon for extra accounts](https://www.feralhosting.com/faq/view?question=193) then share these credentials. This way they will never have total access to your slot.

**2:** Create them a public/private key pair that you can easily revoke so you do not have to share you main password - [Public Key Authentication for password-less login](https://www.feralhosting.com/faq/view?question=13). This still give them the same level of access that you have, but keys are simple to revoke.

**Q:** Can I use FTPS (also known as FTP-ES, FTP-SSL) on my feral slot.

A: Feral do not provide FTPS access as part of their set-up, only SFTP. You can however use this FAQ - [Installing an FTP daemon for extra accounts](https://www.feralhosting.com/faq/view?question=193) to set-up FTPS with limited users inside jailed directories.

**Q:** Is there test file for Feral?
---

A: Yes, here are some links:

[http://aphrodite.feralhosting.com/test.bin](http://aphrodite.feralhosting.com/test.bin)

[http://mirror.nl.leaseweb.net/speedtest/100mb.bin](http://mirror.nl.leaseweb.net/speedtest/100mb.bin)

[http://test.fiberring.net/100mb.bin](http://test.fiberring.net/100mb.bin)

[ftp://scarlet.feralhosting.com/8.0-RELEASE-amd64-disc1.iso](ftp://scarlet.feralhosting.com/8.0-RELEASE-amd64-disc1.iso)

**Q:** Deluge, how do I use plug-ins, RSS and or make torrents.
---

A: You will need to use the Thin client. Here is a FAQ on how to set up the thin client - [Deluge Daemon - Remote control with the local Thin client](https://www.feralhosting.com/faq/view?question=76)

**Q:** I have files with another service provider, can I bring them with me to Feral?
---

A: Yes, you can do this quite easily if you other provider has provided you with SSH access and rsync.

1: [Open a support ticket](https://www.feralhosting.com/manager/tickets/) and provide Staff with your SSH details for you old server and what files you want. They will then start the process of moving your files for you and keep you updated via the ticket.

2: You can move these files yourself if using this guide: [Transferring data from slot to slot](https://www.feralhosting.com/faq/view?question=117). The guide describes using rysnc to move files from one Feral slot to another during an upgrade. This method is identical in moving files from a non Feral server to a Feral server. 

Related FAQ: [Completing a data transfer](https://www.feralhosting.com/faq/view?question=122)

**Q:** Can I use public trackers with my Feral slot?
---

A: Feral supports and allows the use of public trackers. No need to ask or get permission.

**Q:** I want to upgrade or downgrade my slot what do I do?
---

A: To upgrade your slot please:

(1) Purchase the slot from our website. 
(2) Wait until you receive the slot. 
(3) Then open a ticket requesting a data transfer (optional).
(4) Request a refund on your current slot (optional).

This is the official Feral upgrade procedure. Any upgrade or downgrade involves the purchasing of a new physical slot. There is no way to expand or decrease your current slot specifications.

Open a ticket as soon as your purchased slot is allocated. This opens a dialogue between you and the staff and can deal with any issues that might be relevant, such as non payment of a slot and more. Staff are reasonable and friendly people, so don't be afraid to talk to them via the ticket with your concerns. Also be fair to them, don't leave things until the last minute.

Related FAQ: [Completing a data transfer](https://www.feralhosting.com/faq/view?question=122)
Related FAQ: [Using rsync to transfer files to a new slot](https://www.feralhosting.com/faq/view?question=117)
Related FAQ: [Slot Upgrades - Additional Disk Space or Speed Requirements](https://www.feralhosting.com/faq/view?question=33)
Related FAQ: [Late Payments](https://www.feralhosting.com/faq/view?question=8)

**Q:** Can I install my own software software?
---

A: Users do not have Root privileges so cannot use apt or packet managers to install software. See this FAQ for a more in depth explanation with many linked examples - [Generic Software Installation Guide](https://www.feralhosting.com/faq/view?question=195)

If you require and dependencies that are part of the Debian Stable branch, open a ticket and ask staff if they can install them. This is something they will do for users, but they will not support the installation or maintenance of software that they have not provided.

**Q:** Upload Traffic - What happens if I go over my quota?
---

A: Your upload will be throttled to 1Mbits for Cogent and 10Mbits for OVH for the duration of that monthly cycle.

**Q:** What counts to my Upload quota or Usage allowance?
---

A: Anything that is leaving(OUT) your server is upload. So anything your server has to send to you, such as an FTP/SFTP download, is something that is leaving the server. Anything Incoming(IN) is not counted to this usage.

**Q: ** Using SFTP
---

SFTP is the ideal and supported way to securely transfer data between the server and your home computer. SFTP is FTP over SSH. All Feral users have SSH access to their slots. Feral does not use or support FTPS for file transfer.

Here are a list of Windows and Mac FTP/SFTP clients:

**Windows Free Solutions:**

[WinSCP client](http://winscp.net/eng/download.php) Recommended - FTP/SFTP/keyfiles/Custom Commands e.g. unrar/Putty integration/parallel downloads
[Filezilla Client](https://filezilla-project.org/download.php?type=client) FTP/SFTP/keyfiles/parallel downloads
[Bitkinex Client](http://www.bitkinex.com/download) FTP/SFTP/keyfiles/Putty integration/parallel downloads/Segmented downloads

**Mac Free Solutions:**

[Filezilla Client](https://filezilla-project.org/download.php?type=client) FTP/SFTP/keyfiles/parallel downloads

Related tutorial: [WinSCP: Performing Common Tasks (Creating Torrents, Unrar'ing, Symlinks, etc)](https://www.feralhosting.com/faq/view?question=27)
Related tutorial: [FTP / SFTP using Filezilla](https://www.feralhosting.com/faq/view?question=187)
Related tutorial: [Installing an FTP daemon for extra accounts](https://www.feralhosting.com/faq/view?question=193)
Related tutorial: [Automated Sync from SeedBox to Home](https://www.feralhosting.com/faq/view?question=153)

**Q:** Using FTP
---

FTP is a second method for transferring files if SFTP is not available or slow. We recommend using the [FileZilla client](http://filezilla-project.org/download.php?type=client). It runs on all Major platforms. If you require more downloading power, please use a [multi-part](http://en.wikipedia.org/wiki/Download_acceleration) ftp client, like [Bitkinex Client](http://www.bitkinex.com/download) . There is a [Mac version](http://www.globalscape.com/cuteftpmacpro/) of CuteFTP as well.

Related tutorial: [What to Do If FTP Speeds Are Slow](https://www.feralhosting.com/faq/view?question=28)

**Q:** Using SSH
---

SSH is useful for complete control over your account and is used to help fix any problems. We recommend using the [PuTTy client](https://www.feralhosting.com/faq/view?question=12) on Windows. On Macs, you can just use terminal or xterm.

Related tutorial: [Connecting with Putty on Windows](https://www.feralhosting.com/faq/view?question=12)
Related tutorial: [SSH Tunnels Basic - PuTTy](https://www.feralhosting.com/faq/view?question=37)
Related tutorial: [Setting up Public Key Authentication for Password-less Login](https://www.feralhosting.com/faq/view?question=13)
Related tutorial: [SSH guide basics - Mac](https://www.feralhosting.com/faq/view?question=217)

**Q:** Using HTTP / WWW
---

Alternatively, you can use your preferred browser or a download manager to download your files via HTTP.

With the purchase of a slot you are given two unique WWW URLs for you to use:

`username.servername.feralhosting.com` < https has a cert mismatch issue due to the name format.

`servername.feralhosting.com/username` < https has a valid and matching SSL certificate for Feral sub domains.

These URLs represent the same location with two ways to reaching it. The files in one will be the same files in the other and vice versa.

Related tutorial: [Putting Your WWW Folder to Use](https://www.feralhosting.com/faq/view?question=20)
Related tutorial: [Forcing HTTPS](https://www.feralhosting.com/faq/view?question=161)
Related tutorial: [Password Protect your WWW](https://www.feralhosting.com/faq/view?question=22)

**Q:** Using extra domains / Hosting my own domain
---

You also have the option of getting an extra domain. Please read more [here](https://www.feralhosting.com/faq/view?question=52).

You can host a free domain or a domain you already own.



