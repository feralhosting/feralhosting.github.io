### Automated LFTP Sync from SeedBox to Home

This tutorial will explain how to use an automated LFTP script that runs every few minutes (or of your choosing) matching a remote directory with your home.  This script only works one way, so if you remove the file on your server, it will not be removed from your home directory.  It will also work with Windows, Mac, and Linux.

I prefer LFTP because, not only is it a fully automated daemon, it also maximizes my home pipeline. LFTP supports parallel downloads of the same file while also downloading others as well. Only one instance of this script will run, if it is currently transferring, it creates a lock and will not run again until the current operation has completed.

**Prerequisites - Install LFTP @ Home**

### MacOS

[Install Homebrew](https://www.feralhosting.com/faq/view?question=262)

After the above is installed execute the following within terminal to install LFTP

~~~
brew update
brew install lftp
~~~

### Windows

[Install Cygwin](https://www.feralhosting.com/faq/view?question=235)

**Make sure to select the following addons during the installation**

~~~
LFTP
bash
cygrunsrv
cron
~~~

Create a file called `synctorrents.sh`, replace all < > with your values.  The only code you need to modify is within the top 6 lines.

**Important note:** bash takes EOL (End of line) quite seriously. You will need to use UNIX/LF style end of lines for bash scripts. See this FAQ for info [Text editing - Over FTP or SFTP](https://www.feralhosting.com/faq/view?question=219)

In the script these are the variables you will need to customise to meet your requirements.

~~~
#!/bin/bash
login="username"
pass="password"
host="server.feralhosting.com"
remote_dir="/folder/you/want/to/copy"
local_dir="/cygdrive/s/lftp/somefolder/where/you.want/your/files/"
~~~

Here is the basic script:

~~~
#!/bin/bash
login="username"
pass="password"
host="server.feralhosting.com"
remote_dir="/folder/you/want/to/copy"
local_dir="/cygdrive/s/lftp/somefolder/where/you.want/your/files/"
 
trap "rm -f /tmp/synctorrent.lock" SIGINT SIGTERM
if [ -e /tmp/synctorrent.lock ]
then
  echo "Synctorrent is running already."
  exit 1
else
  touch /tmp/synctorrent.lock
  lftp -u $login,$pass $host << EOF
  set ftp:ssl-allow no
  set mirror:use-pget-n 5
  mirror -c -P5 --log=synctorrents.log $remote_dir $local_dir
  quit
EOF
  rm -f /tmp/synctorrent.lock
  trap - SIGINT SIGTERM
  exit 0
fi
~~~

Here is an edited version for use with sftp:

~~~
#!/bin/sh
login="username"
pass="password"
host="server.feralhosting.com"
remote_dir="/folder/you/want/to/copy"
local_dir="/cygdrive/s/lftp/somefolder/where/you.want/your/files/"

trap "rm -f /tmp/synctorrent.lock" SIGINT SIGTERM
if [ -e /tmp/synctorrent.lock ]
then
echo "Synctorrent is running already."
exit 1
else
touch /tmp/synctorrent.lock
lftp -p 22 -u $login,$pass sftp://$host << EOF
set mirror:use-pget-n 5
mirror -c -P5 --log=synctorrents.log $remote_dir $local_dir
quit
EOF
rm -f /tmp/synctorrent.lock
trap - SIGINT SIGTERM
exit 0
fi
~~~

Make the script executable:

~~~
chmod 700 synctorrents.sh
~~~

The important parameters for `lftp` are:

~~~
set mirror:use-pget-n 5
~~~

This makes lftp try to split up files in 5 pieces for parallel downloading. Likewise,

~~~
-P5
~~~

 
Means it will download at most 5 files in parallel (for a total 25 connections). Those 2 combined work wonders. In my case, I always end up downloading the files at the limit of my connection, but feel free to play with them and find what works best for you.

~~~
-c
~~~

Just tells it to try and resume an interrupted download if it' s the case.

**Creating a crontab.** 

WINDOWS USERS: Instead of crontab you may find it easier 
to use the Task Scheduler to run the command at the interval of your choosing.

[Here is a link to a simple guide on using task scheduler](http://www.makeuseof.com/tag/how-to-automate-windows-programs-on-a-schedule/)

### Using Cygwin:

~~~
C:\cygwin\bin\sh.exe -l /home/user/synctorrents.sh >> /your/home/directory/sync_cron.log 2>&1
~~~

The following instructions create a file called crontab and point it to the script you previously made called synctorrents.sh.  This is what automates the process every few minutes.

~~~
touch crontab
~~~

~~~
nano crontab
~~~

~~~
*/5 * * * * /home/user/synctorrents.sh >> /your/home/directory/sync_cron.log 2>&1
~~~

syncs every 5 min, change this to your choosing

Save and exit:

~~~
crontab /crontab
~~~

points crontab to the file you just made and edited

~~~
crontab -l
~~~

lists crontab, confirm to make sure it is linked correctly

I must give credit to [LordHades](http://www.torrent-invites.com/seedbox-tutorials/132965-tutorial-auto-sync-seedbox-home-linux-mac-machine-lftp-shell-script.html) who created this amazing script.



