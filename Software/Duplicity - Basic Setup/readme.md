
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

What is Duplicity?
---

[duplicity](http://duplicity.nongnu.org/): Encrypted bandwidth-efficient backup using the rsync algorithm

Duplicity backs directories by producing encrypted tar-format volumes and uploading them to a remote or local file server. Because duplicity uses librsync, the incremental archives are space efficient and only record the parts of files that have changed since the last backup. Because duplicity uses GnuPG to encrypt and/or sign these archives, they will be safe from spying and/or modification by the server.

Installation
---

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

1: Do these preparation steps:

~~~
mkdir -p ~/programs
[[][/[][ ! "$(grep '~/.local/bin' ~/.bashrc)" ]] && echo 'export PATH=~/.local/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
[[][/[][ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

2: Install librsync

~~~
wget -qO ~/librsync.tar.gz http://downloads.sourceforge.net/project/librsync/librsync/0.9.7/librsync-0.9.7.tar.gz
tar xf ~/librsync.tar.gz && cd ~/librsync-0.9.7
./configure --prefix=$HOME/programs --with-pic
make && make install && cd && rm -rf ~/librsync-0.9.7 ~/librsync-0.9.7
~~~

3: Install Duplicity

~~~
wget -qO ~/duplicity.tar.gz http://code.launchpad.net/duplicity/0.6-series/0.6.22/+download/duplicity-0.6.22.tar.gz
tar xf ~/duplicity.tar.gz && cd ~/duplicity-0.6.22
python setup.py install --prefix=$HOME/.local --librsync-dir=$HOME/programs
cd && rm -rf ~/duplicity-0.6.22 ~/duplicity.tar.gz
~~~

Check it was installed correctly.

~~~
duplicity --version
duplicity --help
~~~



