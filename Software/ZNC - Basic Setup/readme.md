
Current latest stable version of ZNC is: `1.4`

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot.

Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

ZNC installation
---

Use this command to create the `~/bin` directory and reload your shell for this change to take effect.

~~~
mkdir -p ~/bin && bash
~~~

Install the `znc` using these commands:

~~~
wget -qO ~/znc.tar.gz http://znc.in/releases/znc-latest.tar.gz
tar xf ~/znc.tar.gz && cd ~/znc-1.4
./configure --prefix=$HOME && make && make install
cd && rm -rf znc{-1.4,.tar.gz}
~~~

Once it is installed and ready we can start to configure `znc` using this command:

~~~
znc --makeconf
~~~

If you get a `command not found` error:

**Option 1 (recommended):** Start a new SSH session so that `PATH` is correctly set upon login then try again in this new session.

**Option 2:** Alternatively you can use this command to call the binary directly:

~~~
~/bin/znc --makeconf
~~~

ZNC Starting or Restarting:
---

### Start znc

To start `znc` you will need to SSH into your slot and use this command:

~~~
znc
~~~

The binary is located in the `~/bin` directory so it should be in the `PATH`. If you need to call it directly use this command:

~~~
~/bin/znc
~~~

### Restart or Shutdown znc

To properly restart or stop `znc` you connect to your server using and Admin user and execute one of these commands:

> **Important note:** When configuring `znc` for the first time you should have created this user with administrator privileges:

~~~
/znc restart
/znc shutdown
~~~

See here for more commands: [http://wiki.znc.in/Using_commands](http://wiki.znc.in/Using_commands)

Crontab
---

To make sure `znc` is restarted after a reboot use cronjob.

~~~
@reboot ~/bin/znc
~~~

Notifications:
---

Install this module to configure notifications via various platforms.

> **Important note:** In order to use the `libcurl` transport layer you would need to ask for this dependency to be installed via a ticket if it is not present.

~~~
libcurl4-openssl-dev
~~~

The you would use `make curl=yes` instead of `znc-buildmod push.cpp`

~~~
git clone https://github.com/jreese/znc-push.git
cd ~/znc-push
znc-buildmod push.cpp
make install
~~~

with curl (recommended):

~~~
git clone https://github.com/jreese/znc-push.git
cd ~/znc-push
make curl=yes
make install
~~~

Then in you connected network use these commands:

First load the module:

~~~
/msg *status loadmod push
~~~

Then configure it using this command template:

~~~
/msg *push set option value
~~~

So for example:

~~~
/msg *push set service pushbullet
~~~

Then You would set your credentials:

Username:

~~~
/msg *push set username my_pushover_user_key
~~~

Secret:

~~~
/msg *push set secret my_pushover_api_for_this_appliction
~~~

Please see here for more options and services:

[https://github.com/jreese/znc-push](https://github.com/jreese/znc-push)

If you see this error from znc you can ignore it.

~~~
*push> Error: service type not selected
~~~



