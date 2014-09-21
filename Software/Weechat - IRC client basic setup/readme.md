
This FAQ is for downloading and installing [WeeChat](http://www.weechat.org/) on your slot.

WeeChat is a fast, light and extensible chat client. It runs on many platforms like Linux, Unix, BSD, GNU Hurd, Mac OS X and Windows (cygwin). 

Please run this command in SSH first:

~~~
mkdir -p ~/bin && bash
~~~

### 1 Pre-built: Download and extract pre build cmake-2.8.12-Linux-i386

Please see this FAQ. Upon completion of the installation of `cmake` please return to this FAQ and continue.

[CMAKE - Basic Setup](https://www.feralhosting.com/faq/view?question=270)

### 2: Build WeeChat and install it

Please use this script.

**Important note 1:** You need to have completed Step 1 before running this script.

**Important note 2:** If you get an error about gcrypt you will need to open a ticket and ask for `libgcrypt11-dev` to be installed.

~~~
wget -qO ~/install.weechat.sh http://git.io/L6oalA && bash ~/install.weechat.sh
~~~

### 3: Start WeeChat

We have added the location to the `PATH` in step 1, so we can use this command:

~~~
screen -dmS weechat weechat
~~~

Now attach to the screen:

~~~
screen -r weechat
~~~

The full path to execute WeeChat is:

~~~
~/programs/bin/./weechat
~~~

### 4: Configure WeeChat

These are some required settings. You enter them in WeeChat after you have started it.

~~~
/server add What-Network irc.what-network.net/6697 -ssl
~~~

Replace  `"username,username_1,username_2"` and the two  instances of `"username"` with a username of your  choice.

~~~
/set irc.server.What-Network.nicks "username,username_1,username_2"
/set irc.server.What-Network.username "username"
/set irc.server.What-Network.realname "username"
~~~

Some final settings:

~~~
/set irc.server.What-Network.ssl on
/set irc.server.What-Network.ssl_verify off
/set irc.server.What-Network.ssl_dhkey_size 1024
/save
~~~

Add other networks as desired.

### 5: Connecting to predefined IRC networks

Use this command to connect to the Feral Hosting IRC channel,  `#feral` on the `What-Network`  IRC network that we defined in the previous step.

~~~
/connect What-Network
~~~

### 6: Join a channel

~~~
/j #feral
~~~

To detach from the screen, press and hold `CRTL` and `a` then press `d`.

### Further reading

Here you can get information on further configuration, such as auto join and more.

[WeeChat FAQ](http://www.weechat.org/files/doc/weechat_faq.en.html)

[WeeChat Quick Start Guide](http://www.weechat.org/files/doc/stable/weechat_quickstart.en.html)

[WeeChat Quick Start Guide](http://www.weechat.org/files/doc/stable/weechat_user.en.html)




