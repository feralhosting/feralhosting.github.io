
Make a torrent
---

To make a .torrent file using command line, execute this command:

~~~
mktorrent -v -p -l 21 -a http://tracker.url -o filename.torrent folder_name
~~~

`-v` is for verbose
`-p` is for private, as in not DHT or PeerExchange
`-l` is for piece length (or size) for the torrent. It's `2^n` bytes, so `-l 21` would create a `2^21 =2MB` piece size (`22=4MB` and `23=8MB`). Try to keep total of `1000` to `2000` pieces. Increase piece size if needed. 
`-a` is for tracker, the tracker URL follows (one is required; additional `-a` commands add backup trackers)
`-o` is for output, the torrent file name follows

**Important note:** The command needs to be all in one line, and quotes must be used around the folder name if it contains spaces.

Example usage
---

If I wanted to make a torrent for What.cd from the data in the `VA - Summer Trance 2009` directory I already have on my server, I would go into the data folder:

~~~
cd private/tranmission/data
~~~
 
Then type the following command:

~~~
mktorrent -v -p -l 21 -a http://tracker.what.cd:34000/xxxXXXxxx/announce -o VA-Summer_Trance_2009.torrent "VA - Summer Trance 2009"
~~~

Please note that you **must** use quotes if the target dir name contains spaces.

**Changing the piece-size**

The default piece-size is `256kb`, which is too small for many files/filepacks. (It results in bloated .torrent files and a lot of extra, unnecessary announce traffic.) The command to change the piece size is '-l XX' (that's a lowercase "L"), according to the following values:

`-l 18` = `256kb` piece-size (for filesizes under `512MB`)
`-l 19` = `512kb` piece-size (for filesizes from `512MB` to `1024MB` / `1GB`)
`-l 20` = `1MB` (`1024kb`) piece-size (for filesizes from `1GB` to `2GB`)
`-l 21` = `2MB` (`2048kb`) piece-size (for filesizes from `2GB` to `4GB`)
`-l 22` = `4MB` (`4096kb`) piece-size (for filesizes from `4GB` to `8GB`)
`-l 23` = `8MB` (`8192kb`) piece-size (for filesizes from `8GB` to `16GB`)
`-l 24` = `16MB` (`16384kb`) piece-size (for filesizes above `16GB`)

So, using the above example, the command to change the piece-size from the default `256kb` to `4MB` would be:

~~~
mktorrent -v -p -l 22 -a http://tracker.what.cd:34000/xxxXXXxxx/announce -o VA-Summer_Trance_2009.torrent "VA - Summer Trance 2009"
~~~

Automate .torrent creation with a script
---

If you do this a lot, it might make sense to use the script below to automate things. To keep things simple, I suggest creating one shell script for each tracker that you are using on a regular basis. To stick with the example above, create a file mk-what-torrent.sh in your home directory, make it executable and open it in the nano editor

~~~
echo -n '' > ~/mk-what-torrent.sh
~~~

~~~
chmod 700 ~/mk-what-torrent.sh
~~~

~~~
nano ~/mk-what-torrent.sh
~~~

Paste this code into the file, changing the tracker's announce URL to what you actually need (also, remove the `-p` flag if your tracker is not a private tracker):

~~~
#!/bin/sh
for i in "$@"; do
         mktorrent -v -p -a announce.url/here -o "$i.torrent" "$i"
done
~~~

Once you have copied the code into the file press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

Then (optionally), edit your `~/.bash_aliases` file

~~~
nano ~/.bash_aliases
~~~

Adding the line

~~~
alias mk-what-torrent='~/mk-what-torrent.sh'
~~~

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm. Now restart bash using this command:

~~~
bash 
~~~

Now our new bash command  `mk-what-torrent` is available for use via the alias. Now you can just navigate anywhere in your filesystem and create torrents for files and folders using wildcards. For example, `mk-what-torrent D*` will create torrent files (for what) of all files and folders starting with D in the current directory. 




