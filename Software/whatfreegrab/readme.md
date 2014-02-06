
### WhatFreeGrab - a Python freeleech grabber for what.cd

Approved by what.cd staff. [The Original thread on what.cd](https://what.cd/forums.php?action=viewthread&threadid=183793)

~~~
easy_install --user requests HTMLParser
mkdir -p ~/whatfreegrab/torrents
wget -qO ~/whatfreegrab/WFG.py https://whatfreegrab.googlecode.com/git/WFG.py
python ~/whatfreegrab/WFG.py
~~~

Now you will see something like this:

1: Enter your what.cd username and password when prompted.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/1.png)

2: use `~/whatfreegrab/torrents` as the directory for downloading `.torrent` files.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/2.png)

Press enter to begin the script.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/whatfreegrab/3.png)

### Copy files with cron

I recommend that you use a static folder location and not a watch folder for the target.

Then use a cron job to copy the file to where you need. Where `myfolder` is the path that you used in the `wfg.cfg`

~~~
* * * * * cp -rf ~/whatfreegrab/torrents/. ~/private/deluge/watch
~~~
~~~
* * * * * cp -rf ~/whatfreegrab/torrents/. ~/private/rtorrent/watch
~~~
~~~
* * * * * cp -rf ~/whatfreegrab/torrents/. ~/private/transmission/watch
~~~

To add a cron do this command in SSH:

~~~
crontab -e
~~~

The using the arrows keys on your board, move down to the last empty line. 

Once you are done then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

### Running the script:

Now to run the script run this command

~~~
python ~/whatfreegrab/WFG.py
~~~

### Notes

This script will remember what it has previously download even if the torrent files get deleted.

**Reset the script:**

You will need to delete this file:

~~~
rm -f ~/whatfreegrab/wfg.dat
~~~

Then run the script again:

~~~
python ~/whatfreegrab/WFG.py
~~~

Editing the `~/whatfreegrab/wfg.cfg`. You must delete the `~/whatfreegrab/wfg.dat` for changes to take effect.

**Updating the script:**

~~~
rm -f ~/whatfreegrab/wfg.cfg ~/whatfreegrab/wfg.dat
wget -qO ~/whatfreegrab/WFG.py https://whatfreegrab.googlecode.com/git/WFG.py
~~~



