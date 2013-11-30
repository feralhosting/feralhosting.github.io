
This FAQ is for downloading and installing [WeeChat](http://www.weechat.org/) on your slot.

WeeChat is a fast, light and extensible chat client. It runs on many platforms like Linux, Unix, BSD, GNU Hurd, Mac OS X and Windows (cygwin). 

### 1: Do some ground work

Put the files in a nice location:

~~~
mkdir -p ~/programs
~~~

Add the location to your `PATH` using this command.

~~~
[[][/[][ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

### 2 Pre-built: Download and extract pre build cmake-2.8.12-Linux-i386

**Recommended** fast and simple.

~~~
wget -qO ~/cmake.tar.gz http://www.cmake.org/files/v2.8/cmake-2.8.12-Linux-i386.tar.gz
tar xf ~/cmake.tar.gz
cp -rf ~/cmake-2.8.12-Linux-i386/. ~/programs
rm -rf ~/cmake-2.8.12-Linux-i386 ~/cmake.tar.gz
~~~

### 3: Build WeeChat and install it

Please use this script.

**Important note:** You need to have completed Steps 1 and 2 before running this script.

~~~
wget -qO ~/weechat.sh http://git.io/L6oalA && bash ~/weechat.sh
~~~

### 4: Start WeeChat

We have added the location to the `PATH` in step 1, so we can use this command:

~~~
screen -dmS weechat weechat-curses
~~~

Now attach to the screen:

~~~
screen -r weechat
~~~

The full path to execute WeeChat is:

~~~
~/programs/bin/./weechat-curses
~~~

### 5: Configure WeeChat

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
/set irc.server.What-Network.ssl_dhkey_size 512
/save
~~~

Add other networks as desired.

### 6: Connecting to predefined IRC networks

Use this command to connect to the Feral Hosting IRC channel,  `#feral` on the `What-Network`  IRC network that we defined in the previous step.

~~~
/connect What-Network
~~~

### 7: Join a channel

~~~
/j #feral
~~~

To detach from the screen, press and hold `CRTL` and `a` then press `d`.

### Further reading

Here you can get information on further configuration, such as auto join and more.

[WeeChat FAQ](http://www.weechat.org/files/doc/weechat_faq.en.html)

[WeeChat Quick Start Guide](http://www.weechat.org/files/doc/stable/weechat_quickstart.en.html)

[WeeChat Quick Start Guide](http://www.weechat.org/files/doc/stable/weechat_user.en.html)




