
### WhatFreeGrab - a Python freeleech grabber for what.cd

Approved by what.cd staff. [The Original thread on what.cd](https://what.cd/forums.php?action=viewthread&threadid=183793)

~~~
easy_install --user requests HTMLParser
git clone https://code.google.com/p/whatfreegrab/ ~/whatfreegrab
nano ~/whatfreegrab/wfg.cfg
~~~

Now you will see something like this:

~~~
[login]
username = 
password = 

[download]
target = 
template_music = ${torrentId}. ${artist} - ${groupName} - ${groupYear} (${media} - ${format} - ${encoding})
template_other = ${torrentId}. ${groupName}
~~~

Enter your what.cd username and pass:

~~~
[login]
username = username
password = PASSWORD
~~~

In this section enter the relative path to the download directory from, your root, you have selected.

**Important note:** Please use a static folder location and not a watch folder. See below for how to use cron jobs with this folder to copy file.

The script will create the required directories for you if they do not exist.

~~~
[download]
target = myfolder
template_music = ${torrentId}. ${artist} - ${groupName} - ${groupYear} (${media} - ${format} - ${encoding})
template_other = ${torrentId}. ${groupName}
~~~

**Important note:** When using a directory path it will be relative to the command used to execute the script:

For example `myfolder` is the same as `~/myfolder` in this example since we are running the script like this `python ~/whatfreegrab/WFG.py` You could also do `myfolder/12345` and the result will be `~/myfolder/12345`.

If you did `cd ~/whatfreegrab` and then `python WFG.py` the folder path would be relative to this location and you will end up with `~/whatfreegrab/myfolder` after executing the script.

### Save your changes

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

### Copy files with cron

I recommend that you use a static folder location and not a watch folder for the target.

Then use a cron job to copy the file to where you need. Where `myfolder` is the path that you used in the `wfg.cfg`

~~~
* * * * * cp -rf ~/myfolder/. ~/private/deluge/watch
~~~
~~~
* * * * * cp -rf ~/myfolder/. ~/private/rtorrent/watch
~~~
~~~
* * * * * cp -rf ~/myfolder/. ~/private/transmission/watch
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
cd ~/whatfreegrab && git pull origin
~~~



