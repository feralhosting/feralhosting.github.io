
OS X Built-in SSH Client using private/public key pair
---

Please see this FAQ for how to SSH to your slot on OS X if you do not know how: [SSH guide basics - OS X(https://www.feralhosting.com/faq/view?question=217)

**Connecting Via SSH using the default password and using private key files.**

**Step 1:** In the terminal app run this command to create our Feral keyfile called `feral_rsa`:

~~~
ssh-keygen -t rsa -f ~/.ssh/feral_rsa -N ''
~~~

![]()

This part of the command allows us to specify the name of the file so that we do not overwrite and existing keyfile:

~~~
-f ~/.ssh/feral_rsa
~~~

This part of the command is to insert a blank passphrase automatically. The space between the two single quotes is empty, meaning the pass phrase will be blank.

~~~
-N ''
~~~
   
**Step 2:** Then run this command to copy the key to your clipboard:

~~~
cat ~/.ssh/feral_rsa.pub | pbcopy
~~~

**Step 3:** Then run this command, where `user-name` is your Feral user-name and `server` is the name of the Feral server your slot is hosted on::

~~~
ssh username@server.feralhosting.com
~~~

**Step 4:** Once logged into your feral slot via SSH run:

~~~
nano -w ~/.ssh/authorized_keys
~~~

**Step 5:** Paste your clipboard contents into the file, ensuring that the contents are all on one line (remove line breaks)

**Step 6:** Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

**Step 7:** Type `exit` to leave SSH session on feral slot

You have now created a keyfile and uploaded the public key to your Feral slot. You can use the keyfile `~/.ssh/feral_rsa` to connect easily now.

Creating SSH tunnels:
---

**Step 1:** In terminal, type, where `user-name` is your Feral user-name and `server` is the name of the Feral server your slot is hosted on:

~~~
ssh -i ~/.ssh/feral_rsa -D 45555 username@server.feralhosting.com
~~~

You can change `45555` to another port number if you wish. Use a port between the range of `6000` to `50000`.

**Step 2:** You have now created an Socks proxy on port `45555`. See instructions later in this article for instructions on how to use this proxy.

Creating SSH tunnels in background
---

You can semi-automate the above process by creating an alias for the tunnel command and setting it up to run in a screen session in the background

**Step 1:** in terminal type:

~~~
nano ~/.bash_profile
~~~

**Step 2:** In the resulting  editor window type, where `user-name` is your Feral user-name and `server` is the name of the Feral server your slot is hosted on:

~~~
alias feraltun="screen ssh -i ~/.ssh/feral_rsa -D 45555 username@server.feralhosting.com"
~~~

You can change `45555` to another port number if you wish. Use a port between the range of `6000` to `50000`.

**Step 3:** Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

To use your new alias:
---

**Step 1:** Start a new terminal session (type exit to leave the old one if still open)

**Step 2:** Type:

~~~
feraltun
~~~

Your SSH tunnel is now active

**3:** Then press and hold `CTRL` and `a` then press `d` to detach from the screen. This leaves it running in the background.

**4:** You can now close terminal and use your tunnel



