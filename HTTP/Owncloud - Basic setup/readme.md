
**Important note:** For using Owncloud With nginx please see the nginx section of this guide.

Owncloud Manual installation
---

In [SSH](https://www.feralhosting.com/faq/view?question=12) run this command. It will download the `setup.php` to the root of your `WWW`

~~~
wget -P ~/www/$(whoami).$(hostname)/public_html/ https://download.owncloud.com/download/community/setup-owncloud.php
~~~

Now visit the URL in this format, in your browser, it will look something like this:

**Important note:** If you use or force https you may need to unblock the remote content of the installer in Firefox.

![](https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/https.png)

~~~
http://username.server.feralhosting.com/setup-owncloud.php
~~~

You should be able to just click on this file from your apache/nginx/h5ai index.

**1:** Just click next

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/web-install-1.png)

**2:** Leave the installation directory as `owncloud`. This will create and install it to a the `/owncloud` directory in your server root.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/web-install-2.png)

**3:** Click next when done to visit the final stage of the setup.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/web-install-3.png)

The easiest way to install Owncloud is to use the sqlite database option (default). Using MySQL can be done but requires a lot of extra steps that we are not going to cover in this basic set-up.

Once you have visited the URL in a browser you will see this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/1.png)

Using Owncloud with the valid SSL URL format instead of the default.
---

If you want to be able to use the valid SSL URL with owncloud you must make these edits.

Inside your `/owncloud` installation is a folder called `config` and inside this is a file called `config.php`.

So the relative path to to this file from your server root will be:

~~~
owncloud/config/config.php
~~~

To edit this file using nano:

~~~
nano -w ~/www/$(whoami).$(hostname)/public_html/owncloud/config/config.php
~~~

Open this file with a text editor and add these new options:

~~~
  'overwritehost' => 'server.feralhosting.com',
  'overwritewebroot' => '/username/owncloud',
~~~

Where `server` is the name of your Feral server that is hosting owncloud and where `username` is your Feral username.

Once you have done this is will look something like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/config.png)

Now Owncloud will work with the valid SSL URL format and not the other. All 3rd party apps will also work, so this is the best approach to dealing with the issue.

These options are taken from the `config.sample.php` located in the same directory.

nginx
---

**Important note:** This configuration depends on the user installing owncloud to the WWW subdirectory `/owncloud`

**Owncloud custom conf:**

Now download a preconfigured conf file to use in conjunction with this edit:

~~~
wget -qO ~/.nginx/conf.d/000-default-server.d/owncloud.conf http://git.io/nVy4Cg
~~~

Now run this command in SSH:

**Important note:** You need to run this command at least once to properly configure the `owncloud.conf`

~~~
sed -ri "s|fastcgi_pass(.*);|fastcgi_pass    unix:$HOME/.nginx/php/socket;|g" ~/.nginx/conf.d/000-default-server.d/owncloud.conf
~~~

Now reload nginx:

~~~
/usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf
~~~

Owncloud should now work as intended with nginx.



