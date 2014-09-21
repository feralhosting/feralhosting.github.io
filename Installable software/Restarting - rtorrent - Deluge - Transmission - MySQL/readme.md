
**Important note:** An optional way to restart/reset software is to install it again from the software page - this will leave data intact, but will reset configuration, passwords, RSS feeds and custom folders.

Bash script
---

Here is a simple bash script for restarting rtorrent,deluge, transmission (kill only) and mysql with some checks to see they restarted. The script performs the basic kill and restart (where applicable) functions outlined in this FAQ.

If you get errors on restarting a particular program or they fail to start, refer back to this FAQ for troubleshooting.

~~~
wget -qO ~/restart.sh http://git.io/5Uw8Gw && bash ~/restart.sh
~~~

### Manually restarting programs

Copy and paste commands directly as written in this FAQ.

Restarting rtorrent
---

Run the following commands through [SSH](https://www.feralhosting.com/faq/view?question=12).

**Step 1:** Kill rtorrent
 
~~~
killall -9 -u $(whoami) rtorrent
~~~

**Step 2:** Start it again in a screen

~~~
screen -S rtorrent rtorrent
~~~

If all goes well, you should be greeted with your rtorrent  and you should see your torrents. To exit rtorrent (and keep it running) press and hold `CTRL` and `a` then press `d` to detach from the screen once you are sure rtorrent is running.

If you are given a `screen is terminating` error, please consult the commands in Step 3.0

**Step 3.0:** Screen is terminating error

Attempt to start rtorrent using this command:

~~~
rtorrent
~~~

You will now usually see the error that rtorrent it throwing out.
 
You can try this in some cases: 

~~~
rm -rf ~/private/rtorrent/work/rtorrent.*
~~~

If the error means nothing to you can [open a ticket](https://www.feralhosting.com/manager/tickets/new) or ask on [IRC](https://www.feralhosting.com/chat) for help.

**3.1:** Start it again in a screen once you have resolved the errors:

~~~
screen -S rtorrent rtorrent
~~~

If all goes well, you should be greeted with your rtorrent  and you should see your torrents. To exit rtorrent (and keep it running) press and hold `CTRL` and `a` then press `d` to detach from the screen once you are sure rtorrent is running.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Restarting%20-%20rtorrent%20-%20Deluge%20-%20Transmission%20-%20MySQL/1.png)

Restarting Transmission
---

Run the following commands in [SSH](https://www.feralhosting.com/faq/view?question=12).

**1:** Kill transmission

~~~
killall -9 -u $(whoami) transmission-daemon
~~~

**Important note:**  Transmission cannot be started by the user and will be started by the system instead. After killing the process allow up to 5 minutes for it to automatically to restart.

You can do this to see if the process has restarted:

~~~
ps x | grep transmission | grep -v grep
~~~

You will see this if the process is running.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Restarting%20-%20rtorrent%20-%20Deluge%20-%20Transmission%20-%20MySQL/transmission.png)

Restarting Deluge
---

Run the following commands through [ SSH](https://www.feralhosting.com/faq/view?question=12).

Use the commands you need to kill and start the deluge daemon and Web Gui:

### Kill the deluge daemon and Web Gui

**Option 1:** Kill deluge only

~~~
killall -9 -u $(whoami) deluged
~~~

**Option 2:** Kill the Web Gui only

~~~
killall -9 -u $(whoami) deluge-web
~~~

**Option 3** This command would kill the deluge process and the web gui together

~~~
killall -9 -u $(whoami) deluged deluge-web
~~~

### Restart the deluge daemon and Web Gui

**Option 1:** Start deluge only

~~~
deluged
~~~

**Option 2:** Start the Web Gui only

~~~
deluge-web --fork
~~~

**Option 3:** This command would start the deluge process and the Web Gui together

~~~
deluged && deluge-web --fork
~~~

If all goes well, you should be greeted with an empty command prompt:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Restarting%20-%20rtorrent%20-%20Deluge%20-%20Transmission%20-%20MySQL/3.png)

If you get this error you will need to open a [support ticket](https://www.feralhosting.com/manager/tickets/new) with a relevant title. This problem requires Staff to fix.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Restarting%20-%20rtorrent%20-%20Deluge%20-%20Transmission%20-%20MySQL/twisted.png)

Do this command to see if they are running:

~~~
ps x | grep deluge | grep -v grep
~~~

If the processes are running the result will look like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Restarting%20-%20rtorrent%20-%20Deluge%20-%20Transmission%20-%20MySQL/deluge.png)

### Restarting MySQL

Run the following commands through [ SSH](https://www.feralhosting.com/faq/view?question=12). (Copy and paste these commands directly as written). 

**1:** Kill mysql

~~~
killall -9 -u $(whoami) mysqld mysqld_safe
~~~

**2:** Start mysql

~~~
bash ~/private/mysql/launch.sh
~~~

If all goes well, you should be greeted by two messages like the ones below

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Restarting%20-%20rtorrent%20-%20Deluge%20-%20Transmission%20-%20MySQL/4.png)

**Finally...**

If you continue to have problems after following these steps closely, please open a support ticket providing details of the error message you are receiving for which software and we will gladly help you.



