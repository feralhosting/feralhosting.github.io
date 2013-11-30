
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Curl installation
---

**Important note:** `curl`  is already installed on your slot though it is located here instead:

~~~
/opt/curl/current
~~~

Curl manual installation:
---

Use these first two commands to create to do some pre requisite tasks:

~~~
mkdir -p ~/programs
[[][/[][ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Install the program using these commands:

~~~
wget -qO ~/curl.tar.gz http://curl.haxx.se/download/curl-7.33.0.tar.gz
tar xf ~/curl.tar.gz && cd ~/curl-7.33.0
./configure --prefix=$HOME/programs
make && make install && cd
rm -rf ~/curl-7.33.0 ~/curl.tar.gz
~~~

Check your version:

~~~
curl -V
~~~



