
![](http://i.imgur.com/LxxHuH4.png)

This script will send a [Growl (OSX)](http://growl.info/) / [Growl (linux)](http://mattn.github.io/growl-for-linux/) / [Growl/Snarl (Windows)](http://www.prowlapp.com/faq.php#windows) notification when you add a torrent and when the torrent is completed. By default it sends a notification for every torrent, but it can be customized based on watch folder or torrent label.

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

**Step 1**. SSH into your slot.

**Step 2**. Run the below commands

~~~
wget -qO ~/growltorrent.py http://btp.me.uk/growltorrent.py
echo "system.method.set_key = event.download.finished,notify_finished,"execute=python,$PWD/growltorrent.py,--finished,$d.get_name="" >> ~/.rtorrent.rc
echo "system.method.set_key = event.download.inserted_new,notify_inserted_new,"execute=python,$PWD/growltorrent.py,--inserted-new,$d.get_name="" >> ~/.rtorrent.rc
~~~

**Step 3.** Restart your rtorrent

~~~
killall -9 -u $(whoami) rtorrent
screen -dmS rtorrent rtorrent
~~~

**Step 4.** Install the necessary Python library

~~~
easy_install --user gntp
~~~

**Step 5.**. Edit growltorrent.py to include the appropriate information.

Replace hostname with your IP address. The password field is optional (remove the word test and leave "" for no password). You must set the same password in your Growl settings on your computer.

~~~
CONFIG = {
    "hostname": "123.45.67.89",
    "password": "test"
}
~~~

Optionally, change the `ICON_URL` to whatever image you'd like to use as the notification icon. It is currently:

![](http://i.imgur.com/okXCIsQ.png)

~~~
ICON_URL = "http://i.imgur.com/okXCIsQ.png"
~~~

**Step 6.** Be sure to allow network connections in your growl preferences and to forward/open port `23053` on your router. 

You can test your setup with the following commands

~~~
./growltorrent.py --finished "OMG A TORRENT FINISHED"
./growltorrent.py --inserted-new "OMG A TORRENT WAS ADDED"
~~~



