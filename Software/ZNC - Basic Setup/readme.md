
Current latest stable version of ZNC is: `1.2`

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
wget -qO ~/znc-1.2.tar.gz http://znc.in/releases/znc-latest.tar.gz
tar xf ~/znc-1.2.tar.gz && cd ~/znc-1.2
./configure --prefix=$HOME && make && make install
cd && rm -rf znc{-1.2,1.2.tar.gz}
~~~

Once it is installed and ready we can start to configure `znc` using this command:

~~~
znc --makeconf
~~~



