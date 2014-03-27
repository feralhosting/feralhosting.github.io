
This FAQ will explain, how you can sync specific folders to a raspberry pi, using cron and rsync. Furthermore, this guide stands out, when we come to the cron part. In most setups, you will not be able to see the ETA / download speed, if it’s a cronjob running it. This was made possible, from the help of **konichiwa** and **ozymandias**. In addition, we will be running the crontab in sudo, as this can come in handy, if you want to add different jobs, like restarting the pi. However, this is optional. 

Step 1: SSH into your pi
---

I strongly recommend to SSH into your pi, so you can just copy and paste the code, directly to the pi.

**1:** First, we want to open the SSH from outside sources. To do that, you will have to connect your pi to your monitor, and plug in a keyboard. (Mouse not needed). Log into your pi by using:

**Username:** `pi`

**Password default:** `raspberry`

To get into the config of the pi, type:

~~~
sudo raspi-config
~~~

That will get you into a GUI.

A super good idea, is first to `expand filesystem` then `Change User Password`. Now `Add to Rastrack` and `Internationalisation Options`. Here you can change the language if you want to, as well as the keyboard layout, and time zone. It is also safe, to enter the `Overclock` settings, and chose the preset `medium`. If you do this, you will also have to reboot the pi, before we continue. You are prompted for that. If not, type:

~~~
sudo reboot
~~~

Now to enable the SSH access.  Enter `Advanced Options`, then `SSH`, and `Enable`. 

Before we exit, go into `Advanced Options` again, and choose `Update`. This will update the entire pi. It will take `3` to `10` min, depending on overclock, and your SD card’s speed class. 

An SD card speed class 10 can have a noticeable difference difference in large file transfers. Just as big as going from HDD to SSD on a computer, if not bigger.

Reboot your pi, by using:

~~~
sudo reboot
~~~

Go ahead, and unplug the pi form you monitor, as well as your keyboard.

**2:** Now on your regular computer, you will need to connect to the pi.

