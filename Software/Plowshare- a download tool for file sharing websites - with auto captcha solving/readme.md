
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Plowshare
---

Plowshare homepage: [http://code.google.com/p/plowshare/](http://code.google.com/p/plowshare/)
Plowshare Readme: [http://code.google.com/p/plowshare/wiki/Readme4](http://code.google.com/p/plowshare/wiki/Readme4)

Plowshare is a UNIX/Linux command line tool for downloading files from file sharing websites like rapidshare.com, hotfile.com, depositfiles.com, and so on, it currently has support for 49 sites.

The real benefit for users is Plowshare's ability to take a file of links and download them all, with automatic captcha solving, and you can start it running and then logout of your Feral slot leaving it to do all the hard work (maybe even leaving it running overnight to download lots).

The automatic captcha solving is done by using one of several sites which allow you to either buy captchas or to earn them by solving other people's captchas and so build up captcha credits for your own future use. In this guide I will explain how to setup Plowshare to use 9kw.eu which is the site that allows you to earn captchas by solving them as and when you want to earn credits. When Plowshare needs to solve a captcha it will send a request to 9kw.eu and as long as you have credits available the captcha will be solved. As well as 9kw.eu you can also use deathbycaptcha.com and antigate.com which both sell captcha solving cheaply, but only 9kw.eu has the facility to earn credits by solving other people's captchas. Note: Cost, 9kw.eu sells 4000 captchas for EURO €5.00, deathbycaptcha.com sells 5000 captchas for USD $6.95, antigate.com is in the same ballpark.

Plowshare is a command line tool and while not hard to install, setup, and run, it is not for Linux newbies. You really need to know how to edit files on your Feral slot, create and change directories, and such like. This is a step-by-step guide for installing and using Plowshare on your Feral slot and not a how-to-do the basics of Linux.

### Step 1 - Get the Plowshare source file on to your Feral slot.

Download the latest "Plowshare source tarball" (the file which ends in ".tar.gz") from this page:
 
[http://code.google.com/p/plowshare/downloads/list](http://code.google.com/p/plowshare/downloads/list)

The current version as of November 21, 2013 is `plowshare4-snapshot-git20131102.b72c58d.tar.gz `  but that will change in time. You want the "plowshare4-snapshot..." and NOT the "plowshare3-snapshot...".
 
Create a temp 'install' directory on your Feral slot, let's say 'plowtemp', and put the "plowshare-snapshot-version-num.tar.gz" file into that directory.
 
More advanced Linux users can use wget to download the file directly to their Feral slot. e.g.

Note: For the correct link to use with wget click on the ".tar.gz" file on the Plowshare downloads page and then copy the download link on the page you are taken to.

~~~
wget http://plowshare.googlecode.com/files/plowshare4-snapshot-git20130520.2b2d736.tar.gz
~~~

### Step 2 - Untar the Plowshare source.

Make sure you are in the temp install directory you created, e.g. 'plowtemp'.

Untar the source tarball with this command:

~~~
tar -zxvf plowshare-snapshot-*.tar.gz
~~~

The tar command above will create a new directory with the same name as the plowshare-snapshot-version-num.tar.gz but without the ".tar.gz" extension. This directory will contain all the files needed for the installation.

### Step 3 - Install Plowshare.

Change to the directory that was created by tar in Step 2, e.g. 'plowshare-snapshot-version-num'.

If you type the command "ls -l" you should see a file listing of something like this:

~~~
-rw------- 1 YourUserName YourUserName  2342 Jun  9 11:38 AUTHORS
-rw------- 1 YourUserName YourUserName  9203 Jun  9 11:38 CHANGELOG
drwx------ 2 YourUserName YourUserName  4096 Jun  9 11:38 contrib
-rw------- 1 YourUserName YourUserName 35147 Jun  9 11:38 COPYING
drwx------ 2 YourUserName YourUserName  4096 Jun  9 11:38 docs
drwx------ 2 YourUserName YourUserName  4096 Jun  9 11:38 etc
-rw------- 1 YourUserName YourUserName  1338 Jun  9 11:38 INSTALL
-rw------- 1 YourUserName YourUserName  3702 Jun  9 11:38 Makefile
-rw------- 1 YourUserName YourUserName  6805 Jun  9 11:38 README
-rwx------ 1 YourUserName YourUserName  3746 Jun  9 11:38 setup.sh
drwx------ 4 YourUserName YourUserName  4096 Jun  9 11:38 src
drwx------ 2 YourUserName YourUserName  4096 Jun  9 11:38 tests
~~~

To install Plowshare as non-root (you do not have root / sudo privileges on your Feral slot), run the "make install" command below:

**Important note:** It is important that you use exactly this command and not the one specified in the INSTALL file which does not work (I know I tried it and it does not put the executable links in the 'bin' directory - see below).

~~~
make install PREFIX=$HOME
~~~

**Important note:** When you run the command above you might notice the error below - Do Not Worry! The install process is just trying to check that you are installing the newest version of Plowshare and using 'git' to check. Feral slots do not have 'git' installed so this process will not work, but the install will continue to work perfectly well.

~~~
/bin/sh: git: command not found
~~~

The "make install" command will install the Plowshare script into a directory called 'share' in your home directory. It will also create another directory in your home directory called 'bin' (if that does not already exist) into which it will place symbolic links to the various executable scripts that make up Plowshare. Do not move or change the names of these directories or anything inside them or Plowshare won't work.
 
You can now check to see if Plowshare is installed, just run the following command:

~~~
plowdown -h
~~~

You should see a page of usage and options. If instead you get "command not found", it will be because the 'bin' directory has not been added to your $PATH. Just log out of Feral and then log back in again and it should work. (Feral slots have a '.bashrc' file which automatically adds the '~/bin' directory to your path if 'bin' exists and '.bashrc' is run when you login.)

At this point you can delete the temp install directory you created, i.e. 'plowtemp', as well as the source tarball (.tar.gz) file if you want, they won't be needed again.

### Step 4 - Fix Potential IPv6 (Internet Protocol v6) Problem.

There is no support on Feral slots for IPv6 (Internet Protocol version 6) at the moment. Plowshare makes extensive use of a program called 'curl' to access the web and you must create a 'curl' init file to make sure 'curl' always uses IPv4 IP addresses and not IPv6.
 
Create a file in your home directory called '.curlrc' and in it place just the short line below:

~~~
--ipv4
~~~

You can achieve this by running the following command:

~~~
echo '--ipv4' >> ~/.curlrc
~~~

 
### Step 5 - Create an automated captcha Account.

You can use 9kw.eu, deathbycaptcha.com or antigate.com to buy captcha credits, but only 9kw.eu allows you to earn credits by solving other people's captchas - this works by you going to the 9kw.eu 'Captcha' page, it will give you a captcha to solve, when you do so it will give you some credits, then it will give you another captcha to solve and so on.

Note: An alternative to automated captcha solving is manual captcha solving. Just use the "--captchamethod=imgur" option on the command line or "captchamethod=imgur" in your config file. Plowshare will provide you with an imgurlink hosting the captcha, and you will need to solve it yourself which means you will have to keep and eye on the window if downloading more than one file at a time.

### Step 6 - Create a Plowshare Config File.

**Important note:** You do not need to create a config file, everything can be done on the command line, but it is useful to use one.
 
Plowshare uses this file location for its config file: `~/.config/plowshare/plowshare.conf`
 
Go to your home folder and make the directories and file, e.g. like this:

~~~
cd $HOME
mkdir .config
(Note: '.config' may already exist, it will do if you have Deluge installed on your slot.)
cd .config
mkdir plowshare
cd plowshare
touch plowshare.conf
~~~

Now you must edit the 'plowshare.conf' file. Mine looks like this:

~~~
# Plowshare configuration file
#

[General]
# I have a rapidshare Premium account, so have entered my login details:
rapidshare/a=UserName:UserPass

# Plowshare readme (linked at the top of this page) shows how to enter login details for other sites, e.g.
# mediafire/a="UserName:Pass With Spaces Use Quotes"
# freakshare/b=UserName:UserPass
# Note: The "/a" denotes a premium account, the "/b" denotes a registered but free account.

[Plowdown]
# Timeout in seconds: 43200 = 12 hours ` 60 mins ` 60 secs
timeout=43200

# Num retries you want per file.
max-retries=20

# I created a dir to put the download the files in. If you leave this out the PWD will be used, that is whichever
# dir you start the program from. Make sure you use the FULL PATH and not the '~/' home notation.
output-directory=/media/sdh1/home/username/downloads/

# Use online automated captcha solving.
captchamethod=online

# The key for 9kw.eu
9kweu=FITSEKDFVIXXXXXXXXX

# If using deathbycaptcha.com use this instead of "9kweu":
# deathbycaptcha=UserName:UserPass

# If using antigate.com use your key:
# antigate=49b1b8740e4b51cf51838975de9e1c31

# Note: Only use one of: "9kweu=", "deathbycaptcha=", "antigate=" so if you set up
# multiple accounts then make sure only the one you want to use is in the config.
~~~

I have a rapidshare.com account, so my login details go in the `General` section. The other sites can have login details entered as well, see the notes in the example config file above and the readme linked below. If you don't have any account just delete the `General` section.

The `Plowdown` section can have all kinds of things set in them, I just have a few. If you are using 9kw.eu enter your key details in the way of my example, likewise antigate, if deathbycaptcha then enter your username and pass seperated by a ':' and if there are spaces in your user/pass then add double quotes, e.g. deathbycaptcha="User Name:Pass Word".
 
Any option can be placed in the config file, please see the Plowshare Readme config file section, here:
[http://code.google.com/p/plowshare/wiki/Readme4#Configuration_file](http://code.google.com/p/plowshare/wiki/Readme4#Configuration_file)

### Step 7 - Using Plowshare.

Plowshare can be used to download, upload, list, and delete files on the file sharing websites.

See the Plowshare Readme usage examples section, here:

[http://code.google.com/p/plowshare/wiki/Readme4#Usage_examples](http://code.google.com/p/plowshare/wiki/Readme4#Usage_examples)

I would think you'll mainly be downloading files using 'plowdown', here are a few examples of its basic usage, but you can get a lot more information in the readme (already linked above) or by entering 'man plowdown' on the command line. If you want to use 'plowup' for uploading files, 'plowdel' for deleting them, or 'plowlist' for listing the contents of a shared-folder link then read their man pages and the webpage readme.

To download a single file it's as easy as this:

~~~
plowdown http://www.rapidshare.com/files/86545320/TestName.rar
plowdown http://depositfiles.com/files/zqwghtyz
~~~

If a captcha needs to be solved, and you set it up correctly, then that will be done automatically for you.

To download a file of links, just create a text file with each link on a single line, e.g.

~~~
# Links example file: links.txt
http://depositfiles.com/files/zqwghtyz
http://depositfiles.com/files/qwwgmsjs
http://depositfiles.com/files/shashsnd
http://depositfiles.com/files/whayetms
~~~

Then run plowdown with the file name:

~~~
plowdown links.txt
~~~

If you use the -m switch then each link will be 'commented out' in the 'links.txt' file as and when it has been successfully downloaded.

~~~
plowdown -m links.txt
~~~

You can also use plowdown to check - but not download - links, so you can check that all parts of a multi-part archive exist before starting the download process. Again using a single link or a file of links.

~~~
plowdown -c http://depositfiles.com/files/zqwghtyz
plowdown -c links.txt
~~~

**How to run plowdown even after you have logged off Feral:**

A useful hint for Feral users is that if you use the '&' control operator at the end of the command line, then the command will 'return' immediately and continue to run as a background task. This means you can start plowdown and then logoff Feral while plowdown continues to run. If you stay logged in you will continue to get messages from plowdown in your terminal window (unless you used the -q, --quiet switch) but logging out of Feral will not kill the process.
 
Just enter the command, add a '&' at the end of it, and afterwards logout of Feral as normal, e.g.

~~~
plowdown -m links.txt &
~~~

Note: A much better option than using the command followed by '&' so that plowdown will run after you have logged out is to use the Linux 'screen' command. You may have used screen with a torrent program on your Feral slot already. Just type 'screen' to get a new screen, start plowdown, then hit <CTRL>A+D to 'detach' the screen. You can then log out of your Feral slot, maybe leaving files to download overnight. Restore a screen by using 'screen -ls' to list active screens, then 'screen -r screen_id' to restore it. Once restored you can kill that screen using <CTRL>A+K to 'kill' the screen if plowdown has finished or of course you can detach the screen again with <CTRL>A+D. Screen is very powerful and has many features, see the manual linked below.

[Screen User's Manual](http://www.gnu.org/software/screen/manual/screen.html)

That is the end of this tutorial but there is lots more information on the Plowshare site.


