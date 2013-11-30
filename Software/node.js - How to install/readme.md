
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

node.js installation
---

These commands will download the linked version of node.js and set it up inside your `~/private` directory.

This downloads the `node-v0.10.22-linux-x64.tar.gz` and then saves it as `node.tar.gz` in your  `~/private` directory.

~~~
wget -qO ~/node.js.tar.gz http://nodejs.org/dist/v0.10.22/node-v0.10.22-linux-x64.tar.gz
~~~

This unpacks the folder archived inside the node.tar.gz.

~~~
tar xf ~/node.js.tar.gz
~~~

This moves and renames the recently unpacked folder to `~/node`

~~~
cp -rf ~/node-v0.10.*-linux-x64/. ~/programs
~~~

This deletes the tar archive and unpacked folder we no longer need.

~~~
rm -rf ~/node.js.tar.gz  ~/node-v0.10.*-linux-x64
~~~

This command appends the path to the bottom of the `~/.bashrc` for you. As long as you have not changed the paths in the previous commands. If you have, for example, decided to store the main directory in the root, you need to edit the path in the echo.

~~~
[[][/[][ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Tries to call `node.js` to check the version:

~~~
node -v
~~~

Which should return:

~~~
v0.10.22
~~~

If you see the version then it is ready to use.

Once you have done this, you are ready to start writing and running your `node.js` apps from anywhere in your account. I personally put all my apps in `~/node/apps/` to keep things tidy though.

### Install from source:

**Important note:** node takes a very long time to compile from source.

~~~
wget -qO ~/node.tar.gz http://nodejs.org/dist/v0.10.22/node-v0.10.22.tar.gz
tar xf ~/node.tar.gz && cd ~/node-v0.10.*
./configure --prefix=$HOME/programs
make && make install && cd
rm -rf ~/node-v0.10.*/ ~/node.tar.gz
~~~



