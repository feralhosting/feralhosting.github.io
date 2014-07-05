
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Use this command to create the `~/bin` directory and reload your shell for this change to take effect.

~~~
mkdir -p ~/bin && bash
~~~

Installation Step 1: Install Protobuf (required dependency)
---

This is a required dependency that is not included with your slot.

~~~
wget -qO ~/protobuf-2.5.0.tar.gz http://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz
tar xf ~/protobuf-2.5.0.tar.gz && cd ~/protobuf-2.5.0
./configure --prefix=$HOME && make && make install
cd && rm -rf  protobuf{-2.5.0.tar.gz,-2.5.0}
~~~

Installation Step 2: Install Mosh
---

Now download and install `mosh`:

~~~
wget -qO ~/mosh-1.2.4.tar.gz http://mosh.mit.edu/mosh-1.2.4.tar.gz
tar xf ~/mosh-1.2.4.tar.gz && cd ~/mosh-1.2.4
./configure --prefix=$HOME PKG_CONFIG_PATH=$HOME/lib/pkgconfig LDFLAGS="--static" && make && make install
cd && rm -rf  mosh{-1.2.4.tar.gz,-1.2.4}
~~~

Connect to your slot using this command.

For *older* versions of `mosh` only:

~~~
mosh username@server.feralhosting.com --server="LANG=$LANG ~/bin/mosh-server"
~~~

For `mosh` versions 1.2.4 + you only need this command:

~~~
mosh username@server.feralhosting.com --server=~/bin/mosh-server
~~~

Notes
---

About this error:

~~~
/usr/bin/mosh: Did not find mosh server startup message.
~~~

If you are getting this is it because you did not use `--server=~/bin/mosh-server'` in your connect command.

It is possible to add this location to the `PATH` to simplify the connection but is must be done in a specific way. So we (and the developer) instead recommend you use an alias for connecting, for example:

~~~
alias moshcnct='mosh username@server.feralhosting.com --server=~/bin/mosh-server'
~~~

If you must add it to your `PATH` you will need to:

1: Add it to your `~/.bashrc` and only this file.

2: The `PATH` must be at the top of the file, before any `if` statements.

This is what you will need to add:

~~~
PATH=$HOME/bin:$PATH
~~~

Or you can use this command. It will check for the line and if it does not already exist then insert it at line 1. This will fix your issue.

~~~
[ ! "$(grep 'PATH=$HOME/bin:$PATH' ~/.bashrc)" ] && sed -i '1iPATH=$HOME/bin:$PATH' ~/.bashrc
~~~

MOSH on your OS:
---

iOS - [iSSH](https://itunes.apple.com/us/app/issh-ssh-vnc-console/id287765826)

Android - [JuiceSSH](https://play.google.com/store/apps/details?id=com.sonelli.juicessh&hl=en_GB)

Windows Cygwin x86 or x64 - [Cygwin - Linux tools on Windows](https://www.feralhosting.com/faq/view?question=235)

OS X 10.6 or later - [https://mosh.mit.edu/mosh-1.2.4-3.pkg](https://mosh.mit.edu/mosh-1.2.4-3.pkg)



