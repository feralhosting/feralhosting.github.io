

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot.

Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Aerofs introduction
---

Aerofs is essentially a peer to peer secure dropbox style app. You only share directly with your attached devices.

"AeroFS encrypts your data end-to-end, and only shares your files with those who you invite. Files are never stored in the public cloud."

Install AeroFS:
---

Please go to [https://aerofs.com/](https://aerofs.com/ "aerofs.com") and create an account.

~~~
wget -qO ~/aerofs.tgz https://dsy5cjk52fz4a.cloudfront.net/aerofs-installer.tgz
tar xf ~/aerofs.tgz
wget -qO ~/sharutils.deb http://ftp.uk.debian.org/debian/pool/main/s/sharutils/sharutils_4.11.1-1_amd64.deb
dpkg-deb -x ~/sharutils.deb ~/aerofs
cp -rf ~/aerofs/usr/bin/. ~/aerofs && rm -rf ~/aerofs/usr
rm -f ~/sharutils.deb && rm -f ~/aerofs.tgz
~~~

Add the path of the binary to your `PATH` for easy execution in your terminal using this command:

~~~
[[][/[][ ! "$(grep '~/aerofs' ~/.bashrc)" ]] && echo 'export PATH=~/aerofs:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

At first run we need set up the app and it work better in a screen, so type this command:

~~~
screen -S aerofs
~~~

Inside the screen type:

~~~
aerofs-cli
~~~

This will start the set-up process.

- Enter the email you registered with when prompted.

- Enter you password for this account when prompted.

- Enter the path you want for you Aerofs folder when prompted. This path will `~/Aerofs` by default if you just press enter.

When the set-up is complete press this keyboard sequence to detach from the screen:

Press and hold `CTRL` and `A` then press  `D`

Once you have setup up Aerofs you can start it easily using this command:

~~~
screen -dmS aerofs aerofs-cli
~~~

To use the process interactively use this command:

~~~
aerofs-sh
~~~

Here is the result:

~~~
AeroFS>
~~~

Type `help` to see the help page

~~~
AeroFS> help
~~~



