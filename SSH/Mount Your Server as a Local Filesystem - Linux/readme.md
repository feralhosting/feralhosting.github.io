
This guide is intended for GNU Linux users who wish to mount their server onto their local file system so they can quickly access files stored there. This guide is prepared for Ubuntu but users of other Linux distributions should use their own package managers to install to necessary software. 

[h3]Installation & Configuration[/h3]
[b]1:[/b] Install the [i]sshfs[/i] package (use [i]apt-get[/i] instead of [i]aptitude[/i] on some versions)

[code]sudo aptitude install sshfs[/code]
[b]2:[/b] Add yourself to group [i]fuse[/i]

[code]sudo adduser $USER fuse[/code]
If using [i]$USER[/i] creates problems, substitute it for your local username.

[b]3:[/b] Log out and log back in again for the changes to take effect

[b]4:[/b] Create a local directory where you want to mount your data

[code]mkdir ~/feral[/code]
[b]5:[/b] Perform initial test to see if you can mount manually

[code]sshfs -o idmap=user username@server.feralhosting.com:/media/DiskID/home/username ~/feral[/code]
[b]6:[/b] If all went well and you don't want to automount (and automate) this, then you are finished. Simply run the previous command whenever you want accesss! Run this command to safely unmount: 

[code]fusermount -u ~/feral[/code]
[h3]Advanced[/h3]
[b]7:[/b] Those who wish to automount their server need to edit /etc/fstab:

[code]sudo nano /etc/fstab[/code]
[b]8:[/b] Add the following line to the end of fstab:

[code]sshfs#username@server.feralhosting.com:/media/DiskID/home/username /home/localusername/feral/ fuse    user,idmap=user 0 0[/code]
[b]9:[/b] Run [i]sudo mount -a[/i] and your server should mount OK. On the next reboot it should all work automatically.



