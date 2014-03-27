Basic screen switches
---

There are many more Screen options and switches. To read the built-in Linux manual for Screen, please type this in the shell: 

~~~
man screen
~~~

(While reading the man pages, you can move forward by a full page with the Space bar, or line by line with the Enter key.)

~~~
screen
~~~

Run a new screen session. It opens a new session, with just a bash prompt.

~~~
screen program_name
~~~

Run a new screen session and launches the program you specify.

~~~
screen -t some_title
~~~

Run a new screen session, with the title `some_title`.

~~~
screen -S session_name
~~~

Run a new screen session and specify a meaningful name for the session.

~~~
screen -S session_name program_name
~~~

Run a new screen session and specify a meaningful name for the session and launch some program at the same time. 

~~~
screen -r
~~~

Reattach to a previously detached session (if there is more than one detached screen running, it will display a list).

~~~
screen -ls
~~~

It will display a list of screen sessions running.

~~~
exit
~~~

When typed inside a screen, it will terminate the current screen session.

Nested Screen Sessions
---

It's possible to get stuck in a nested screen session. A common scenario: you start an SSH session from within a screen session. Within the SSH session, you start screen. By default, the outer screen session that was launched first responds to `C-a` commands. To send a command to the inner screen session, use `C-a a`, followed by your command. 

For example:

~~~
C-a a d
~~~

Detaches the inner screen session.
 
~~~
C-a a K
~~~

Kills the inner screen session. 

Usage Examples
---

~~~
screen -S my_htop htop
~~~

This will launch htop in a screen with the session being named `my_htop`, so if you need to reattach to it with `screen -r`, it will be more obvious which one it is.

~~~
screen -R my_htop
~~~

If you used the -S switch to name the session, you can then reattach to it by specifying the session name after the -R switch. Useful if you have several sessions of screen running detached.

![](https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Screen%20Command%20-%20a%20Basic%20Guide/1.jpg)

Key Bindings while running screen (case sensitive!)
---

~~~
Ctrl-a c
~~~

Create a new window and switch to it.

~~~
Ctrl-a d
~~~

detach from the current screen session, letting it run in the background.

~~~
Ctrl-a k
~~~

Kill the current window, after confirmation.

~~~
Ctrl-A  DD
~~~

have screen detach and log you out. 

~~~
Ctrl-a Ctrl-a
~~~

Switch to other running screen window

~~~
Ctrl-a n
~~~

Go to the next window.

~~~
Ctrl-a p
~~~

Go to the previous window.

~~~
Ctrl-a w
~~~

Show a list of windows.

~~~
Ctrl-a S
~~~

Split the current window in two.

~~~
Ctrl-a Q
~~~

Close split screen. (It will kill the split section currently **not** in focus)

~~~
Ctrl-a TAB
~~~

Move between split sections of the screen.

~~~
Ctrl-a A
~~~

Give the the current window a name.

~~~
Ctrl-a "
~~~

List all windows - move around to change the window with the arrow keys.

~~~
Ctrl-a F
~~~

Resize the window to the current region size.

~~~
Ctrl-a ESC
~~~
 
Enter scrollback mode. Use your arrow keys to move up and down inside your screen session. 

Usage Examples - Split Screen
---

To run two screen sessions in a split window, first start a screen with

~~~
screen
~~~

(You can give it a session name with `-S` if you want)

Then you should see a bash prompt.  The session name by default is `bash`.

![](https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Screen%20Command%20-%20a%20Basic%20Guide/2.jpg)

Start another screen session inside the first screen, with

~~~
screen
~~~

(Again, you can give it a session name with `-S` if you want)

You can now switch between the two active screens with `Ctrl-a Ctrl-a` or `Ctrl-a n`.
You can view a list of opened sessions with `Ctrl-a w`.

![](https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Screen%20Command%20-%20a%20Basic%20Guide/3.jpg)

Now let's split one of those screens into a split-window with `Ctrl-a S`. 

![](https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Screen%20Command%20-%20a%20Basic%20Guide/4.jpg)

You can move between the halves with `Ctrl-a TAB`. The bottom half is blank for now, and you cannot type in it.
While in the bottom half, use `Ctrl-a n`to bring up one of the screen sessions we launched earlier. You should now see a bash prompt in each half.

![](https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Screen%20Command%20-%20a%20Basic%20Guide/5.jpg)

You can now execute separate commands in each half.

One good use could be to run the space check with a `watch` command in one half, and your `htop`, or anything you want to keep an eye on. See the tip below for the watch command example.

![](https://raw.githubusercontent.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Linux%20Command-Line%20-%20Advanced/Screen%20Command%20-%20a%20Basic%20Guide/6.jpg)

Tip
---

**1:** To use the watch command to check your space, just type this command:

~~~
 watch -n 60 du ~/ -s --si
~~~

It will execute the command you specify, refreshing it on the screen, with an interval of 60 seconds.

**2:** If you create a `.screenrc` file in your home directory, you can use the following command in the `.screenrc` file to create a status bar that will be displayed at the bottom of the screen session (Please see the screenshots above). It will also display a list of active sessions, similar to `Ctrl-a w`:

~~~
# An alternative hardstatus to display a bar at the bottom listing the
# windownames and highlighting the current windowname in blue. (This is only
# enabled if there is no hardstatus setting for your terminal)
hardstatus on
hardstatus alwayslastline
hardstatus string "%{.bW}%-w%{.rW}%n %t%{-}%+w %=%{..G} %H %{..Y} %m/%d %C%a "
altscreen on
caption always
caption string "%= %-w%L>%{= BW}%n*%t%{-}%52<%+w %L="
defscrollback 30000
startup_message off
defsilence on
~~~



