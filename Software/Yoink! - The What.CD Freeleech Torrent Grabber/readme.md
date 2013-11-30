
**Important notice:** This will download ALL freeleech torrents. At `28.10.2013` there was about `1610` torrents totalling `320GB`. This can change quite drastically in either direction so be careful.

Make sure you have the space to spare before running this script. You can cancel the script while it running by pressing and holding `CTRL` then pressing `c`. When you run the script again it will detect torrents it has already downloaded and continue from where it left off. Do this to grab some, check the space, do some more.

### Yoink! The Freeleech Torrent Grabber

[Yoink!](https://github.com/phracker/yoink)

In SSH do this command. Use this FAQ if you do not know how to SSH into your slot: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

### Download and prepare Yoink!

~~~
wget -qO ~/yoink.py https://raw.github.com/phracker/yoink/master/yoink.py
easy_install --user requests HTMLParser
python ~/yoink.py
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Yoink!%20-%20The%20What.CD%20Freeleech%20Torrent%20Grabber/1.png)

Now you will need to configure the `~/.yoinkrc` file:

Run this command to edit it with nano in SSH:

~~~
nano ~/.yoinkrc
~~~

Then Make these edits:

~~~
user:What.CDusername
password:What.CDWebsitePass
target:RelativePathToRtorrentWatchFolder
~~~

For example:

~~~
user:peterpan
password:sds32tsekjfsd893
target:~/private/rtorrent/watch
~~~

The press and hold `CTRL` then press `x` to save. Press `y` to confirm.

**Important note:** You can set the directory to anything to test the script is working. The script simply downloads the requested torrent files to the `target` directory.

For example:

~~~
mkdir -p ~/yoinktest
~~~

Then set the `target` in the `~/.yoinkrc` to:

~~~
user:peterpan
password:sds32tsekjfsd893
target:~/yoinktest
~~~

**Important note:** For Deluge you may want to: 

1: Set a custom location for your downloaded torrents

2: Use a cronjob to copy them to Deluge's watch folder. 

This so that your files are not removed from the target directory for Yoink to check what you have already downloaded. You only need to do this for deluge. Skip it otherwise.

Make this folder using this command:

~~~
mkdir -p ~/yoinkfiles
~~~

In your `~/.yoinkrc` use this target:

~~~
~/yoinkfiles
~~~

Now add this to your crontab.

~~~
crontab -e
~~~

Then add this at the end on a blank line

~~~
* * * * * cp -rf ~/yoinkfiles/. ~/private/deluge/watch
~~~

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

Now run the script again:

~~~
python ~/yoink.py
~~~

And all the torrents will be downloaded to `~/yoinktest/`. 

All you need to do once the script is running is wait for it to finish Yoinking.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Yoink!%20-%20The%20What.CD%20Freeleech%20Torrent%20Grabber/2.png)

### crontab

~~~
crontab -e
~~~

Add this line for it to run every hour, edit as you see fit:

~~~
00 * * * * python ~/yoink.py
~~~

Press and hold `CTRL` then press `x` to save. Press `y` to confirm and exit.



