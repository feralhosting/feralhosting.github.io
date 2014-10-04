
### ruTorrent Is Not a Bittorrent client

It is important that you understand that ruTorrent is not a bittorrent client, which is why it cannot crash and cannot be restarted. It is a web application that runs in the browser and is dependant on things like apache/nginx and php.

ruTorrent is a web-based user interface (WebUi) for [rTorrent](http://www.feralhosting.com/faq/view?question=2) which is a bittorrent client. rTorrent runs quietly in shell and you do not get to see it most of the time unless you want to. You use your web browser to load ruTorrent — ruTorrent connects to rTorrent behind the scenes and shows you what goes on in rTorrent, your bittorrent client.

You might compare ruTorrent to a remote control, and rTorrent to a TV set.

Apart from having an excellent, very much uTorrent-like user interface, ruTorrent extends rTorrent's functionality considerably through the use of plugins. You will be able to create torrents, use RSS feeds, delete torrents with data, choose custom locations for data, use labels, sort your torrents by label, tracker, ratio, name, state, peers, seeds, creation date and more.

### Plugins

On Feral servers ruTorrent is autoinstalled (using the Software Manager page) with a recommended set of plugins.

Explore all the [available plugins](http://code.google.com/p/rutorrent/wiki/Plugins). Should you wish to try any of them apart from those that came preinstalled with your ruTorrent, just upload them to `/rutorrent/plugins`.

[Rutorrent - Installing the mediashare plugin](https://www.feralhosting.com/faq/view?question=209)
[Rutorrent - Colored Ratio Column Plugin](https://www.feralhosting.com/faq/view?question=184)
[Rutorrent - Installing the fileshare plugin](https://www.feralhosting.com/faq/view?question=210)
[Feralstats plugin for ruTorrent](https://www.feralhosting.com/faq/view?question=126)

The idea is a simple one. You upload the plugin folder to your `rutorrent/plugins` folder.

~~~
~/www/username.server.feralhosting.com/public_html/rutorrent/plugins
~~~

Where username is your Feral username and server is the name of the server that is hosting rutorrent.

### Troubleshooting

**Error:** ruTorrent fails to load and gets stuck showing the `loading` spinner

Clear your browser cache (also known as `temporary files`, not just history), restart your browser and reload ruTorrent, in this particular order.

[Firefox](http://support.mozilla.org/en-US/kb/how-clear-firefox-cache)

[Chrome](https://support.google.com/chrome/answer/95582?hl=en)

If this doesn't work, one of your browser extensions/plugins may be conflicting with ruTorrent. Test ruTorrent in your browser's incognito/private browsing mode. If this works, try disabling your extensions/plugins one by one to see which is causing the conflict.

**Important note:** AdBlock users on Eros: AdBlock blocks what it thinks are ads coming from domains that match the `/eros.` rule, which includes `eros.feralhosting.com`. This will stop ruTorrent loading correctly over HTTPS, causing it to look like: 

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/eros.png)

To prevent this, simply add `*.feralhosting.com` to your AdBlock exceptions list, or disable AdBlock.

**Error:** `could not connect to rTorrent — check if rTorrent is really running` in message in the logger:

This error means that ruTorrent failed to connect to rTorrent — rTorrent probably crashed.

In most cases rTorrent will be restarted by the system automatically within 10 minutes, after which you'll be able to load ruTorrent.

If after 10 minutes you are still unable to load ruTorrent, then something is preventing rTorrent from being restarted.

To manually restart your client, please refer to the following FAQ: [Restarting rtorrent, Deluge, Transmission, or MySQL](https://www.feralhosting.com/faq/view?question=158)

**Error:** `Torrent was not passed to rTorrent` - This error mostly happens when the size of the `.torrent` you're trying to load using ruTorrent is too big. As a workaround, upload the `.torrent` via FTP/SFTP to

~~~
~/private/rtorrent/watch
~~~

This folder is called a `watch` folder — any torrent you put there will be loaded automatically in rTorrent within seconds.

### nginx

If you see this error with rutorrent:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/nginxrutorrent.png)

Run this command in [SSH](https://www.feralhosting.com/faq/view?question=12) and then reload rutorrent:

~~~
wget -qO ~/rutnginx.sh http://git.io/9vlcyw && bash ~/rutnginx.sh
~~~

### Public Trackers are red / unreachable

In the rutorrent WebUi do this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/ruTorrent%20-%20troubleshooting/publictorrents.png)

