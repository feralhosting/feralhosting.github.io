
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

Use this command to create the `~/bin` directory and reload your shell for this change to take effect.

~~~
mkdir -p ~/bin && bash
~~~

Use these first two commands to create to do some pre requisite tasks:

First we need a pretty important, but optional, ruby dependency.  This lets us have a "history" in our ruby shell.

~~~
wget -qO ~/readline.tar.gz ftp://ftp.cwru.edu/pub/bash/readline-6.3.tar.gz
tar xf ~/readline.tar.gz && cd readline-6.3
./configure --prefix=$HOME && make && make install
cd && rm -rf readline{.tar.gz,-6.3}
~~~

Install the program using these commands:

~~~
wget -qO ~/ruby.tar.gz http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.3.tar.gz
tar xf ~/ruby.tar.gz && cd ~/ruby-2.1.3
./configure --prefix=$HOME && make && make install
cd && rm -rf ruby{-2.1.3,.tar.gz}
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



