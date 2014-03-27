
This guide is for people who download data from one tracker and wish to upload it to another tracker, all on their Feral box.

**Step 1:** Locate your data:

Delugestores it's data in the following folder:

~~~
~/private/deluge/data
~~~

rTorrent stores it's data in the following folder:

~~~
~/private/rtorrent/data
~~~

Transmission stores it's data in the following folder:

~~~
~/private/tranmission/data
~~~

**Step 2: ** When you log in with putty, switch to that folder, by typing:

For Deluge:

~~~
cd ~/private/deluge/data
~~~

For rtorrent:

~~~
cd ~/private/rtorrent/data
~~~

For Transmission:

~~~
cd ~/private/transmission/data
~~~

**Step 3: ** You can view the contents of that folder with the command:

~~~
ls
~~~

**Step 4: ** Once your data is finished downloading, you can then create a new .torrent file using this command:

~~~
mktorrent -l 21 -p -v -a http://tracker.url -o filename.torrent  "folder_name/"
~~~

Example:

(this command is all one line, no matter if it wraps in putty or on here)

~~~
mktorrent -l 21 -p -v -a http://tracker.what.cd:34000/your_secret_code/announce -o VA-SomeDanceAlbum.torrent "VA - Some Dance Album/"
~~~

Please substitute things with your corresponding file and folder names. If the folder contains spaces and/or special characters like parentheses, use quotes around the name, just like in the example above. You can of course choose any name you want for the .torrent file. I know that What.cd doesn't like spaces in the .torrent file name, so I omitted spaces in the example above.

The command will run and display a summary on in putty when it's done. The .torrent file will be in the same folder where you created it, in this case the data folder:
`~/private/rtorrent/data` or `~/private/transmission/data`

You can now download the .torrent file with filezilla to your PC, and then upload it to the tracker website. When the tracker generates a new .torrent file, download it to your PC, and load it via the wtorrent web gui. Or you can upload it to the server with filezilla, and drop it in the watch folder:
`~/private/rtorrent/watch` or `~/private/tranmission/watch`

It will automatically load in rtorrent or Transmission, do a hash check, and start seeding to the new tracker.



