
Transmission can be installed from the [**Install Software** link in your Manager](https://www.feralhosting.com/manager/) for the slot you wish to use it on.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Transmission%20and%20Transmission%20Remote%20GUI/transslotdetail.png)

If you wish to set up an RPC client you will need to take note of your server name (in green), it's also listed in the menu.

### Remote GUI Client for Transmission

Transmisson Remote GUI is a stand-alone client that runs on your computer and allows you to control your instance of Transmission running on the server remotely. It supports the following platforms: Windows, Mac, and Linux

To start, [download the latest version](http://code.google.com/p/transmisson-remote-gui/) then follow the configuration instructions below.

**Important note:** The similarly named [transmission-remote-dotnet](http://code.google.com/p/transmission-remote-dotnet/) does not work with our installations.

### Configuring Remote GUI

Opening the client you should see something similar to the following image. Click the down arrow by the connection symbol to open the menu:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Transmission%20and%20Transmission%20Remote%20GUI/1.png)

Select "New connection...":

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Transmission%20and%20Transmission%20Remote%20GUI/2.png)

You will then be presented with the "Connection options" window like so:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Transmission%20and%20Transmission%20Remote%20GUI/3.png)

We will need to fill it with information similar to below. If you want the RPC connection to be unsecured then use something similar to:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Transmission%20and%20Transmission%20Remote%20GUI/4.png)

For a secure connection (always recommended) then please select SSL and use the following port:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/Transmission%20and%20Transmission%20Remote%20GUI/5.png)

**Connection:** You may choose a name or leave it blank for it to be automatically filled by the `Remote host` field.

**Remote host:** Enter the host `transmission.username.server.feralhosting.com` replacing `username` with your Feral username in lowercase and `server` with your server name, for example:

~~~
transmission.peterpan.aphrodite.feralhosting.com
~~~

**Port:** If you check `Use SSL` then use port `443` otherwise, port `80`. SSL will encrypt your connection and is recommended.

**User name:** Your Feral username.

**Password:** As listed under the Transmission section of your "Slot Detail" page.

Once filled in, click OK and it will save then connect to the profile.

### Troubleshooting Transmission

If Transmission is acting abnormally e.g., has become unresponsive then a restart is in order

If transmission is acting abnormally (e.g., has become unresponsive or frozen) you will need to restart it. Log into your slot via [SSH](https://www.feralhosting.com/faq/view?question=12), and run this command:

~~~
killall -9  -u $(whoami) transmission-daemon
~~~

It will then be restart automatically in the next 5 minutes.

If the problem persists or Transmission is not restarted then please open a support ticket.

### What version of Transmission am I running?

Login to the Web Gui, press the "gears" button on the bottom left hand corner and select "About". You will then be presented with a dialogue showing the version number.



