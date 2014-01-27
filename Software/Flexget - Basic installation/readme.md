
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Flexget Setup
---

Create our VirtualENV environment using `pip`. Do not use `easy_install` to install `virtualenv`

~~~
easy_install --user pip
~/.local/bin/pip install --user virtualenv
~/.local/bin/virtualenv ~/flexget/
~/flexget/bin/pip install flexget
~~~

**Important note:** If you installed `virtualenv` using `easy_install` and have some errors when trying to create a virtual environment, then do these steps:

~~~
easy_install --user pip
~/.local/bin/pip uninstall virtualenv
cd && rm -rf .local/bin/virtualenv*
~/.local/bin/pip install --user virtualenv
~/.local/bin/virtualenv ~/flexget/
~/flexget/bin/pip install flexget
~~~

Running flexget
---

Now you can either call `flexget` directly like this:

~~~
~/flexget/bin/flexget
~~~

Or use this command to activate in this SSH session:

~~~
source ~/flexget/bin/activate
~~~

Once it is activated all you need to do is

~~~
flexget
~~~

Experimental Web Gui:

~~~
flexget-webui --port PORT --username USERNAME --password PASSWORD -d
~~~

Then connect to the Web Gui in a browser using the URL format:

~~~
server.feralhosting.com:PORT
~~~

**server** = Your Feral server name that hosts the slot you installed Flexget on

**PORT** = a port between 5000 and 55000

**USERNAME** = Your Feral username

**PASSWORD** = A password just for the Web Gui

RSS Configuration
---

The `config.yml` file can be found here:

~~~
~/.flexget/config.yml
~~~

You can test and debug it before using here like this:

~~~
~/flexget/bin/flexget --test
~~~

The RSS/filter configuration will require some reading up so here is a link:

[http://flexget.com/wiki/Configuration](http://flexget.com/wiki/Configuration)



