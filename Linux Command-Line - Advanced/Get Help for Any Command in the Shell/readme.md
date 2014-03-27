
There are a couple of different ways to get help with a command in Linux. This will be a brief overview of each method. You are encouraged to [Google the internet](http://www.google.com) if you require more in-depth information on any command. There are some great resources out there, that we use ourselves, either for daily use, or for writing these FAQ's.

For help on connecting to the shell on your slot, please see [this FAQ](https://www.feralhosting.com/faq/view?question=12).

The three ways of getting help for a command are:

The Command Itself - command run without any options usually displays help on its usage
The `-h` (or `--help`) switch - a switch that displays a quick and dirty version of help for the command
The `man` (manual) command - the extensive and very detailed manual that is built into Linux.


**The Command Itself**

Sometimes just running the command itself, without any switches or options, will give you information on how to use it. One example is the `unrar` command. When executed by itself in the shell, it gives the following output:

~~~
UNRAR 3.90 freeware      Copyright (c) 1993-2009 Alexander Roshal

Usage:     unrar <command> -<switch 1> -<switch N> <archive> <files...>
               <@listfiles...> <path_to_extract\>

<Commands>
  e             Extract files to current directory
  l[t,b]        List archive [technical,bare]
  p             Print file to stdout
  t             Test archive files
  v[t,b]        Verbosely list archive [technical,bare]
  x             Extract files with full path
~~~

(I have pasted only part of the output here, there are more options displayed.)

For more information about the `unrar` command, please see [this FAQ](https://www.feralhosting.com/heron/faq/view?question=36).

**Important note**: If the output scrolls off the screen before you have a chance to read it, you can simply scroll up, or use the `more` command to make it stop at each page-full:

~~~
unrar | more
~~~

`|` - a pipe command that helps pass the output of one command to another
more - a program that displays output one screen at a time
unrar - the program whose output we are passing to more

The output will stop when it reaches the bottom of your screen, and display a `--More--` prompt at the bottom. Use the `Spacebar` to go forward a full screen, or use `Enter key` to go forward one line at a time. Arrow keys also may work for up and down movement. Press the `Q key` to get back to the prompt without further scrolling.

### The help (-h) Switch

Almost all commands in Linux share a common switch for getting help for the command: `-h` (or `--help`). This is an agreed-upon standard by all program developers and should be present in each command. If one form does not work, try the other variant.

Here is an example, using the `mktorrent` command:

~~~
mktorrent -h
~~~

Will give something like:

~~~
mktorrent 1.0 (c) 2007, 2009 Emil Renner Berthing

Usage: mktorrent [OPTIONS] <target directory or filename>

Options:
-a <url>[,<url>]* : specify the full announce URLs
                    at least one is required
                    additional -a adds backup trackers
-c <comment>      : add a comment to the metainfo
-d                : don't write the creation date
-h                : show this help screen
-l <n>            : set the piece length to 2^n bytes,
                    default is 18, that is 2^18 = 256kb
-n <name>         : set the name of the torrent,
                    default is the basename of the target
-o <filename>     : set the path and filename of the created file
                    default is <name>.torrent
-p                : set the private flag
-v                : be verbose
~~~

(I have trimmed some of the output to save space here.)

As you can see, the help output gives you the syntax of the command (the order of options and switches in the command), as well as all of the options and switches that can be used when executing the command. For more info on using the `mktorrent` command, please see [this FAQ page](https://www.feralhosting.com/faq/view?question=71).

### The `man` Command

Linux includes a huge depository of help called `man` (short for `manual`). It is a way to store a software manuals on the system itself, without having to go to the web to locate the developer page. It covers nearly all of the common Linux commands.

To use the man command, just prefix it to the command you want to know more about:

~~~
man rtorrent
~~~

To navigate the man pages, the controls are similar to the `more` command from above:
 
Enter key - move forward by a single line
Space bar - move forward by a whole screen
Arrow keys - move up and down freely
Pg Up + Pg Down - move up and down by whole screen freely
Q key - quit the man session and go back to the prompt

Please go here for more information about using rtorrent in [this FAQ](https://www.feralhosting.com/faq/view?question=2).

I hope that this introduction will give you the skills and confidence to navigate the shell in Linux more comfortably.