To do that, follow this guide: [SSH](https://www.feralhosting.com/faq/view?question=12). Just replace `server.feralhosting.com`, with the IP of your raspberry pi.

Step 2: Installing rsync
---

Since I want to make this using `sudo`, i will do this:

~~~
sudo crontab –e
~~~

and not just using this command:

~~~
crontab –e
~~~

I will be running everything with `sudo` in front of every command. This is especially important, when we make the SSH-keys, since `sudo` will store the keys in different places.

If you don’t want to use this command:

~~~
sudo crontab –e
~~~

but prefer to only use this version:

~~~
crontab –e
~~~

Then don’t use `sudo` at all.

**1: rsync** To install rsync, SSH into your pi, and run this command:

~~~
sudo apt-get install rsync
~~~

We will leave that for now, since we will make the SSH-keys first.

Step 3: Install SSH-keys
---

We want SSH-keys with no passphrase, since it is supposed to do the sync by its own, automatically.

**1: Making the keys**

First, go to the SSH screen of the pi.
Remember, if you want to use 

~~~
sudo crontab –e
~~~

Use sudo, or if you chose not to use sudo:

~~~
crontab –e
~~~

Then run this command:

~~~
sudo ssh-keygen -q -t rsa -b 2048 -N ''
~~~

You can specify a name and path for this file if you want using the `-f` argument:

~~~
sudo ssh-keygen -q -f "/root/.ssh/mykey.pub" -t rsa -b 2048 -N ''
~~~

This will create a key, with no passphrase. It will hang for some time. When is asks where to save it, just press enter, since we want it in the default directory.

Now we want to transfer the public key, to feralhosting.

Type this command:

~~~
sudo ssh-copy-id -i /root/.ssh/id_rsa.pub user@server.feralhosting.com
~~~

Done with the SSH-keys.

Step 4: Making the rsync script
---

We want to make many of these commands, and we want them to be run every 5 min. But if we simply put this into cron, cron will run it every 5 min. Since it’s unlikely that the first will be done in 5 min, multiple rsync’s will begin, downloading the same file. Then finally crash the pi. We would very much wan, to avoid this:

There is this thing called flock. It will create a `flocktmp.lock` file, denying any new rsync’s beginning, until the first one is done. We can simply not use this for all the rsync commands. That’s why we are going to put all the rsync’s, into one script.

**1: The script**

In the pi’s terminal, type:

~~~
sudo mkdir $HOME/scripts/
~~~

Now we have the directory, and we now want to make the script. Type:

~~~
sudo nano $HOME/scripts/SB_sync
~~~

Since we want to make a shell script, type this at the top:

~~~
 #!/bin/sh
~~~

**2: Making the rsync command**

On the FOURTH line (keep two empty lines under `#!/bin/sh`), we are now ready to make the rsync command. Here is an example:
~~~
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"path/to/remote/dir/"' "/path/to/store/on/pi" 2>&1 > /home/pi/SB_sync_logs/1.name.of.folder.log 
~~~

I’ve already set up my hard drive to my pi, and I want to sync my folder called `iRL HD`
So MY rsync command would look like this:

~~~
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/iRL HD/"' "/media/HDD01/shares/SB/iRL HD" 2>&1 > /home/pi/SB_sync_logs/1.iRL.HD.log
~~~

For now, exit using `ctrl+x`, then `y` and enter, to save the script.
We also want this to be executable.
To do that, type:

~~~
sudo chmod +x $HOME/scripts/SB_sync
~~~

What this basically does `--chmod=a+rwx`, is setting the permissions on the downloaded files, so EVEYONE gets access to it. The permission are equal to `chmod 777`. 
What the –delete parameter does, is to delete the files on the pi, if they are deleted from the seedbox. If you don’t want this, you can simply remove the `–delete` parameter, and the pi won’t delete anything, only download.
What is the `2>&1 >` for? That I will explain later. But it’s related to our little cron trick. 

Step 5: The cron trick
---

I will first explain what exactly it does. The `2>&1 >` is a part of a log writing progress. If you write the rsync directly in the terminal, you would see the download speed, / size / ETA. We still want to be able to do this, even though it is being run automatically. `2>&1 >` will write a log, to `/home/pi/SB_sync_logs/1.name.of.folder.log`, containing the same info, as if it was being run manually in the terminal. So we will be able to see, how long the individual download is. Since the `.log` is being kept writing to, just close the log, and open it again, and it will be updated. The > at the end, means that it will overwrite the .log file, when it is being run again. That way we wont get a super long log file. IF you want a super long log file, just add an extra `>`. So it would be  `2>&1 >>`. I strongly recommend, not doing this though.

This gives us an individual detailed log, for every rsync you make. We also want a log, just showing the overall progress, of which rsync it is doing right now right?

To do this, go ahead and open up your script again.

**1: Completing the script**

To open your script, type:

~~~
sudo nano $HOME/scripts/SB_sync
~~~

Right under `#!/bin/sh`, type: `mkdir -p /home/pi/SB_sync_logs`. This will make a directory, for all the small logs.

On the third line, type: `echo "Syncing my rsync" > /home/pi/SB_sync.log`. This will be the text showing up, in the `overall status` log.

Your script should now look like this:

~~~
#!/bin/sh
mkdir -p /home/pi/SB_sync_logs
echo "Syncing my rsync" > /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"path/to/remote/dir/"' "/path/to/store/on/pi" 2>&1 > /home/pi/SB_sync_logs/1.name.of.folder.log
~~~

Repeat this progress, if you want another rsync in this script.

My whole script looks like this:

~~~
#!/bin/sh
mkdir -p /home/pi/SB_sync_logs
echo "Syncing iRL HD" > /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/iRL HD/"' "/media/HDD01/shares/SB/iRL HD" 2>&1 > /home/pi/SB_sync_logs/1.iRL.HD.log
echo "Syncing SUBLiME HD" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/SUBLiME HD/"' "/media/HDD01/shares/SB/SUBLiME HD" 2>&1 > /home/pi/SB_sync_logs/2.SUBLiME.HD.log
echo "Syncing Mikkel" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/Mikkel/"' "/media/HDD01/shares/SB/Mikkel" 2>&1 > /home/pi/SB_sync_logs/3.Mikkel.log
echo "Syncing Far" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/Far/"' "/media/HDD01/shares/SB/Far" 2>&1 > /home/pi/SB_sync_logs/4.Far.log
echo "Syncing Fannie" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/Fannie/"' "/media/HDD01/shares/SB/Fannie" 2>&1 > /home/pi/SB_sync_logs/5.Fannie.log
echo "Syncing Agents Of S.H.I.E.L.D" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/TV - Agents Of S.H.I.E.L.D/"' "/media/HDD01/shares/SB/TV - Agents Of S.H.I.E.L.D" 2>&1 > /home/pi/SB_sync_logs/6.Agents.Of.S.H.I.E.L.D.log
echo "Syncing Arrow" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/TV - Arrow/"' "/media/HDD01/shares/SB/TV - Arrow" 2>&1 > /home/pi/SB_sync_logs/7.Arrow.log
echo "Syncing Dexter" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/TV - Dexter/"' "/media/HDD01/shares/SB/TV - Dexter" 2>&1 > /home/pi/SB_sync_logs/8.Dexter.log
echo "Syncing The Walking Dead" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/TV - The Walking Dead/"' "/media/HDD01/shares/SB/TV - The Walking Dead" 2>&1 > /home/pi/SB_sync_logs/9.The.Walking.Dead.log
echo "Syncing Revolution" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/TV - Revolution/"' "/media/HDD01/shares/SB/TV - Revolution" 2>&1 > /home/pi/SB_sync_logs/10.Revolution.log
echo "Syncing The Big Bang Theory" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/TV - The Big Bang Theory/"' "/media/HDD01/shares/SB/TV - The Big Bang Theory" 2>&1 > /home/pi/SB_sync_logs/11.Big.Bang.Theory.log
echo "Syncing What.cd" >> /home/pi/SB_sync.log
/usr/bin/rsync -avhPS --chmod=a+rwx --delete user@server.feralhosting.com:'"private/rtorrent/data/What.cd/"' "/media/HDD01/shares/SB/What.cd" 2>&1 > /home/pi/SB_sync_logs/12.What.cd.log
echo "Syncing Complete" >> /home/pi/SB_sync.log
~~~

Please notice, that ONLY the first `echo "Syncing my folder" > /home/pi/SB_sync.log`, have ONE >. All the others should have two `>>`. As you can see in my script above. Also notice, that the numbers in the rsync command itself, goes higher and higher, depending on how many rsyncs you have.

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

Step 6: Check the script
---

Okay, so now we want to see if the script actually works. The first time it is used, you will have to accept feralhosting’s fingerprint. Else cron won’t be able to run it. The smart thing with our cron logs, is that it does not only show progress, it also shows errors. This can come in very handy.

So to accept feralhosting’s fingerprint, we will have to run the script manually at least one time.

Type:

~~~
$HOME/scripts/SB_sync
~~~

Then accept feralhosting’s fingerprint. When the sync then starts, just cancel it again. Hold `CTRL` and then press `c` to do that. 

Step 7: flock
---

As said earlier, we only want this script run, if it aint already running. To do that, we need to modify our cron job, in the cron tab. 

**1: Making the cron entry**

Type:

~~~
sudo crontab –e
~~~

Go to the bottom of the document, (one empty line between the above text, to our entry) and type:

~~~
 */5 * * * * /usr/bin/flock -xn /tmp/flocktmp.lock -c "/home/pi/scripts/SB_sync"
~~~

This will run the script, every five min.
Then `ctrl+x` then `y`, to save and exit. 
And that is basically it. Thank you for following this FAQ. 
Credit to konichiwa, and ozymandias, for helping out with the technical stuff.

-by Zeroz

Helpful pictures
---

**How the overall log file looks**

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Raspberry%20Pi%20-%20Sync%20with%20rysnc/1.1.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Raspberry%20Pi%20-%20Sync%20with%20rysnc/2.2.png)

