
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

**Important Note:** Do not install Python manually without a good reason. It will most likely cause more problems than is solves.

**Python 2.7.3 is already installed on your slot**

Type to show the current version:

~~~
python -V
~~~

To install python mods using the Feral python uses these steps:

**1:** Add the `~/.local/bin` location to your `PATH` using this command:

~~~
[ ! "$(grep '~/.local/bin' ~/.bashrc)" ] && echo 'export PATH=~/.local/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

**2:** Now install `virtualenv` like this:

~~~
easy_install --user virtualenv
~~~

Other mods can be installed using the `--user` argument, for example:

~~~
easy_install --user somemodule
~~~

For example:

~~~
easy_install --user pip
pip install --user requests
pip install --user HTMLParser
~~~

**3:** Now you can use VirtualENV with programs, for example, installing [flexget](http://flexget.com):

~~~
virtualenv ~/flexget/
~/flexget/bin/pip install flexget
~~~

**Related FAQ:** [Flexget - Basic installation](https://www.feralhosting.com/faq/view?question=234)

Installing Python locally:

You **do not** need to follow this FAQ to use python or python scripts. If you have a missing module you can open a ticket and ask staff to install it or use the above section to install it locally.

This is a basic guide to installing Python to your home directory . You will also be able to use `easy_install` to install mods.

### Python Active State 2.7.5.6:

Includes lots of things such as VirtualENV, distribute, PIP and more. Super simple to install.

~~~
wget -qO ~/ActivePython.tar.gz http://downloads.activestate.com/ActivePython/releases/2.7.5.6/ActivePython-2.7.5.6-linux-x86_64.tar.gz
tar xf ActivePython.tar.gz
bash ~/ActivePython-2.7.5.6-linux-x86_64/install.sh
~~~

Select a path to install to. This will create the path if it does not exist.

**Important note:** We do not recommend you install directly to `$HOME` or use this installation in the `PATH` over the existing version.  There will be problems if you do. Do something like this instead:

~~~
Install directory: ~/activestate
~~~

If you make an mistake while typing press and hold `CTRL` and press `backspace` to delete characters.

Read the information displayed, it will tell you what `PATH` to add and where.

Optional: To remove the installation files.

~~~
cd && rm -f ActivePython{-2.7.5.6-linux-x86_64.tar.gz,-2.7.5.6-linux-x86_64}
~~~

Type this command to reload the shell:

~~~
bash
~~~

To use `easy_install` with this installation use the full path to your installation.

~~~
~/activestate/bin/easy_install
~~~

Done.

Installing Python 2.7.6 from source:
--

In SSH do these commands. Use this FAQ if you do not know how to SSH into your slot: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

**Important note:** We do not recommend you install directly to `$HOME` or use this installation in the `PATH` over the existing version.  There will be problems if you do. Do something like this instead:

~~~
--prefix=$HOME/python/python.2.7
~~~

~~~
mkdir -p ~/python/python.2.7
wget -qO ~/Python-2.7.6.tgz http://www.python.org/ftp/python/2.7.6/Python-2.7.6.tgz
tar xf ~/Python-2.7.6.tgz && cd ~/Python-2.7.6
./configure --prefix=$HOME/python/python.2.7 && make && make install
~~~

The configuration and installation can take some time to be patient.

When it is finished installing, do some clean up with this command.

~~~
cd && rm -rf ~/Python{-2.7.6,-2.7.6.tgz}
~~~

Python has been installed. Now check which version is in use:

~~~
~/python/python.2.7/bin/python -V
~~~

Installing distribute
---

~~~
wget -qO ~/distribute_setup.py http://python-distribute.org/distribute_setup.py
~/python/python.2.7/bin/python ~/distribute_setup.py
cd && rm -f distribute_setup.py
~~~

Distribute is replacing setuptools.

Installing setuptools:
---

~~~
wget -qO ~/setuptools.egg https://pypi.python.org/packages/2.7/s/setuptools/setuptools-0.6c11-py2.7.egg
~/python/python.2.7/bin/python ~/setuptools.egg
cd && rm -f setuptools.egg
~~~

That is done. Python and set-up tools are now installed and added to your paths. There should be no need to prefix when installing mods.

Using `easy_install` from the command line to install mods:

~~~
~/python/python.2.7/bin/easy_install pip
~~~

~~~
~/python/python.2.7/bin/pip install virtualenv
~~~

~~~
~/python/python.2.7/bin/pip install flexget
~~~



