
This is a community written FAQ, and is supported by Feral customers in the [#Feral](https://www.feralhosting.com/chat) IRC channel, and not by Feral Hosting itself.

Prerequisites:

*You must be able to connect via SSH to your slot -- all of these commands are run in SSH. Related tutorial:  [How to SSH Into Your Feral Slot](https://www.feralhosting.com/faq/view?question=12)

These steps are run exactly as written. please do not modify them.

These will install the plugin, but not configure it.

~~~
cd ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/
svn co -q http://svn.rutorrent.org/svn/filemanager/trunk/filemanager
svn co -q http://svn.rutorrent.org/svn/filemanager/trunk/fileshare
ln -s ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/fileshare/share.php ~/www/$(whoami).$(hostname)/public_html/
~~~

These steps are run exactly as written. please do not modify them.

These will fix the bug in the plugin that wont let it run, and will configure it to run on your slot.

~~~
sed "/if(getConfFile(/d" -i ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/fileshare/share.php
sed "s|robits.org/rutorrent|$(whoami).$(hostname)|g" -i ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/fileshare/conf.php
~~~


Based on the directions located [here.](http://forums.rutorrent.org/index.php?topic=705.0)




