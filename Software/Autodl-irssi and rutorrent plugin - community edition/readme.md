
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

rtorrent change 30.06.2013
---

rtorrent was changed to use a socket and this has broken the way autodl rutorrent plugin and autodl connect to each other. Both sides will need to be patched for it to work again.

If you see this error in your rutorrent Web Gui:

~~~
Error downloading files. Make sure autodl-irssi is started and configured properly (eg. password, port number): Error getting files listing: Error: Could not connect: (111) Connection refused
~~~

You must apply this fix:

~~~
wget -qO ~/autodlrutorrentfix.sh http://git.io/BBUryw && bash ~/autodlrutorrentfix.sh
~~~

Reset the password and port for autodl and the rutorrent plugin
---

This script will ask you for you password and then update the `autodl.cfg` and the rutorrent `conf.php` and then restart irssi.

~~~
wget -qO ~/autodlport.sh http://git.io/vCft_Q && bash ~/autodlport.sh
~~~

What's changed from the original Autodl to the new github release?
---

The main application on [ autodl on Sourceforge](http://sourceforge.net/projects/autodl-irssi/) was not being actively developed and the author was M.I.A. The official forum was removed also. This is a new community driven version that has been forked to [autodl on github.com](https://github.com/autodl-community/autodl-irssi) and is now actively maintained, updated and developed. It is also the new home of the new wiki and other information resources.

Installing autodl-irssi
---

This FAQ requires you SSH into your box. You can read more about how to SSH into your box here: [SSH Guide Basic](https://www.feralhosting.com/faq/view?question=12)

After you’re connected to your box, run the following commands:

We highly recommend that you perform a clean install when switching from the official release of autodl-irssi to prevent any possible conflicts. Running these commands in your terminal or deleting that directory through an FTP client is suggested:

**Important note:** These commands do not delete the `~/.autodl` folder or the `~/.autodl/autodl.cfg` but this file will be overwritten during manual installation below so please back it up now if you need it.

~~~
killall -9 irssi -u $(whoami); screen -wipe
cp -f ~/.autodl/autodl.cfg ~/.autodl/autodl.cfg.bak
cd && rm -rf .irssi/scripts/AutodlIrssi .irssi/scripts/autorun/autodl-irssi.pl
cd && rm -rf www/$(whoami).$(hostname)/public_html/rutorrent/plugins/autodl-irssi
~~~

Automated installation using the bash script
---

After SSH'ing into your slot run the following command:

~~~
wget -qO ~/install.autodl.sh http://git.io/oTUCMg && bash ~/install.autodl.sh
~~~

**Important note:** The script does not delete the `autodl.cfg`. It will only edit the `port` and `password` of any existing `autodl.cfg` and will back it up first just in case.

What the script does?

Backs up any existing `~/.autodl.autodl.cfg` files by renaming it to `autodl.cfg.bak`
Downloads the latest Autodl  and Autodl rutorrent plugin.
Applies the latest updates for trackers.
Generates a port and password (random 20 mixed case alphanumerical) for the user and updates or creates the `autodl.cfg` and corresponding rutorrent plugin
Applies the Autodl and rutorrent plugin fixes.
Starts irssi in a background screen process
Updates Autodl to make sure the app is aware it is current for first use by the user.
Prints helpful info in SSH.

Manual installation
---

~~~
mkdir -p ~/.irssi/scripts/autorun ~/.autodl
echo -e "[options]\ngui-server-port = 0\ngui-server-password = PASS" > ~/.autodl/autodl.cfg
wget -qO ~/autodl-irssi.zip http://update.autodl-community.com/autodl-irssi-community.zip
unzip -qo ~/autodl-irssi.zip -d ~/.irssi/scripts/
cp -f ~/.irssi/scripts/autodl-irssi.pl ~/.irssi/scripts/autorun/
cd && rm -f autodl-irssi.zip .irssi/scripts/{README*,autodl-irssi.pl,CONTRIBUTING.md}
~~~

Configuring your autodl-irssi connection to the autodl-irssi rutorrent plugin. This step is not required. If you don’t want to use the UI configuration editor, 

To configure autodl-irssi for rutorrent:

You can use any torrent client. You just need the rutorrent UI installed to use this feature.

~~~
nano ~/.autodl/autodl.cfg
~~~

The `autodl.cfg` it will look like this

~~~
[options]
gui-server-port = 0
gui-server-password = PASS
~~~

**1:** Change the port to something between `6000` and `50000`

**2:** Create a password and replace `PASS` with your new password.

Save the file by Pressing **CTRL X** then **Y**

**These next commands are to download and then edit the GUI plugin to connect with the process. And are required if you wish to use the rutorrent GUI to manage autodl-irssi.**

~~~
cd ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/
wget -qO autodl-rutorrent.zip https://github.com/autodl-community/autodl-rutorrent/archive/master.zip
unzip -qo autodl-rutorrent.zip
cp -rf autodl-rutorrent-master/. autodl-irssi
rm -rf autodl-rutorrent.zip autodl-rutorrent-master
cp -f autodl-irssi/_conf.php autodl-irssi/conf.php
nano autodl-irssi/conf.php
~~~

**Edit this info:**

~~~
$autodlPort = 15896; // Set the same port value as you set earlier (the one in ~/.autodl/autodl.cfg)
~~~

~~~
$autodlPassword = "ey47DT7heE7E8"; // Set the same password as before (while editing ~/.autodl/autodl.cfg)
~~~

Save the file by Pressing **CTRL X** then **Y**

**Run Irssi in a screen**
 
~~~
screen -dmS autodl irssi
~~~

Press and hold **CTRL A D** ( in that order ) to detach from the screen leaving the process running in the background.

To re attach to this screen in SSH to control irssi type this command in your shell:

~~~
screen -r autodl
~~~

**Using rutorrent autodl-irssi plugin:**

Check out the Wiki Page.

[https://github.com/autodl-community/autodl-irssi/wiki/_pages](https://github.com/autodl-community/autodl-irssi/wiki/_pages)

** Updating **

If you are running the autodl-irssi-community version (installed here) and `NOT` the autodl-irssi version from months ago, you can update to the latest plugin version by re-running these steps, or running the following command in irssi:

**Important note:** If you update the core program files (not just not the trackers) you will have to run the fix script at the top of this FAQ again.

Inside the screen you would type this into `irssi`:

~~~
/autodl update
~~~



