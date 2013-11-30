
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

ImageMagick installation
---

**Important note:** ImageMagick can be installed upon request of the user by [opening a ticket](https://www.feralhosting.com/manager/tickets/new):

Manual installation:
---

Use these first two commands to create to do some pre requisite tasks:

~~~
mkdir -p ~/programs
[[][/[][ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Install the program using these commands:

~~~
wget -qO ~/imagemagick.tar.gz http://www.imagemagick.org/download/ImageMagick.tar.gz
tar xf ~/imagemagick.tar.gz
cd ~/ImageMagick-6.8.7-5
./configure --prefix=$HOME/programs
make && make install && cd 
rm -rf ~/imagemagick.tar.gz ~/ImageMagick-6.8.7-5
~~~