The file will grow longer, the longer the script goes, and eventually say `Syncing Complete`

**How the detailed log files look**

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Raspberry%20Pi%20-%20Sync%20with%20rysnc/3.3.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Raspberry%20Pi%20-%20Sync%20with%20rysnc/4.4.png)

Troubleshooting
---

**Are you having problems with permissions?**

This command, will give it `777` rights (Open to EVERYONE)

~~~
sudo chmod –R 777 *
~~~

**Still having problems with permissions?**

Type this:

~~~
sudo chown pi:pi –R *
~~~

**The log showing up weird using SSH?**

You can also use nano in terminal. The catch is, that nano will just show one long gigantic line. You can go to the end of that line, by pressing `ctrl` plus `e` and to the start of the line, by pressing `ctrl` plus `a`. But if you want to have a MUCH better overview, you're want to use tightvnc.

That’s because you need the GUI, to view the log properly. Follow this guide, to install `tightvnc`, so you can view your raspberry pi’s desktop remotely - [installing tightvnc on the raspberry pi](http://programmaticponderings.wordpress.com/2012/12/26/installing-tightvnc-on-the-raspberry-pi/) 

**Another way of monitoring if the pi is downloading.**

We can see the general internet from the pi, using `bwm-ng`.

To get this, type:

~~~
sudo apt-get install bwm-ng
~~~

When you now type `bwm-ng` in pi’s terminal, you can see the general speed the whole pi is using. But do you really want to type that long sentence each time to check the speed? NO

We want to create an alias. So we only need to type `speed`, to see the speed.

Type this in the terminal:

~~~
sudo nano ~/.bash_aliases
~~~

Now type this in:

~~~
alias speed='bwm-ng'
~~~

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

For the alias to take effect, reboot the pi using:

~~~
sudo reboot
~~~

**You wonder if you can see the temperature of the pi, still using a alias?**

Ofc. This also comes in handy when you overclock, to monitor your pi won’t get hotter than 70deg.
In terminal type:

~~~
nano ~/.bash_aliases
~~~

Now add this to the document:

~~~
 alias temp='/opt/vc/bin/vcgencmd measure_temp'
~~~

As you proberly can see, you would have to type: `/opt/vc/bin/vcgencmd measure_temp`, to see the temp, but now you only need to write `temp`.

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

For the alias to take effect, reboot the pi using:

~~~
sudo reboot
~~~



