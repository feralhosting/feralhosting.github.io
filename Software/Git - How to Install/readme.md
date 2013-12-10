
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Git 1.7.10.4
---

This command will show you your installed Git version

~~~
git --version
~~~

If you specifically need a higher version you can used the FAQ to install 1.8.5.1

Git 1.8.5.1
---

You need to SSH into your slot to complete this guide. If you don't know how to do this [here is a basic guide](https://www.feralhosting.com/faq/view?question=12)

~~~
mkdir -p ~/programs
[ ! "$(grep '~/programs/bin' ~/.bashrc)" ] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

~~~
wget -qO ~/git-1.8.5.1.tar.gz http://git-core.googlecode.com/files/git-1.8.5.1.tar.gz
tar xf ~/git-1.8.5.1.tar.gz && cd ~/git-1.8.5.1
./configure --prefix=$HOME/programs --with-curl=/opt/curl/current
make && make install && cd && rm -rf ~/{git-1.8.5.1,git-1.8.5.1.tar.gz}
~~~

Then do this to check the version.

~~~
git --version
~~~

If the version is still `1.7.10.4` do this command then try again:

~~~
source ~/.bashrc
~~~

You can now do things like clone. Here is an example command:

~~~
git clone git://github.com/username/repo.git ~/where/you/want/this/repo
git clone https://github.com/username/repo.git ~/where/you/want/this/repo
~~~



