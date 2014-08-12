
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

If you specifically need a higher version you can used this FAQ to install a newer version.

Git 2.0.3
---

You need to SSH into your slot to complete this guide. If you don't know how to do this [here is a basic guide](https://www.feralhosting.com/faq/view?question=12)

~~~
mkdir -p ~/bin && bash
~~~

Now install git using these commands:

~~~
wget -qO ~/git-2.0.3.tar.gz https://www.kernel.org/pub/software/scm/git/git-2.0.3.tar.xz
tar xf ~/git-2.0.3.tar.gz && cd ~/git-2.0.3
./configure --prefix=$HOME --with-curl=/opt/curl/current
make && make install
cd && rm -rf git{-2.0.3,-2.0.3.tar.gz}
~~~

Then do this to check the version.

~~~
git --version
~~~

If the version is still `1.7.10.4` then open a new SSH connection for the changes to take effect:

You can now do things like clone. Here is an example command:

~~~
git clone git://github.com/username/repo.git ~/where/you/want/this/repo
git clone https://github.com/username/repo.git ~/where/you/want/this/repo
~~~

Install from github source.
---

For the latest git you can do this.

**Important note:** Only use this method if you require the very latest code. Otherwise user the officially released tar ball in the previous section.

~~~
wget -qO ~/git.zip https://github.com/git/git/archive/master.zip
unzip -qo ~/git.zip && cd git-master
make configure
./configure --prefix=$HOME --with-curl=/opt/curl/current
make && make install
cd && rm -rf git{.zip,-master}
~~~



