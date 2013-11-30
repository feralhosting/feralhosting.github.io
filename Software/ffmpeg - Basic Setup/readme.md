
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

ffmpeg installation (static)
---

FFmpeg is already installed on your slots and available for you to use, do this command in SSH to see:

~~~
ffmpeg
~~~

If you require and alternative or updated build then use this FAQ to install a pre compiled statically linked version.

**Important note:** `ffmpeg` has a directory structure that does not really fit in with other FAQs so it gets to use a unique location and `PATH`. It will be installed to `~/ffmpeg` in this FAQ:

We will use the statically linked, pre-compiled version of `ffmepg` since it makes this a lot easier. All versions are from [http://johnvansickle.com/ffmpeg/](http://johnvansickle.com/ffmpeg/)

Use these first two commands to create to do some pre requisite tasks:

~~~
mkdir -p ~/programs
[[][/[][ ! "$(grep '~/ffmpeg' ~/.bashrc)" ]] && echo 'export PATH=~/ffmpeg:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Install the program using these commands:

~~~
wget -qO ~/ffmpeg.tar.gz http://johnvansickle.com/ffmpeg/releases/ffmpeg-2.0.1-64bit-static.tar.bz2
tar xf ~/ffmpeg.tar.gz
cp ~/ffmpeg-2.0.1-64bit-static/. ~/ffmpeg
chmod 700 ~/ffmpeg/ffmpeg  ~/ffmpeg/ffprobe  ~/ffmpeg/ffmpeg-10bit
rm -f ~/ffmpeg.tar.gz ~/ffmpeg-2.0.1-64bit-static
~~~

Check your version:

~~~
ffmpeg -version
~~~

The path to the binary will be:

~~~
~/ffmpeg/ffmpeg
~~~



