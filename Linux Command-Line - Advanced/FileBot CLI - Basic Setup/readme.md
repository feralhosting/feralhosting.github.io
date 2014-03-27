
**Important note:** You will need to have Java install to use this program - [Java 1.7](https://www.feralhosting.com/faq/view?question=183)

Filebot basic installation to use the command line options (no GUI) on your Feral slot.

FileBot is the ultimate tool for organizing and renaming your movies, tv shows or anime, and music well as downloading subtitles and artwork. It's smart and just works.

Powerful and full-featured cmdline interface and scripting interface for any kind of automation

[Filebot Command Line](http://www.filebot.net/cli.html)

FileBot CLI setup
---

The download, unpacking and editing.

~~~
wget -qO ~/filebot.zip http://downloads.sourceforge.net/project/filebot/filebot/FileBot_4.0/FileBot_4.0-portable.zip
unzip -qo ~/filebot.zip -d ~/filebot && rm -f ~/filebot.zip
~~~

Now to run filebot you would do this, which will also show you the `-help` page to:

FileBot CLI - usage
---

~~~
~/filebot/filebot.sh
~~~

~~~
~/filebot/bin/filebot.sh -rename "$HOME/path/to/episodes"
~~~

Use `" "` around paths. Use `$HOME` in paths instead of `~`. Filebot gets confused about the `~`

Please refer to this page: [Filebot Command Line](http://www.filebot.net/cli.html) for more options.



