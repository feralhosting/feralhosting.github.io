~~~
Mac Users that need a RSS download scheduler, check out [**Automatic**](http://codingcurious.com/automatic/)
~~~

**Step 1:**

Install uTorrent. Open preferences with **ctrl + p**. Under **Directories** set **Store .torrents in** to your desired torrent directory (remember this directory for later).

Under **UI Settings** select **Don't Start Download Automatically**.

**Optional:**

Under **Scheduler** — **Enable Scheduler**. Click your mouse and run over all the boxes; repeat this until all boxes are white.

Refer to [uTorrent documentation](http://www.utorrent.com/documentation/rss/) for setting up RSS in uTorrent.

**Step 2:**

Install CuteFTP Pro and Set up your FTP connection to your Feral box.

Press **ctrl + F9** to open the **Local Monitor** dialog. Press **Next**.

**Monitor the following local path** — the directory you set uTorrent to save .torrents in.

**Upload to the following remote path**

~~~
 /home/**USERNAME**/private/rtorrent/watch
~~~

You can substitute above for transmission or any other client that uses watch folders. Click **Next** and leave everything else default.

With everything set up, uTorrent will download a .torrent from RSS and CuteFTP will see the new .torrent and upload it to your watch directory on your Feral box.

**CuteFTP Mac Professional does not have a folder monitoring feature (yet), however [[b]Yummy FTP**](http://www.yummysoftware.com/download) does.[/b]

**Step 1:**

Inside Yummy FTP, connect with your Feral FTP login details.

**Step 2:**

Navigate to rtorrent's or transmission's folder, right click on the **watch** folder and click **Save as FTP Watcher**

**Step 3:**

On the Finder dialogue that opens, choose the folder where your torrents are saved automatically and click Save.

**Step 4:**

Now open a new Finder, navigate to that same folder, look for the **Watcher** file and double click it to start monitoring that folder.


---
**Thanks to user fiendskull9 for testing this setup.**