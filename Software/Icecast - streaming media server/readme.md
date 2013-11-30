
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Installing Icecast On To Your Feralhosting Slice!
---

**0:** Make sure you have enough time to do this. It can take from a couple minutes, to a couple hours! Hopefully this guide will keep it to a couple minutes! 

**1:** These dependencies are now installed on all servers by default. IF you have any issues Open a ticket asking for an install of "libxml2", "libxslt" and "libogg/libvorbis-devel".

**2:** SSH in to your Feral slice

**3:** Run this:

~~~
svn co -q http://svn.xiph.org/icecast/trunk/icecast ~/icecast
~~~

This will download icecast SVN, you do not have to use the SVN.

**4:** Once this has finished cd to your icecast folder:

~~~
mkdir -p ~/private/icecast/var/log/icecast && cd ~/icecast
~~~

**5:** Now, run autogen: 

~~~
./autogen.sh --prefix="$HOME/private/icecast"
~~~

Where the prefix is the location you want to install icecast to. If you are following along with this guide for the first time or you are unsure of what to put at the prefix, simply use the provided command.

**6:** Now we need to make, simply type: 

~~~
make && make install
~~~

**7:** After "make" finishes, we need to run 

We should receive no errors. However, if you do receive a permissions error check your prefix that we set in step 5!

**8:** After "make install" finishes you need to edit your "icecast.xml" to your liking, I will not cover editing that here, you can look elsewhere online on editing your "icecast.xml". You can edit this via the ssh tunnel you have open or just open it directly in an FTP client then saving it back to the server. This file can be found in the folder:

~~~
~/private/icecast/etc/icecast.xml
~~~

**9:** Now we need to run icecast on our server. First navigate to the bin folder: 

Now use this command to run the server: 

~~~
~/private/icecast/bin/./icecast -c ~/private/icecast/etc/icecast.xml
~~~

This will start our icecast server using the configuration file you set up in step five.

**10:** Your server is now up and running the final thing you need to do is set up your source client.
A few clients you can use are Nicecast(MAC), ices2, ices0.

**11:** A final thing, make sure you set up your mount point in your source client! If you do not do this, no one will be able to listen to your stream!





