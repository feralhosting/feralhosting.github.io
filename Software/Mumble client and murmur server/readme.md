
**Important note:** This `x86` binary will not run on the Feral servers dues to security restrictions.

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

[Mumble](http://mumble.sourceforge.net/) is an open source, low-latency, high quality voice chat software primarily intended for use while gaming.

How to install and use the murmur Mumble server for use with Mumble clients.

The murmur server is the server for the mumble VoIP client.

~~~
wget -qO ~/server.tar.bz2 http://downloads.sourceforge.net/project/mumble/Mumble/1.2.8/murmur-static_x86-1.2.8.tar.bz2
tar xf server.tar.bz2 && cp -rf ~/murmur-static_x86-1.2.8/. ~/private/murmur && cd && rm -rf {murmur-static_x86-1.2.8,server.tar.bz2}
~~~

That is basically it for the download and extraction of the server. There are a couple of things we need to do before we start it.

Find and open this file.

~~~
~/private/murmur/murmur.ini
~~~

For example in SSH do this:

~~~
nano -w ~/private/murmur/murmur.ini
~~~

We must change the default port:

~~~
port=64738
~~~

to something else, any number between 6000 - 50000 is OK, for example:

~~~
port=23456
~~~

Optionally you can set a server password.

~~~
serverpassword=
~~~

Once this is done you can run the program using this command:

~~~
~/private/murmur/./murmur.x86 -ini ~/private/murmur/murmur.ini
~~~

Superuser password:
---

Please Look in this file `~/private/murmur/murmur.log` for your super user password.

The result should look something like:

~~~
<W>2014-05-19 08:56:47.423 1 => Password for 'SuperUser' set to '*i]>~ZIQ]eL*-K#'
~~~

This command should work to show it in SSH when used against a default log:

~~~
sed -n 7p ~/private/murmur/murmur.log
~~~

Mumble Client:
---

Now you need to install the [Mumble client](http://mumble.sourceforge.net/) for your platform.

Create a new server and use the Address:

~~~
server.feralhosting.com
~~~

Where server is the actual name of your feral server.

**Important note:** You can use this command to run more than once server instance. So be careful to check for before running it.

Use this command to see all running instances of the murmur server

~~~
ps x | grep murmur | grep -v grep
~~~

To kill the process (all running instances) use this command:

~~~
killall -u $(whoami) murmur.x86
~~~



