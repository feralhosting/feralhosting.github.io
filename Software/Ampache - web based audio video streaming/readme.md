
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Streaming
---

Use VLC to stream with Ampache. It can now accept invalid SSL certificates. This script will also modify the `conf` to scan for `mkv` files in catalogues.

Ampache
---

**First:** go to the software install page for feralhosting at: [Install Software](https://www.feralhosting.com/manager/slot/install).

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/install_mysql.png)

**NOTE:** MYSQL can take up to 15 minutes to install as it is compiled upon request of installation so please be patient.

In SSH do these commands. Use this FAQ if you do not know how to SSH into your slot: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Installing Ampache on Feral slots.
---

You will need your MySQL details to complete this FAQ.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/mysql_socket.png)

The bash script
---

Because there are quite a few configuration and tweaks required to make Ampache work on your slot, a manual guide a bit too much since the bash script already automates it for you. For this reason there is only a bash script installer.

This bash script uses Ampache master from github and also applies some default configuration settings.

- Uses the github repo to install so is always up to date
- Makes a slight template modification to insert your mysql socket path into the installer.
- fixes ffmpeg path to use new updated static binary (ffmpeg 2.1) built 31.10.2013
- enables debug, logging and creates folders and modifies required paths.
- enables transcoding and related settings
- bumps memory limit to `2048` and creates a supporting `.htaccess` since Ampache cannot override this setting itself.
- changes minimum bitrate to `192`
- Allows `mkv` files to be scanned and added to catalogues

~~~
wget -qO ~/ampache.sh http://git.io/wESU5A && bash ~/ampache.sh
~~~

**Important note:** You must change this setting once you have access to the web interface for transcoding to work

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/streaming.png)

Don't forget to change it.

Post script installation
---

After you have used the bash script then navigate to this folder in your web browser, it should be like:

~~~
http://username.server.feralhosting.com/ampache/
~~~

Now you should come to a page where it should check so all your settings are OK, should say OK with a green text on all points there. Then you just press `Start Configuration`.

**Step 1:**

**Important note:** You mysql socket will be automatically entered for you in the hostname field. Refresh the page if you have removed it to get it back

Then you come to the page where you need the information from your MySQL installation on the Slot Details page for the relevant slot. You need your mysql root password.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/stage1.png)

**Step 2:**

Fill in the required information in the format shown in the image below:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/stage2.png)

This is what you see if the configuration file is successfully written:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/stage22.png)

Press `Proceed to step 3`. Create the admin account for your Ampache server, then go next and you should be finished with the setting up part.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/stage3.png)

Login with your admin account, to add where you keep your music you press `add catalog`, then navigate to the directory in which you keep all your music on your server via SSH. write `pwd` while in this directory. You should get the full filepath back, such as `/media/c0d7/home/user/private/rtorrent/data` , you fill this in under Path. and then write whatever you want under the catalog name. Then it should say catalogue created.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/login.png)

**Important note:** You must change this setting once you have access to the web interface for transcoding to work:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/streaming.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/catalogue.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/cataloguecreated.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ampache%20-%20web%20based%20audio%20video%20streaming/player.png)



