
If you are finding that your FTP speeds have become slower than usual, there is a workaround that can be applied by increasing the number of concurrent connections that your FTP client will use when connecting to your Feral box.

### In Filezilla (and similar clients)

Locate your Site Manager and go to your Feral box entry. Click on the **Transfer Settings** tab and increase this number to 7. Experiment with the number and your speeds should increase somewhat.

These are parallel (concurrent) downloads and not multi segmented. Filezilla does not support multiple segments. Please see this FAQ for more info [What is multisegmented downloading - how does it help](https://www.feralhosting.com/faq/view?question=182)

### Bitkinex multi segmented downloads

[BitKinex 3.2.3 (windows platform)](http://www.bitkinex.com/ftp/client/bitkinex323.exe) you can use up to 50 segments, locate your feral server entry in the Control window. Right-click on the feral server and select:

`Properties > Connections > Total number of connections used by this data source:`

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/What%20to%20do%20if%20FTP%20speeds%20are%20slow/bit-1.png)
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/What%20to%20do%20if%20FTP%20speeds%20are%20slow/bit-2.png)
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/What%20to%20do%20if%20FTP%20speeds%20are%20slow/bit-3.png)

You can set this individually for each connection instead, to do this right click on the relevant connection go to it's properties. then:

Increase this number to `50` connections (default is `5` connections, you can experiment with this number later). First uncheck in the same window: `Inherit properties from the parent node (SFTP/SSH)`, otherwise the options stay greyed out.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/What%20to%20do%20if%20FTP%20speeds%20are%20slow/bit-4.png)
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/What%20to%20do%20if%20FTP%20speeds%20are%20slow/bit-5.png)

### In CuteFTP Pro

You can use Multi-Part. When using this mode, the file you are downloading is split into several chunks in the background which are then transferred in several threads simultaneously, and then reassembled, once complete, on your local computer. This is the fastest method of transferring large files.

Go to `Tools > Global Options > Transfer > When selecting MAX in multi-part transfer, use...`

When selecting a file to download, right-click on `File > Download Advanced > Multi-part Download > MAX (7 parts)`

### LFTP 

The Windows and OSX versions are port from the Unix version. Once you have `lftp` installed for your platform you can use the Unix section below to run `lftp` via a terminal like Putty or terminal in OSX

Once you have `lftp` installed continue with the unix section of this FAQ for LFTP.

### In lftp (Windows via cygwin)

For Windows users to install lftp - [Cygwin and lftp on Windows ](https://www.feralhosting.com/faq/view?question=235)

### In lftp (OSX via Homebreww)

For Mac users to install lftp - [OSX - Homebrew](https://www.feralhosting.com/faq/view?question=262)

### In lftp (Unix)

The first thing you will do is open your terminal program and type this command:

~~~
lftp sftp://user-name@server.feralhosting.com
~~~

Where user-name is your Feral username and server is the name of the Feral server your lost is hosted on, for example:

~~~
lftp sftp://peterpan@aphrodite.feralhosting.com
~~~

At this point you will be asked for your Feral FTP / SFTP / SSH password. Enter it now then press enter.

If you connect successfully then can do this command to save your connection and password for future use:

~~~
set bmk:save-passwords true
bookmark add Feral
~~~

Now you can navigate your slot using `lftp` just like normal:

~~~
cd ~/private/rtorrent/data
~~~

Will put you inside this folder.

### lftp usage

You can use the command `pget` to transfer a file with several connections (specify `-n maxcon`). You can also use `mirror` to transfer a folder but specify:

~~~
--use-pget[-n=N]
~~~

or 

~~~
--parallel[=N]
~~~

The former uses `pget` to transfer each file, the latter specifies to transfer multiple files at once. You can set whatever default combination you like in your `~/.lftp/rc` file, such as the following:

~~~
set pget:default-n 10
set mirror:use-pget-n 10
set mirror:parallel-transfer-count 2
set mirror:parallel-directories true
~~~

### [Progressive Downloader for OSX](http://www.macpsd.net/)

You can max out your connection with progressive downloader as an alternative to FTP by playing around with the thread count in `Progressive downloader -> Preferences -> Maximum thread count`: try 10-15. I was having problems with slow FTP speeds but after some experimenting this solution worked for me and i'm now able to max out my connection with no problems. For this to work you will need to put your public_html folder to use, you can do that by following the guide in the wiki located [here](https://www.feralhosting.com/faq/view?question=20)

### aria2c

1: Follow this FAQ - [Putting your WWW folder to use](https://www.feralhosting.com/faq/view?question=20)

2: Use this FAQ - [aria2c ](https://www.feralhosting.com/faq/view?question=236)

For Mac users to install aria2c - [OSX - Homebrew](https://www.feralhosting.com/faq/view?question=262)

While this FAQ appears Windows only, the commands and set-up of aria2c work exactly the same across platforms.

### Further Problems

If you continue to have problems then it is likely out of our direct control and down to network issues. We will need to collect data about your connection: 

** Bug in lftp's mirror-over-sftp **

If you use sftp with lftp and "mirror" freezes, it's a known bug in lftp-4.4, upgrade to version >= 4.4.8 
or downgrade to 4.3 - discussion and fix is [here](https://github.com/lavv17/lftp/issues/39)



