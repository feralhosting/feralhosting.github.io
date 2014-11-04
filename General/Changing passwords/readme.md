
Account Manager
---

> **Important note:** To prevent emails going into your spam folder you can white-list the domain `@feralhosting.com` to be safe before asking for a password reset. 

[How to whitelist an email address with Gmail, Outlook.com or Yahoo! Mail](http://onlinegroups.net/blog/2014/02/25/how-to-whitelist-an-email-address/)

To change your password for the `www.feralhosting.com` website and Account Manager, please use this method:

[Recover account](https://www.feralhosting.com/recover-account)

Installable Software
---

A few of these methods will require you to use the command-line. [SSH guide basics - PuTTy](https://www.feralhosting.com/faq/view?question=12) or [SSH guide basics - OS X](https://www.feralhosting.com/faq/view?question=217)

Deluge WebUi password
---

To change the Deluge WebUI password:

**1:** Login to the WebUI using the details in your Software Status page

**2:** Click on `Preferences`

**3:** Click on `Interface` in the menu that opens up

**4:** Enter your old password

**5:** Enter the new password you wish to use!

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/General/Changing%20passwords/deluge.png)

Transmission Password
---

> **Important note:** Transmission cannot manually restarted by the user. After killing the process allow up to 5 minutes for it to automatically to restart.

To change the password in Transmission, you will need to [SSH](https://www.feralhosting.com/faq/view?question=12) into your slot and stop it with this command:

~~~
killall -9 -u $(whoami) transmission-daemon
~~~

Then edit the file using this command:

Optionally, you can edit it over FTP, please read and understand this FAQ first - [Text editing - Over FTP or SFTP](https://www.feralhosting.com/faq/view?question=219)

~~~
nano -w ~/.config/transmission-daemon/settings.json
~~~

You need to edit a setting called:

~~~
rpc-password
~~~

It iwll look something like this (hashed):

~~~
"rpc-password": "{1ef8c83d004191e6db813e30be525c4b116e3da4BE6155cy",
~~~

You enter your new password in plain text like this.

~~~
"rpc-password": "NEChu=@f%o9i*MH$SUZs",
~~~

Transmission will hash your password automatically when it starts.

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

> **Important note:** Make sure you finish editing the file before it starts back otherwise things might not work.

ruTorrent WebUI Password
---

**Important Note:** Please also see this FAQ to manage your rutorrent password and users: [Password protect your WWW folder](https://www.feralhosting.com/faq/view?question=22)

If you simply want to reset your ruTorrent password, you can request a reinstall from the `Install Software` link in your [Account Manager](https://www.feralhosting.com/manager/) to get a new system-generated password for your ruTorrent web interface. 

If you want to set a custom password for your ruTorrent WebUI, you will need to [SSH](https://www.feralhosting.com/faq/view?question=12) to your slot, and make changes to the `.htpasswd` file, using the `htpasswd` program. Again, please see this FAQ: [Password protect your WWW folder](https://www.feralhosting.com/faq/view?question=22)

By default, when rutorrent is installed from the `Install Software` link in your [Account Manager](https://www.feralhosting.com/manager/), it places the `.htpasswd` file in the rutorrent folder.

To use `htpasswd`, you need to execute the following set of commands in the shell:

~~~
htpasswd -m ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/.htpasswd username
~~~

> **Important note:** Replace `username` with your Feral user name. This will prompt to update the password for this user if they exist instead of creating a new one.

At this point, you will be prompted to enter your new password, and then verify.

If you get the following error, it means that the location of your `.htpasswd` file is not where you specified:

~~~
htpasswd: cannot modify file /media/DiskID/home/username/www/username.server.feralhosting.com/public_html/rutorrent/.htpasswd; use '-c' to create it
~~~

Then please adjust the command line accordingly, from inside the rutorrent folder:

~~~
htpasswd -cm ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/.htpasswd username
~~~

This will create a new and hashed `.htpasswd` file.

You can get more info about the `htpasswd` command by typing `htpasswd` in SSH without any options. It will then display the options and switches you can use.

### Shell (SSH), FTP, and SFTP Passwords

Changing the default shell access password complicates things for the support team when you need their help. You will need to include your new password with every support ticket. If you are just looking to simplify your login procedure in PuTTY, consider [setting up publickey authentication](https://www.feralhosting.com/faq/view?question=13).

FTP and your SFTP password can be changed by logging in via PuTTY and typing this command:

~~~
passwd
~~~

You should then see on-screen prompts asking you for your current and new passwords.

If you don't remember your originally assigned password, please go to the [Slot Details](https://www.feralhosting.com/manager/slot/) for your slot, and it will be listed there.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)



