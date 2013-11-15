
This guide is intended for GNU Linux users who wish to mount their server onto their local file system so they can quickly access files stored there. This guide is prepared for Ubuntu but users of other Linux distributions should use their own package managers to install to necessary software. 

### Installation & Configuration

**1:** Install the `sshfs` package (use `apt-get` instead of `aptitude` on some versions)

~~~
sudo aptitude install sshfs
~~~

**2:** Add yourself to group `fuse`

~~~
sudo adduser $USER fuse
~~~

If using `$USER` creates problems, substitute it for your local username.

**3:** Log out and log back in again for the changes to take effect

**4:** Create a local directory where you want to mount your data

~~~
mkdir ~/feral
~~~

**5:** Perform initial test to see if you can mount manually

~~~
sshfs -o idmap=user username@server.feralhosting.com:/media/DiskID/home/username ~/feral
~~~

**6:** If all went well and you don't want to automount (and automate) this, then you are finished. Simply run the previous command whenever you want accesss! Run this command to safely unmount: 

~~~
fusermount -u ~/feral
~~~

### Advanced

**7:** Those who wish to automount their server need to edit /etc/fstab:

~~~
sudo nano /etc/fstab
~~~

**8:** Add the following line to the end of fstab:

~~~
sshfs#username@server.feralhosting.com:/media/DiskID/home/username /home/localusername/feral/ fuse    user,idmap=user 0 0
~~~

**9:** Run `sudo mount -a` and your server should mount OK. On the next reboot it should all work automatically.



