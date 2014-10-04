
### WhatFreeGrab - a Python freeleech grabber for what.cd

Approved by what.cd staff. [The Original thread on what.cd](https://what.cd/forums.php?action=viewthread&threadid=183793)

[https://github.com/emjaytee404/whatfreegrab](https://github.com/emjaytee404/whatfreegrab)

Installation:
---

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH guide basics - PuTTy](https://www.feralhosting.com/faq/view?question=12) or [SSH guide basics - OS X](https://www.feralhosting.com/faq/view?question=217)

~~~
git clone https://github.com/emjaytee404/whatfreegrab.git ~/whatfreegrab
python ~/whatfreegrab/WFG-setup.py
~~~

You will see something like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/install-1.png)

If you do not have the required dependencies the script will detect this and ask if you want to download them.

**Important note:** This is the recommended way, but if you wish to install the modules globally for your user please see this FAQ: [Python - Usage and Installation](https://www.feralhosting.com/faq/view?question=204)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/install-2.png)

If you have already satisfied the dependency requirements you will see something like this.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/install-3.png)

Credentials:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/credentials.png)

Here you will need to enter your What.CD username and password. Once you have done this press enter to continue.

If you get this error:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/error.png)

This is because the `whatfreegrab` script requires a newer version of `requests` than provided the Debian (if it has been installed system wide on user request). To fix this you need to install `reqeusts` locally. Please see this FAQ for installing modules locally to override system wide modules.

[Python - Usage and Installation](https://www.feralhosting.com/faq/view?question=204)

Torrents Directory
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/target-1.png)

You will be asked to provide a directory for your download torrents. This can be anywhere you like.

**Important notes:** If the directory structure does not exist it will be created. So there are two things to note about this when selecting a location for the torrents:

1: A full path or using the `~` will be the best option to make sure the correct location is used. For example the FAQ uses `~/torrents`. This will create a new folder in your slot root called `torrents` regardless of other conditions.

2: Using a relative path such as `some/path/to/torrents/` the directory structure will be created based on where you are located in SSH and how you execute the script. For example, `python ~/whatfreegrab/wfg.py` will create the directory structure from the slot root down, so you would have `~/some/path/to/torrents/` while `cd ~/whatfreegrab` then doing `python wfg.py` will create the directory structure relative to this location, giving us `~/whatfreegrab/some/path/to/torrents/`

**Recommended:** Use one of the default watch folders for torrent clients:

~~~
~/private/rtorrent/watch
~/private/transmission/watch
~/private/deluge/watch
~~~

**Blackhole:**

The example image uses a neutral location to store downloaded torrents. This folder will be created for us if it does not already exist when the script runs.

~~~
~/torrents
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/target-2.png)

Setup Final Stages:
---

The setup script will then provide us with some useful information:

**1:** The location of the configuration file.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/final-1.png)

**2:** Script options

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/final-2.png)

**3:** A cronjob for use with the script. Take note of this for after the setup script has finished.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/final-3.png)

**4:** And we are done with the setup script.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/final-4.png)

Running the script:
---

**Important note:** Remember, running this script more than once an hour is considered abusive by what.cd. Your account can be banned for running `whatfreegrab` too often.

**Manually:**

Now to run the script run this command whenever you want to get the latest freeleech torrents:

~~~
python ~/whatfreegrab/WFG.py
~~~

**Automatically:**

When the set-up script is run it will generate a cron job for us. For example the FAQs generated cronjob was:

~~~
56 * * * * python2 /media/DiskID/home/username/whatfreegrab/WFG.py
~~~

This will run hourly on the 56th minute of every hour. There is no need to have it run every 5 minutes.

Adding a cronjob:
---

To add a cron do this command in SSH:

~~~
crontab -e
~~~

The using the arrows keys on your board, move down to the last empty line. 

Once you are done then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

Optional - Copy files with cron
---

If you use the blackhole option you will need to copy your torrent files to the desired watchfolder using a cronjob

~~~
* * * * * cp -f ~/torrents/. ~/private/deluge/watch/
~~~

~~~
* * * * * cp -f ~/torrents/. ~/private/rtorrent/watch/
~~~

~~~
* * * * * cp -f ~/torrents/. ~/private/transmission/watch/
~~~

Notes
---

To simply reconfigure the script you can rerun the set-up or edit the configuration file:

**Run the set-up script:**

~~~
python ~/whatfreegrab/WFG-setup.py
~~~

**Edit the configuration file:**

~~~
nano ~/whatfreegrab/wfg.cfg
~~~

**Reset the script** (downloaded torrents and similar):

This script will remember what it has previously download even if the torrent files get deleted. This will cause `whatfreegrab` to re-download any torrents it previously grabbed.

~~~
rm -f ~/whatfreegrab/wfg.dat
~~~

Then run the script again:

~~~
python ~/whatfreegrab/WFG.py
~~~

**Updating the script:**

~~~
cd ~/whatfreegrab
git pull
~~~



