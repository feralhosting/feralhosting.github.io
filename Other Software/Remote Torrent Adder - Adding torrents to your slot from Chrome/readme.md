
**1:** Start by installing the extension from here:

[Remote torrent adder](https://chrome.google.com/webstore/detail/oabphaconndgibllomdcjbfdghcmenci)

**2:** Open the settings for the extension.

**3:** Fill in the data in the form under the WebUI tab accordingly:

### Rutorrent

**Client:** ruTorrent WebUI from the drop down menu

**Host:** `server.feralhosting.com` For example: `aphrodite.feralhosting.com`

**Port:** leave blank

**SSL** Checked if you are using SSL

**Username:** Your `Feral Username`

**Password:** Your `rutorrent Web Gui Password` (as shown on your Slot Details page for rutorrent)

**Important note:** on your username and password: If you have changed your default rutorrent Web Gui config using the [Password Protect Your WWW Page(s)](https://www.feralhosting.com/faq/view?question=22) guide you will need to use the **Username** and **Password** you created there.

**Relative Path SSL:** `/username/rutorrent/`

**Label:** [Nothing required]

**Directory:** This is the directory where your torrent **data** will be stored, you will need the full path to this folder.
To get this you have to SSH into your box, then navigate to your:

Paste the following command into the terminal: 

~~~
ls -d $HOME/private/rtorrent/data
~~~

The output should look something like this:

~~~
/media/DiskID/home/username/private/rtorrent/data/
~~~

If you press a torrent link now it should load the .torrent directly into rtorrent
on your slot.

You will get an error like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/Remote%20Torrent%20Adder%20-%20Adding%20torrents%20to%20your%20slot%20from%20Chrome/error.png)

But it stills works.

### Still having issues? read this section

If you are having issues you can try these server settings instead:

**Important note:** If you force redirection to https this URL format **will not work** unless you accept the cert in Chrome first every session. Follow these steps.

1: You will need to visit the `https://username.server.feralhosting.com` URL in a Chrome and accept the cert for this session.

2: You will need to check `SSL` in the remote torrent adder options since https is being forced.

These settings will work if https redirection is not forced, or you have visited the https URL for this session

**Host:** `username.server.feralhosting.com` For example: `peterpan.aphrodite.feralhosting.com`

**Port:** leave blank

**Relative Path:** `/rutorrent/`

**SSL:** Checked if https is being forced, otherwise leave unchecked.

### Client: Deluge

**Host:** server.feralhosting.com

**Port:** leave blank

**Username:** Your Feral username

**Password:** You Deluge Web Gui password as listed on your Slot Details page.

**Relative path:**

~~~
/username/deluge
~~~

### Notes

You can also let the option of downloading on your torrent only be available by right-clicking
the torrent link by deselecting the "clicks on links" in the "link catching" tab.
(I'd recommend doing this so you don't download all kinds of rubbish onto your slot)

You will also override downloading this on your box by holding down Alt+Ctrl+Shift
while clicking the link.




