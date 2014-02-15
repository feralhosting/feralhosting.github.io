
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Installation
---

This script will set-up couchpotato and automatically proxypass it for you on Apache and/or nginx, if it is installed and then run it in the background.

~~~
wget -qO ~/couchpotato.sh http://git.io/NWQA2Q && bash ~/couchpotato.sh
~~~

**Important notes:** 

**1:** If you get an empty blue screen in your browser press F5 (or CTRL + F5) to reload the page. That is all you should need to do.

**2:** It may take a minute or two for the URL given in the script to work so be patient. Press F5 to reload the URL.

**Run the CouchPotato Wizard**

Visit the URL shown in SSH after the script completes. It will be in this format:

~~~
https://server.feralhosting.com/username/couchpotato
~~~

**Set a username and password**

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/1.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/2.png)

Make sure to set a username and password. This is important, otherwise anyone can get access, and automatically start downloads on your slot.

**Set the directory to download the NZB/torrent to**


Under Downloaders, the default option is Black Hole, which will just download the NZB/torrent to a folder. You should set the directory to wherever your client watches.

By default, that should be:

~~~
/media/DiskID/home/username/private/client/watch
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/3.png)

Make sure to replace **client** with whichever client you use, for example, `/private/rtorrent/watch`.

CouchPotato also has support for other clients, such as Transmission, which allows it to interact directly with the client, but information for these isn't be included here.

**6: Complete the rest of the wizard**

Fill in any sites that you are a member of. 

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/4.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/5.png)

Enabling renaming is optional, and isn't covered in this FAQ.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/6.png)

Optional:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/7.png)

Click this Green link to finish the wizard:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/8.png)

Login to couchpotato and enjoy!

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/CouchPotato%20-%20An%20automatic%20NZB%20and%20torrent%20downloader%20for%20Films/9.png)



