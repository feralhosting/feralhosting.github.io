
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

node.js installation
---

Use this command to create the `~/bin` directory and reload your shell for this change to take effect.

~~~
mkdir -p ~/bin && bash
~~~

This command downloads the `node-v0.10.24-linux-x64.tar.gz` and then saves it as `node.tar.gz` in your servers root directory.

~~~
wget -qO ~/node.js.tar.gz http://nodejs.org/dist/v0.10.24/node-v0.10.24-linux-x64.tar.gz
~~~

This unpacks the folder archived inside the node.tar.gz.

~~~
tar xf ~/node.js.tar.gz
~~~

This copies the contents of the unpacked archive to your server root using  `~/`:

~~~
cp -rf ~/node-v0.10.24-linux-x64/. ~/
~~~

This deletes the tar archive and unpacked folder we no longer need.

~~~
cd && rm -rf node{.js.tar.gz,-v0.10.24-linux-x64}
~~~

Tries to call `node.js` to check the version:

~~~
node -v
~~~

Which should return:

~~~
v0.10.24
~~~

If you see the version then it is ready to use.

Once you have done this, you are ready to start writing and running your `node.js` apps from anywhere in your account. I personally put all my apps in `~/node/apps/` to keep things tidy though.

Install from source
---

**Important note:** node takes a very long time to compile from source.

Use this command to create the `~/bin` directory and reload your shell for this change to take effect.

~~~
mkdir -p ~/bin && bash
~~~

Now run these commands:

~~~
wget -qO ~/node.tar.gz http://nodejs.org/dist/v0.10.24/node-v0.10.24.tar.gz
tar xf ~/node.tar.gz && cd ~/node-v0.10.24
./configure --prefix=$HOME
make && make install && cd
rm -rf ~/{node-v0.10.24,node.tar.gz}
~~~



