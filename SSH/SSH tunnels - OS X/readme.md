
OS X Built-in SSH Client using private/public key pair
---

SSH is the built-in OS X SSH client and is very powerful and simple to use if you follow the instructions in this guide.

**Connecting Via SSH using the default password and using private key files.**

**1:** In terminal on mac run

~~~
ssh-keygen -t rsa
~~~

- enter for default file save location
- enter when prompted for passphrase (no passphrase)
   
**2:** Then run:

~~~
cat ~/.ssh/id_rsa.pub | pbcopy
~~~

to copy the key to your clipboard

**3:** Then run:

**Important note:** This is NOT a number 1. It is a non-capitalised letter `L`

~~~
ssh -l username server.feralhosting.com
~~~

For example:

~~~
ssh -l peterpan aphrodite.feralhosting.com
~~~

Replace `username` and  `server` with your own details provided to by Feral. Use the SSH password from your feral Manager Slot details page for the relevant slot.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

**4:** Once logged into your feral slot via ssh run:

~~~
nano ~/.ssh/authorized_keys
~~~

**5:** Paste your clipboard contents into the file, ensuring that the contents are all on one line (remove line breaks)
**6:** Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.
**7:** Type `exit` to leave ssh session on feral slot

Creating SSH tunnels:
---

**1:** In terminal, type 

~~~
ssh -D 45555 -l username server.feralhosting.com
~~~

- replace `username` and `server` with your own details.
- you can change `45555` to another port number if you wish. Use a port between the range of `6000` to `50000`.

**2:** You have now created an Socks proxy on port 55555. See instructions later in this article for instructions on how to use this proxy.

Creating SSH tunnels in background
---

You can semi-automate the above process by creating an alias for the tunnel command and setting it up to run in a screen session in the background

**1:** in terminal type 

~~~
nano ~/.bash_profile
~~~

**2:** In the resulting  editor window type 

~~~
alias feraltun="screen ssh -D 55555 -l username server.feralhosting.com"
~~~

- replace `username` and `server` with your own details.
- you can change `45555` to another port number if you wish. Use a port between the range of `6000` to `50000`.

**3:** Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

**To use your new alias:**

**1:** Start a new terminal session (type exit to leave the old one if still open)

**2:** Type:

~~~
feraltun
~~~
 
- your SSH tunnel is now active

**3:** Then press and hold `CTRL` and `a` then press `d` to detach from the screen. This leaves it running in the background.

**4:** You can now close terminal and use your tunnel

**Important note:** If you have any questions about this procedure for OS X or suggestions on improving the instructions, please contact liriel in IRC.



