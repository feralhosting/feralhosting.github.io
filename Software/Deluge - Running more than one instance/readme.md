
How to run multiple instances of Deluge on a Feral Slot
---

**Important note:** This is a community supported FAQ. Feralhosting does not officially support this document.

Please seek help in the feralhosting.com IRC channel if you need assistance. Many Feral customers volunteer their time to create and support these FAQs. Please be considerate of their time -- they will help when they can, but are not always available.

These instructions are intended to be run over [SSH](https://www.feralhosting.com/faq/view?question=12). You may be able to modify them to work under another method, if you desire.

Make a copy of the existing config:
---

**Copy/Paste exactly as given**

~~~
cp -r ~/.config/deluge ~/.config/deluge2
~~~

Clean up the config:
---

**Copy/Paste exactly as given**

~~~
# Delete the .pid file
find ~/.config/deluge2 -name deluged.pid -exec rm '{}' \;

# Delete the torrents already added
find ~/.config/deluge2/state -name \*torrent -exec rm '{}' \;

# Update the locations in the config
sed -i 's|/private/deluge/|/private/deluge2/|g' ~/.config/deluge2/core.conf*
~~~

Update the port in use:
---

**Copy/Paste exactly as given**

~~~
OLD_PORT=$(grep daemon_port ~/.config/deluge2/core.conf | awk '{print $2}' | cut -d\,  -f1)
NEW_PORT=$((RANDOM%10000+40000))
sed -i "s|${OLD_PORT}|${NEW_PORT}|g" ~/.config/deluge2/core.conf*
~~~

Retrieve important information:
---

**Copy/Paste exactly as given**

~~~
PASSWORD=$(cat ~/.config/deluge2/auth | grep $(whoami) | cut -d\:  -f2)
echo "Your deluge web interface connection information is as follows:"; echo "HOST=localhost"; echo "PORT=${NEW_PORT}"; echo "USERNAME=$(whoami)"; echo "PASSWORD=${PASSWORD}"; echo "###";

echo "Your deluge thin client connection information is as follows:"; echo "HOST=$(hostname)"; echo "PORT=${NEW_PORT}"; echo "USERNAME=$(whoami)"; echo "PASSWORD=${PASSWORD}";
~~~

Start new instance:
---

**Ignore any of the following errors:**

`ERROR    14:26:39 torrentmanager:372 Unable to add torrent!`

**Copy/Paste exactly as given**

~~~
deluged -c ~/.config/deluge2/
~~~

If, and **only if**, you get the error:

`ERROR    15:04:01 rpcserver:375 Couldn't listen on any:52055: Errno 98 Address already in use.` re-run the "Update the port in use" and "Retrieve important information" sections. You may safely run these commands as many times as needed.

Create the needed folders:
---

**Copy/Paste exactly as given**

~~~
mkdir -p ~/private/deluge2/{completed,data,torrents,watch}
~~~

To connect to your new instance:
---

### To add to the web interface:

Load up your Deluge web interface

Connection Manager -> Add. Fill in the details with the details above for the web interface.

### To add to the [thin](https://www.feralhosting.com/faq/view?question=76) client:

Load up your Deluge thin client

Connection Manager -> Add. Fill in the details with the details above for the web interface.

Important caveats 
---

1) If you run the command ‘killall -9 deluged’, *all* instance of deluge will be killed and need to be restarted.

2) If you want this instance of deluge to restart automatically if and when the server reboots, you can add a ‘crontab’ entry to do that:

~~~
crontab -e
~~~

This will open up your crontab. At the bottom of the file, add the following:

~~~
@reboot /usr/local/bin/deluged -c ${HOME}/.config/deluge2
~~~




