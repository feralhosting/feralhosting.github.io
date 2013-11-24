
Connecting with Terminal
---

Mac OS X comes with its own implementation of OpenSSH, so you don't need to install any third-party software to take advantage of the extra security SSH offers — just open a terminal window and jump in.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/macterminal1.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/macterminal2.png)

If you haven't already created a dock icon for "Terminal" then  go to the Applications folder, then Utilities from within that. Terminal is in the Utilities folder. Just drag it on to the Dock, and it'll make a permanent Dock icon.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/terminalicon.png)

OS X Built-in SSH Client
---

When you open the terminal you will see something like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SSH/SSH%20guide%20basics%20-%20OS%20X/3.png)

Now we enter the SSH command to connect to the slot, where `username` is your Feral username and `server` is the name of the server you wish to SSH into:

~~~
ssh username@server.feralhosting.com
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SSH/SSH%20guide%20basics%20-%20OS%20X/4.png)

If this is the first time connecting to this host you will see something like this.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SSH/SSH%20guide%20basics%20-%20OS%20X/5.png)

Type `yes` to save the host's key.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SSH/SSH%20guide%20basics%20-%20OS%20X/6.png)

Now enter your Feral SSH/SFTP password at the prompt found on your slot details page for the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

**Do not type it in** — copy it (be careful not too introduce extra white spaces) paste it by pressing: 

**command-v** or a **middle-click on a 3-button mouse** to paste it in.

**There will be no visual response when you paste in your password** — this is a security measure so that your password cannot be stolen by someone looking over your shoulder. Simply paste it and press **enter** to send the password to the server.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SSH/SSH%20guide%20basics%20-%20OS%20X/7.png)

At this point you should be logged into your Feral server and ready to execute commands in shell.

After you have saved the host key and use the command shown in this FAQ it will look like this when connecting.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SSH/SSH%20guide%20basics%20-%20OS%20X/8.png)

You have now successfully connected to your slot via SSH using terminal on OS X.



