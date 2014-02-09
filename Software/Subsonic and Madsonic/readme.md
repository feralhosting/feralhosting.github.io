
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Important notes:
---

- Default mp3 bitrate is set in `Settings/Players/Max bitrate` per selected player
- Subsonic will ask for a license key after 30 days, that you can get by donating to the creator of the program. After 30 days, video streaming and mobile application support are deactivated. You can use the bash script to install Madsonic instead, that has no such restrictions but you have to pay for the Madsonic mobile app.
- HTML5 - [Minisub Chrome App](https://chrome.google.com/webstore/detail/minisub/jccdpflnecheidefpofmlblgebobbloc) (if you use https you must visit the subsonic server URL and accept the cert first
- Works with the IOS and Android apps. Madsonic may behave differently with some apps that were designed to support Subsonic.

[Subsonic Device options](http://www.subsonic.org/pages/apps.jsp)

[Madsonic Android Play Store](https://play.google.com/store/apps/details?id=github.madmarty.madsonic)

[Madsonic Android Amazon Store](http://www.amazon.com/Madsonic-Media-Streamer/dp/B00COJ4G1O)

Subsonic or Madsonic automatic installation using a bash script:
---

**install.subsonic.sh/install.madsonic.sh bash script features:**

- Installs Java 1.7 (kept up to date with current updates)
- Installs Subsonic or Madsonic servers. Can be installed side by side since they use separate locations and URLs
- Detects previous installations giving the option to remove, update or quit.
- Fully configures the start-up script. Unique to each user.
- Option to enter a path to a media folder during installation.
- Creates a custom script to `restart/start/kill` subsonic/madsonic (RSK) when the script is executed.
- Will `proxypass` automatically on Nginx or Apache so the URL will be in the valid SSL format `https://server.feralhosting.com/username/subsonic` or `https://server.feralhosting.com/username/madsonic`. 
- Lets you easily move between Apache or nginx. You can simply run current the script to apply the proxypass to an existing installation if you update to nginx.

**For Subsonic:**

~~~
wget -qO ~/install.subsonic.sh http://git.io/GBjb3w && bash ~/install.subsonic.sh
~~~

**For Madsonic:**

~~~
wget -qO ~/install.madsonic.sh http://git.io/Eq97bg && bash ~/install.madsonic.sh
~~~

Then follow the progress in your terminal. Some steps require user input. You will be asked whether you want to install Subsonic or Madsonic.

Once this script has been executed once, the `install.subsonic.sh`/`install.madsonic.sh` is copied to the `~/bin` directory as `install.madsonic` and the `subsonicrsk`/`madsonicrsk` is created in the `~/bin`

Now you can simply type this from anywhere in SSH to execute the installer script: 

~~~
install.subsonic
install.madsonic
~~~

Subsonic removal
---

Run the script again to kill all be given the option to remove Subsonic or Madsonic. It will kill all Java processes and removes the folders and files the script created. Then you can simply run the script again to reinstall.

subsonicrsk / madsonicrsk
---

Execute the `restart/start/kill` script like this (requires you ran the relevant installer script at least once):

~~~
subsonicrsk
madsonicrsk
~~~

The `restart/start/kill` (rsk) script does these things:

- Displays the URL used to access Subsonic when installed.
- Displays the last generated PID for the process when was installed using the `install.subsonic.sh` or started using the `subsonicrsk`
- Lists all Java processes
- Offers to Kill the PID that was generated the last time subsonic was installed using the `install.subsonic.sh` or started using the `subsonicrsk`
- Offers to Kill ALL java processes currently running.
- Start the `install.subsonic.sh` or manually installed version.

To update these scripts you must run the `install.subsonic.sh` script again.

Crontab and Subsonic.
---

This script creates a special mini bash script for restarting the Subsonic process located at `~/bin/subsonicron`. This bash script will check to if the `PID` created by Subsonic or Madsonic the last time it was run is currently alive. If it is alive, the script does nothing, to prevent duplicate processes being run. If the process is not alive the script will restart Subsonic or Madsonic. So if you add it to your crontab using the command below you can make sure the process is always available.

Use these commands to edit your crontab:

This crontab command will check to restart at reboot:

Run at reboot:

Subsonic:

~~~
@reboot bash -l ~/bin/subsonicron
~~~

Madsonic:

~~~
@reboot bash -l ~/bin/madsonicron
~~~

Check every minute. You can customise the timing before you use the command:

Subsonic:

~~~
* * * * * bash -l ~/bin/subsonicron
~~~

Madsonic:

~~~
* * * * * bash -l ~/bin/madsonicron
~~~

Notes:
---

Avconv: A static build found here can also be used.

[http://johnvansickle.com/libav/](http://johnvansickle.com/libav/)

[libav.09.02.2014.zip](https://bitbucket.org/feralhosting/feralfiles/downloads/libav.09.02.2014.zip)

Use these commands to download and extract a static build 06.14.2013 ready for use:

~~~
wget -qO ~/avconv.zip https://bitbucket.org/feralhosting/feralfiles/downloads/libav.09.02.2014.zip
mkdir -p ~/private/subsonic/transcode
unzip -qo ~/avconv.zip -d ~/private/subsonic/transcode
chmod 700 ~/private/subsonic/transcode/{avconv,avconv-10bit,avprobe,qt-faststart}
rm -f ~/avconv.zip
~~~

The you need to add a new `Settings/Transcoding/Add transcoding` in Subsonic or Madsonic:

~~~
Name: avconv mp3
Convert From: ogg oga aac m4a flac wav wma aif aiff ape mpc shn
Convert To: mp3
Step 1: avconv -i %s -b %bk -q 0 -loglevel error -f mp3 -
Step 2: is blank since its not needed
~~~

credits: [subsonic forum](http://forum.subsonic.org/forum/viewtopic.php?f=2&t=10655)



