
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

ffmpeg installation (static)
---

FFmpeg is already installed on your slots and available for you to use, do this command in SSH to see:

~~~
ffmpeg -v
~~~

If you require and alternative or updated build then use this FAQ to install a pre compiled statically linked version. We will use the statically linked, pre-compiled version of `ffmepg` from [http://johnvansickle.com/ffmpeg/](http://johnvansickle.com/ffmpeg/)

Use this command to create the `~/bin` directory and reload your shell for this change to take effect.

~~~
mkdir -p ~/bin && bash
~~~

**1:** Install the program using these commands:

~~~
wget -qO ~/ffmpeg.tar.gz http://johnvansickle.com/ffmpeg/releases/ffmpeg-2.3.3-64bit-static.tar.bz2
tar xf ~/ffmpeg.tar.gz && cd && rm -rf ffmpeg-2.3.3-64bit-static/{manpages,presets,readme.txt}
cp ~/ffmpeg-2.3.3-64bit-static/* ~/bin
chmod 700 ~/bin/{ffmpeg,ffprobe,ffmpeg-10bit,qt-faststart}
cd && rm -rf ffmpeg{.tar.gz,-2.3.3-64bit-static}
~~~

**2:** Check your version:

~~~
ffmpeg -version
~~~

The path to the binary will be:

~~~
~/bin/ffmpeg
~~~



