
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot.

Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Ruby installation
---

**Important note:** Ruby 1.9 is already installed on your slot. Use this command to check the existing version:

~~~
ruby -v
~~~

Ruby manual installation
---

Use these first two commands to create to do some pre requisite tasks:

~~~
mkdir -p ~/programs
[[][/[][ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Install the program using these commands:

~~~
wget -qO ~/ruby.tar.gz http://cache.ruby-lang.org/pub/ruby/2.0/ruby-2.0.0-p247.tar.gz
tar xf ~/ruby.tar.gz && cd ~/ruby-*
./configure --prefix=$HOME/programs && make && make install
cd && rm -rf ~/ruby-* ~/ruby.tar.gz
~~~

Now these to check your versions:

~~~
ruby -v
gem -v
~~~

This command to update gems:

~~~
gem update --system
~~~



