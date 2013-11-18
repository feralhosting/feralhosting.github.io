
You will need to have MySQL already installed. You can do this from your [Manager](https://www.feralhosting.com/manager/)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/install_mysql.png)

In SSH do these commands. Use this FAQ if you do not know how to SSH into your slot: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

### Download and extract

Download the phpBB3 package:

~~~
wget -qO ~/phpBB-3.0.12.zip https://www.phpbb.com/files/release/phpBB-3.0.12.zip
~~~

Then extract the file archive:

~~~
unzip -qo ~/phpBB-3.0.12.zip -d ~/www/$(whoami).$(hostname)/public_html
~~~

Optional: Clean up by removing the phpBB3 zip

~~~
rm -f ~/~/phpBB-3.0.12.zip
~~~

### Preparation

**1:** Make a limited access user and a new database to use with phpBB3 - [Adminer - MySQL administration](https://www.feralhosting.com/faq/view?question=116)

**2:** Set your default mysql and mysqli socket paths - [PHP - modify settings](https://www.feralhosting.com/faq/view?question=213)

**3:** The continue with the installation using `mysql + mysqli extenstion` and `localhost` as the hostname.

### Installation

phpBB3 is now ready to install via a web browser.

It is highly recommended you follow this FAQ and create a new database with a limited user instead of using root- [How to install MySQL and MySQL Adminer for easy MySQL administration](https://www.feralhosting.com/faq/view?question=116)

Next Visit the web based installer, which by default is at

~~~
www/username.feralhosting.com/public_html/phpbb3/
~~~

Progress with the installer.

**Important note:** Feral does not include email support via php mail. You will have to configure phpBB3 to use an external smtp service, like Google Apps.

### Database settings

**Important note:** Make sure you completed step 3 of the preparation.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/phpBB3 - basic setup/dbsettings.png)

### URL Settings

While phpBB3 can use both URL formats, it will default to `username.server.feralhosting.com` as the primary URL format (noticeable with login redirects and similar). 

Fortunately we can change this without having to hack phpbb3.

When you arrive at Server URL Settings page of the installer, follow the pointers in the image to make the server.feralhosting.com/username URL format the default and primary one.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/phpBB3 - basic setup/urlsettings.png)



