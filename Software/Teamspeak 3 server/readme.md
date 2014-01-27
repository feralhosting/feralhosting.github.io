
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Error on Start up
---

If Teamspeak is not giving you the privilege key on first run you will need to check the logs at:

~~~
~/private/teamspeaks/logs
~~~

And look for this error

~~~
Server() error while starting servermanager, error: instance check error
~~~

It means Teamspeak is detecting another users instance and will not let you run yours, do this command in SSH to confirm:

~~~
ps -e | grep ts3server
~~~

If you get any results that means there is another instance running.

Sadly, there is no workaround right now for this issue. Your options are:

**1:** Try to get a non for profit license or purchase an annual license: [http://sales.teamspeakusa.com/licensing.php](http://sales.teamspeakusa.com/licensing.php)

**2:** Consider this alternative Voip Client called Mumble: [Mumble client and murmur server](https://www.feralhosting.com/faq/view?question=227)

Teamspeak 3 on Feral Slots.
---

To install this software using a custom bash script connect to your slot using SSH. If you don't know how to do this [here is a basic guide](https://www.feralhosting.com/faq/view?question=12):

~~~
wget -qO ~/install.teamspeak.sh http://git.io/aOACkQ && bash ~/install.teamspeak.sh
~~~

Once this script has been executed to completion once, one script is copied to your `~/bin` folder.

`~/teamspeak.sh` is copied to `~/bin/teamspeak`

Now you can simply type this from anywhere to execute the script: 

~~~
teamspeak
~~~

**Features:**

Installs and starts a new instance of `3.0.10.3`

Sets up the `ts3server.ini` for the user automatically.

Detects previous version from installed to the same path or from the script and gives the choice to:

Kill the last known PID and delete the folders. A fresh install.

In place Upgrade. Overwrites the core files with new one. Leaves the sq DB and `ts3server.ini` intact.

**Post Script installation:**

The bash script creates a symbolic link to the main `ts3server_startscript.sh` in your `~/bin` directory.

Once teamspeak 3 has been installed using the bash script you can use these easy commands to control it:

~~~
ts3server start
ts3server stop
ts3server restart
~~~

Please see the rest of this FAQ for client set-up using your privilege key.

Manual Installation steps:
---

We need the `Linux Server amd64 3.0.10.3`  which you can download manually and then upload to your server. Please just upload the zip to your server root/home folder to keep in line with the rest of the guide.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/0.png)

[http://www.teamspeak.com/?page=downloads](http://www.teamspeak.com/?page=downloads)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/0.1.png)

Download the server:

~~~
wget -qO ~/teamspeak.tar.gz http://dl.4players.de/ts/releases/3.0.10.3/teamspeak3-server_linux-amd64-3.0.10.3.tar.gz
tar xf ~/teamspeak.tar.gz
cp -rf ~/teamspeak3-server_linux-amd64/. ~/private/teamspeak
rm -rf ~/teamspeak3-server_linux-amd64 ~/teamspeak.tar.gz
~~~

Open the file with nano:

~~~
nano ~/private/teamspeak/ts3server.ini
~~~

Copy and paste this code below:

~~~
machine_id=
default_voice_port=port number between 6,000 and 30,000
voice_ip=0.0.0.0
licensepath=
filetransfer_port=port number between 30,001 and 40,000
filetransfer_ip=0.0.0.0
query_port=port number between 40,001 and 50,000
query_ip=0.0.0.0
query_ip_whitelist=query_ip_whitelist.txt
query_ip_blacklist=query_ip_blacklist.txt
dbplugin=ts3db_sqlite3
dbpluginparameter=
dbsqlpath=sql/
dbsqlcreatepath=create_sqlite/
dblogkeepdays=90
logpath=logs
logquerycommands=0
dbclientkeepdays=30
~~~

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

Do these commands in SSH. They will edit the required sections for you using random numbers.

~~~
sed -i "s|default_voice_port=.*|default_voice_port=$(shuf -i 6000-30000 -n 1)|g" ~/private/teamspeak/ts3server.ini
sed -i "s|filetransfer_port=.*|filetransfer_port=$(shuf -i 30001-40000 -n 1)|g" ~/private/teamspeak/ts3server.ini
sed -i "s|query_port=.*|query_port=$(shuf -i 40001-50000 -n 1)|g" ~/private/teamspeak/ts3server.ini
~~~

Your final file will look something like this.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/3.png)

~~~
sed -i 's|COMMANDLINE_PARAMETERS="${2}"|COMMANDLINE_PARAMETERS="${2} inifile=ts3server.ini"|g' ~/private/teamspeak/ts3server_startscript.sh
~~~

Once you have done this type:

~~~
bash ~/private/teamspeak/ts3server_startscript.sh start
~~~

This will start the teamspeak server.

The Output should look like this.

**Important note:** If you don't get the info see the note at the top of this FAQ.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/4.png)

**It is very important you do not lose this information until you have entered it into the Teampseak Client. So copy ( by highlighting in putty ) and paste into a text editor of your choosing until we need it in a couple of steps**

Get the `Hostname:Default_voice_port` to use when connecting with this command.

~~~
echo "$(hostname):$(sed -n -e 's/default_voice_port=\(.*\)/\1/p' ~/private/teamspeak/ts3server.ini)"
~~~

Teamspeak 3 Client
---

Download and install the Teamspeak 3 client for your platform from: [http://www.teamspeak.com/?page=downloads](http://www.teamspeak.com/?page=downloads)

Once you have installed it run the app and click on connections.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/4.5.png)

Enter you hostname and voice port from the command above. Other settings can be tweaked once you have become Server Query.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/5.png)

On first connect you will see this. Copy and paste the privilege key that was printed in SSH when the teamspeak server was first run.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/6.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/7.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/8.png)

If you see this then you have completed this guide.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Teamspeak%203%20server/9.png)

**Notes:** 

On a default installation your are limited to `32` clients. This is more than enough for a few friends and more. If you require more you can apply for a **Not for Profit License** and use up to `512` clients.

[Teamspeak Not for Profit License](http://forum.teamspeak.com/showthread.php/48339-How-to-obtain-a-Non-Profit-License-%28NPL%29-and-Increase-Your-Virtual-Servers-Slots)

If you cannot connect then check the logs in `~/private/teamspeak/logs`. If you do not see the IP or ports you configured then to you have either not created the `ts3server.ini` properly or edited the start script correctly. Check over those steps again then stop the server and restart it.

To stop/restart the server for any reason you use the commands start / stop / restart

~~~
bash ~/private/teamspeak/ts3server_startscript.sh start
~~~

~~~
bash ~/private/teamspeak/ts3server_startscript.sh stop
~~~

~~~
bash ~/private/teamspeak/ts3server_startscript.sh restart
~~~



