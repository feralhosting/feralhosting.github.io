
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Use these first two commands to create to do some pre requisite tasks:

~~~
mkdir -p ~/programs
[[ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Protobuf
---

This is a required dependency that is not included with your slot.

~~~
wget -qO ~/protobuf-2.5.0.tar.gz http://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz
tar xf ~/protobuf-2.5.0.tar.gz && cd ~/protobuf-2.5.0
./configure --prefix=$HOME/programs && make && make install && cd
rm -rf  ~/protobuf-2.5.0.tar.gz ~/protobuf-2.5.0
~~~

Mosh
---

Now download and install `mosh`:

~~~
wget -qO ~/mosh-1.2.4.tar.gz http://mosh.mit.edu/mosh-1.2.4.tar.gz
tar xf ~/mosh-1.2.4.tar.gz && cd ~/mosh-1.2.4
./configure --prefix=$HOME/programs PKG_CONFIG_PATH=$HOME/programs/lib/pkgconfig
make && make install && cd
rm -rf ~/mosh-1.2.4.tar.gz ~/mosh-1.2.4
~~~

Add the `LD_LIBRARY_PATH` using this command to overcome this error:

~~~
mosh-server: error while loading shared libraries: libprotobuf.so.8: cannot open shared object file: No such file or directory
~~~

By using this command:

~~~
[[ ! "$(grep '~/programs/lib' ~/.bashrc)" ]] && echo 'export LD_LIBRARY_PATH=~/programs/lib:$LD_LIBRARY_PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Connect to your slot using this command.

For older versions of `mosh`

~~~
mosh username@server.feralhosting.com --server="LANG=$LANG mosh-server"
~~~

For 1.2.4 +

~~~
mosh username@server.feralhosting.com
~~~


