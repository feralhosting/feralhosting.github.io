
**Important note:** Owncloud does not work with nginx.

Owncloud Manual installation

In [SSH](https://www.feralhosting.com/faq/view?question=12) run this command. It will download the `setup.php` to the root of your `WWW`

~~~
wget -qP ~/www/$(whoami).$(hostname)/public_html/ https://download.owncloud.com/download/community/setup-owncloud.php
~~~

Now visit the URL in your browser, it will look something like this:

~~~
http://server.feralhosting.com/username/setup-owncloud.php
http://username.server.feralhosting.com/setup-owncloud.php
~~~

You should be able to just click on this file from your apache/h5ai index.

**1:** Just click next

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/web-install-1.png)

**2:** Leave the installation directory as `owncloud`. This will create and install it to a the `/owncloud` directory in your server root.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/web-install-2.png)

**3:** Click next when done to visit the final stage of the setup.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/web-install-3.png)

The easiest way to install Owncloud is to use the sqlite database option (default). Using MySQL can be done but requires a lot of extra steps that we are not going to cover in this basic set-up.

Once you have visited the URl in a browser you will see this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Owncloud%20-%20Basic%20setup/1.png)

Using Owncloud with the valid SSL URL format instead of the default.
---

If you want to be able to use the valid SSL URL with owncloud you must make these edits.

Inside your `/owncloud` installation is a folder called `config` and inside this is a file called `config.php`.

So the relative path to to this file from your server root will be:

~~~
owncloud/config/config.php
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



