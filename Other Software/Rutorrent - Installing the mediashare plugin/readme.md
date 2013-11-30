
Prerequisites:

* Install the Divx web player first. If this is not installed, rutorrent will appear to freeze when you attempt to play a file.

You must be able to connect via SSH to your slot -- all of these commands are run in SSH.

When following this guide, be aware that you do **not** need to modify the commands.

These steps will install the mediastream and filemanager plugins -- but will *not* configure them.

~~~
cd ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/
svn co -q http://svn.rutorrent.org/svn/filemanager/trunk/mediastream
svn co -q http://svn.rutorrent.org/svn/filemanager/trunk/filemanager
~~~

This step will clean up permissions so the plugin 'mediastream' will run correctly. If you get the error "Video cannot be found, it may have been removed", you likely need to look closer at these steps:

~~~
mkdir ~/www/$(whoami).$(hostname)/public_html/stream
ln -s ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/mediastream/view.php ~/www/$(whoami).$(hostname)/public_html/stream/
~~~

This step will update the config file to have the proper URL -- there is usually no need to modify any of this command:

~~~
sed -i "s|'http://mydomain.com/stream/view.php';|'http://$(whoami).$(hostname)/stream/view.php';|g" ~/www/$(whoami).$(hostname)/public_html/rutorrent/plugins/mediastream/conf.php
~~~

This guide is based off of the guide at http://www.torrent-invites.com/seedbox-tutorials/210810-watching-video-your-seedbox-rutorrent-mediastream.html, but updated to run without needing administrative access.

Please refer to the images there to see how to use this plugin once installed.



