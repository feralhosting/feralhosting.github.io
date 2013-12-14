
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Important notes:
---

- Default mp3 bitrate is set in `Settings/Players/Max bitrate` per selected player
- The bash script makes installation and management of Subsonic and Madsonic very easy. Consider using it over the manual steps.
- Use the version used of ffmpeg linked in this guide as the newer or older versions may play well with Subsonic. 
- Subsonic will ask for a license key after 30 days, that you can get by donating to the creator of the program. After 30 days, video streaming and mobile application support are deactivated. You can use the bash script to install Madsonic instead, that has no such restrictions.
- HTML5 - [Minisub Chrome App](https://chrome.google.com/webstore/detail/minisub/jccdpflnecheidefpofmlblgebobbloc) (if you use https you must visit the subsonic server URL and accept the cert first
- Works with the IOS and Android apps. Madsonic may behave differently with some apps that were designed to support Subsonic. Madsonic has its own Android app.

Subsonic or Madsonic automatic installation using a bash script:
---

**install.subsonic.sh/install.madsonic.sh bash script features:**

- Installs Java 1.7
- Installs Subsonic or Madsonic servers. Can be installed side by side since they use separate locations.
- Detects previous installations giving the option to remove, update or quit.
- Fully configures the start-up script. Unique to each user.
- Option to enter a path to a media folder during installation.
- Creates a custom script to `restart/start/kill` subsonic/madsonic (RSK) when the script is executed.
- Will `proxypass` automatically if nginx is detected so the URL will be in the valid SSL format `https://server.feralhosting.com/username/subsonic` or `https://server.feralhosting.com/username/madsonic`

For Subsonic:

~~~
wget -qO ~/install.subsonic.sh http://git.io/GBjb3w && bash ~/install.subsonic.sh
~~~

For Madsonic:

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

- Displays the URLs and ports used to access subsonic when installed.
- Displays the last generated PID for the process when it ran using the subsonic.4.8.sh or the subsonicrsk.sh
- Lists all Java processes
- Offers to Kill the PID that was generated the last time subsonic was launched using the subsonic.4.8.sh or the subsonicrsk.sh
- Offers to Kill ALL java processes currently running.
- Start the subsonic.4.8.sh or manual 4.8 version installed.

To update these scripts you must run the **subsonic.4.8.sh** or **subsonic.4.8** again.

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

Subsonic Manual installation Steps Intro:
---

**Important Note:** Please use the bash script for Madsonic.

**Important Note:** Java is installed on your slot but the included version is very unstable with Subsonic. You will need to install Java 1.7:

How to install Java 1.7
---

If you would like to install a newer Java version you can use this guide:

[How to install java 1.7](https://www.feralhosting.com/faq/view?question=183)

Reinstalling or stopping the subsonic server
---

You can delete the contents of `~/private/subsonic` and re-install to reset the 30 days limit. Users will have to be re created as well as lost settings so doing this is not always easy.

**Important note:** Kill the Subsonic Java process before reinstalling otherwise attempting to reinstall subsonic and reusing the same port may prevent you from connecting to the port. To do this in SSH, type: 

The easiest way to stop the running subsonic process is to use this command:

~~~
killall -9 -u $(whoami) java
~~~

This will kill `ALL` Java processes. `There are no Feral Java processes` so this only matters if you are running another custom application.

If you only want to kill the specific subsonic Java process then you must do this:

~~~
ps x
~~~

In a terminal and look for the pid of a line similar to this. The PID of this line is 30801

~~~
30801   ?Sl     4:23 java -Xmx150m -Dsubsonic.home= -Dsubsonic.host= -Dsubsonic.port= -Dsubsonic.httpsPort= -Dsubsonic.contextPath=/ -Dsubsonic.defaultMusicFolder=
~~~

To kill this process type `kill -9 PID` with the `PID` in our examples being

~~~
kill -9 30801
~~~

If you still cannot connect to your usual port after a reinstall or a reboot of subsonic, try changing ports.

FFmpeg versions
---

All versions used in the scripts and FAQ are based on static builds created here: [http://forum.madsonic.org](http://forum.madsonic.org).

[Madsonic build ffmpeg.31.10.2013.zip](https://bitbucket.org/feralhosting/feralfiles/downloads/ffmpeg.31.10.2013.zip)

Alternate static builds:

[http://johnvansickle.com/ffmpeg/](http://johnvansickle.com/ffmpeg/)

[ffmpeg-2.0.1-64bit-static.zip](https://bitbucket.org/feralhosting/feralfiles/downloads/ffmpeg-2.0.1-64bit-static.zip)

Subsonic Manual installation Steps using SSH
---

We are using the files here because they work “out of the box” pretty much. 4.6 does not seem to work with default settings using either a slots included ffmpeg or a static build. With this FAQ all transcoding and stuff just works. No tweaking needed.

Open up a Terminal to your slot using putty or a terminal. your SFTP/SSH details will be on your [Slot Manager/server/](https://www.feralhosting.com/manager/) page. [Use this guide if you need to know how to SSH](https://www.feralhosting.com/faq/view?question=12)

Once you have successfully SSH'd into your slot carry on with the FAQ.

**Important note:** The guide will have the commands you need to type or paste. In PuTTy a right click is paste or use press and hold the `SHIFT` key the press `INS`

Creates some directories we need for configuring the start-up script

~~~
mkdir -p  ~/private/subsonic/{transcode,playlists,Podcasts}
~~~

Gets the latest version of subsonic from sourceforge.net, currently at: `4.8`

~~~
wget -qO ~/subsonic.tar.gz http://sourceforge.net/projects/subsonic/files/subsonic/4.8/subsonic-4.8-standalone.tar.gz
~~~

Extracts the archive we just downloaded

~~~
tar xf ~/subsonic.tar.gz -C ~/private/subsonic/
~~~

Downloads a long term hosted version of ffmpeg static. Dated at `06/14/2013`

~~~
wget -qO ~/ffmpeg.zip https://bitbucket.org/feralhosting/feralfiles/downloads/ffmpeg.31.10.2013.zip
~~~

Extracts the ffmpeg version we downloaded to the transcode directory

~~~
unzip -qo ~/ffmpeg.zip -d ~/private/subsonic/transcode/
~~~

Copies over the local version of lame to ~/private/subsonic/transcode/

~~~
cp -f /usr/local/bin/lame ~/private/subsonic/transcode/
~~~

Copies over the local version of flac to ~/private/subsonic/transcode/

~~~
cp -f /usr/bin/flac ~/private/subsonic/transcode/
~~~

Make the binaries executable:

~~~
chmod 700  ~/private/subsonic/transcode/{Audioffmpeg,ffmpeg,lame,flac}
~~~

Tidy up to files we downloaded:

~~~
rm -f ~/{subsonic.tar.gz,ffmpeg.zip}
~~~

Now you can edit the `subsonic.sh` with a text editor over ftp or do this

~~~
nano -w ~/private/subsonic/subsonic.sh
~~~

This is the main section we are interested in:

~~~
SUBSONIC_HOME=/var/subsonic
SUBSONIC_HOST=0.0.0.0
SUBSONIC_PORT=4040
SUBSONIC_HTTPS_PORT=0
SUBSONIC_CONTEXT_PATH=/
SUBSONIC_MAX_MEMORY=150
SUBSONIC_PIDFILE=
SUBSONIC_DEFAULT_MUSIC_FOLDER=/var/music
SUBSONIC_DEFAULT_PODCAST_FOLDER=/var/music/Podcast
SUBSONIC_DEFAULT_PLAYLIST_FOLDER=/var/playlists

quiet=0
~~~

Change the:

**1:** `SUBSONIC_HOME=/var/subsonic` to `SUBSONIC_HOME=~/private/subsonic`

**2:** `SUBSONIC_HOST=` leave this as it is `0.0.0.0` This default behaviour binds to all network interfaces.

**3:** The `SUBSONIC_PORT=` and `SUBSONIC_HTTPS_PORT=` ports, change them to anything over `10000` and under `50000`. Try avoid rounded numbers like `15000`

**4:** `SUBSONIC_MAX_MEMORY=` to `2048` like `SUBSONIC_MAX_MEMORY=2048`

**5** `SUBSONIC_PIDFILE=` Set the path for the `PID` file as: `~/private/subsonic/subsonic.sh.PID`

**6:** `SUBSONIC_DEFAULT_MUSIC_FOLDER` Is the path to you music folder (but this can be done in the gui)

**7:** Optional Step : `SUBSONIC_DEFAULT_PODCAST_FOLDER=` and `SUBSONIC_DEFAULT_PLAYLIST_FOLDER=`  Are the paths to the `Podcast` and `playlist` folders (only if you have changed them from the guides defaults, otherwise skip this step)

**8:** Add some language settings odd characters (3 lines with export L...)

It will now look something like this edited version below:

~~~
SUBSONIC_HOME=~/private/subsonic
SUBSONIC_HOST=0.0.0.0
SUBSONIC_PORT=45681
SUBSONIC_HTTPS_PORT=45682
SUBSONIC_CONTEXT_PATH=/
SUBSONIC_MAX_MEMORY=512
SUBSONIC_PIDFILE=~/private/subsonic/subsonic.sh.PID
SUBSONIC_DEFAULT_MUSIC_FOLDER=~/PATH/TO/music
SUBSONIC_DEFAULT_PODCAST_FOLDER=~/private/subsonic/Podcast
SUBSONIC_DEFAULT_PLAYLIST_FOLDER=~/private/subsonic/playlists

export LANGUAGE=en_GB.UTF-8
export LANG=en_GB.UTF-8
export LC_ALL=en_GB.UTF-8

quiet=0
~~~

The press and hold `CTRL` then press `x` to save. Press `y` to confirm.

You can start the subsonic service (from any location) using this command:

~~~
bash ~/private/subsonic/subsonic.sh
~~~

The output should look something like this:

~~~
Started Subsonic PID
~~~

To visit your subsonic Gui you visit your hostname URL with the port. Enjoy.

~~~
Hostname:Port
~~~

Notes:
---

Avconv: A static build found here can also be used.

[http://johnvansickle.com/libav/](http://johnvansickle.com/libav/)

[libav.31.10.2103.zip](https://bitbucket.org/feralhosting/feralfiles/downloads/libav.31.10.2103.zip)

Use these commands to download and extract a static build 06.14.2013 ready for use:

~~~
wget -qO ~/avconv.tar.gz https://bitbucket.org/feralhosting/feralfiles/downloads/libav.31.10.2103.zip
tar xf ~/avconv.tar.gz -C ~/private/subsonic/transcode/
rm -f ~/avconv.tar.gz
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



