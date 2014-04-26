
Install Pydio
---

Formerly AjaXplorer, file sharing platform for the enterprise

In SSH do these commands. Use this FAQ if you do not know how to SSH into your slot: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

~~~
wget -qO ~/pydio.zip http://downloads.sourceforge.net/project/ajaxplorer/pydio/stable-channel/5.2.3/pydio-core-5.2.3.zip
unzip -qo ~/pydio.zip
cp -rf ~/pydio-core-5.2.3/. ~/www/$(whoami).$(hostname)/public_html/pydio
sed -i 's|//define("AJXP_LOCALE", "en_EN.UTF-8");|define("AJXP_LOCALE", "en_GB.UTF-8");|g' ~/www/$(whoami).$(hostname)/public_html/pydio/conf/bootstrap_conf.php
~~~

The last command sets the locale to `en.GB.UTF-8`.

Or you could edit it to be say `en_US.UTF-8` if you wanted.

Remove the files we don't need:

~~~
cd && rm -rf pydio{-core-5.2.3,.zip}
~~~

If you are using nginx you may want to do this:

Create a `.conf` file on the folder:

~~~
~/.nginx/conf.d/000-default-server.d
~~~

I will call mine `pydio.conf`. Now add these lines to it and save the changes.

~~~
location /pydio/ { }
location /pydio/conf/           { deny all; }
location /pydio/data/           { deny all; }
location /pydio/data/public     { allow all; }
location /pydio/robots.txt      { access_log off; log_not_found off; }
location /pydio/favicon.ico     { access_log off; log_not_found off; }
location ~ /pydio/\.            { access_log off; log_not_found off; deny all; }
location ~ /pydio/~$            { access_log off; log_not_found off; deny all; }
~~~

Now reload the configurations using this command (You can ignore errors about the log file):

~~~
/usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf
~~~

Now visit the URL (where `server` is name of your Feral Slot's server and your username):

~~~
https://server.feralhosting.com/username/ajaxplorer
~~~

Ignore the warnings.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/1.png)

Click "Start Wizard"

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup1.png)

This is an overview of the setup wizard:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup2.png)

Enter a username and password:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup2.5.png)

Configure the Global options as you wish, they can be left as they are:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup3.png)

Select "Database" from the drop down menu:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup4.png)

For this FAQ we use sqlite, so select sqlite from the drop down menu, the path is relative to the installation folder's root.

For mysql:

The socket path must start with `:` , for example:

~~~
:/media/DiskID/home/username/private/mysql/socket
~~~

This is a relevant FAQ - [Mysql - Change php settings using htaccess](https://www.feralhosting.com/faq/view?question=213) which will allow you to use `localhost` as the hostname.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup5.png)

Optional: Add some users if you wish. This can be done later:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup6.png)

Click on "Install AjaXplorer Now!" to finish the installation.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/setup7.png)

Once you have installed AjaXplorer you will create a "Workspace"

You start this process by clicking on your `username` in the top right, then clicking on `settings`

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/workspace1.png)

In the settings page click on `Workspaces` to view the drop down menu and then click on `New Workspace`

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/workspace2.png)

Now you can configure some basics of your new workspace. In this example I have used:

**Access Driver:** File System (Standard)
**Path:** The full path to the root of this workspace, which in my example is my root folder.
**File Creation Mask:** 0700 (0666 is the default)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Pydio%20-%20Basic%20setup/workspace3.png)



