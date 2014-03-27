
You need to SSH top your slot to start/complete this guide. Please see this [Basic SSH Guide](https://www.feralhosting.com/faq/view?question=12)

Now that you've logged in, you need to navigate to your downloads directory. This can be done by 

~~~
cd Path/to/your/downloads/Directory_name
~~~

Don't type the whole name, just the first few letters and press tab. Let autocomplete do the job for you. Now that you're in your downloads directory, the terminal should say something like this: 

~~~
/media/sdb1/home/belligerant/private/rtorrent/data
~~~

**1: To prepare mediainfo:** 
 
~~~
mediainfo filename.avi > filename.txt
~~~

You'll find filename.txt in the folder you ran the command in. Remember, autocomplete is your friend. 

**2: To prepare Screenshots:** 

**Important note:**  You can use [Static ffmpeg builds](https://www.feralhosting.com/faq/view?question=268) if needed.)

~~~
ffmpeg -ss 00:05:00 -vframes 1 -i "Filename.avi" -y -f image2 "screenshot1.png"
ffmpeg -ss 00:10:00 -vframes 1 -i "Filename.avi" -y -f image2 "screenshot2.png"
ffmpeg -ss 00:15:00 -vframes 1 -i "Filename.avi" -y -f image2 "screenshot3.png"
~~~

or

**Important note:** If `mplayer` shows `command not found` you will need to open a ticket and ask staff to install it.

~~~
mplayer "Filename.avi" -nosound -vo png:z=0 -ss 360 -frames 1
mplayer "Filename.avi" -nosound -vo png:z=0 -ss 600 -frames 1
mplayer "Filename.avi" -nosound -vo png:z=0 -ss 900 -frames 1
~~~

(You will need a FTP Client to download the screens and mediainfo.txt)

**Important note:** Folder names with spaces will require that your wrap them in quotes, for example `"folder name"`



