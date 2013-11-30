
### Installing [homebrew](http://brew.sh/) on OS X Mavericks

This is quite a simple thing to do and once you have done it you will be able to install some useful apps for use with your slot.

The first thing you need to do is open your terminal:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/macterminal1.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/macterminal2.png)

If you haven't already created a dock icon for "Terminal", open your Macintosh HD and go to the Applications folder, then Utilities from within that. Terminal is in the Utilities folder. Just drag it on to the Dock, and it'll make a permanent Dock icon.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/terminalicon.png)

### Installing homebrew

In your terminal you need yo paste this command and then press enter:

~~~
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
~~~

This will begin the homebrew installation procedure:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew1.png)

You will need to follow the prompts from the script. Here you will need to press `enter` to continue.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew2.png)

Enter your user's password to allow the software to be installed. It should be your login password for this device.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew3.png)

You may see this notice if you have not done this or something similar before. You will need to accept the installation. Click "Install" to continue:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew4.png)

After you click "Install" you will see the software will be downloaded and installed:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew5.png)

Click "Done" whe it has finished to continue with the homebrew installation:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew6.png)

Now you should be able to continue with the homebrew installation script to actually install homebrew itself.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew7.png)

You will the terminal showing info similar to this while the installation is in progress. Just wait for it to finish.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew8.png)

Once it has finish you will see something similar to this in your terminal.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew9.png)

The closing section of the installer told us that we should run this command

~~~
brew doctor
~~~

Do this now:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrew10.png)

You have now successfully installed homebrew and are now ready to install some apps.

### Installing homebrew apps.

The first thing to do is update the formulae:

~~~
brew update
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewupdate1.png)

Once everything is updated it will look like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewupdate2.png)

[A list of available programs](https://github.com/mxcl/homebrew/tree/master/Library/Formula)

The basic idea of it is that you will run this command in your terminal window

~~~
brew install someapp
~~~

**lftp:**

~~~
brew install lftp
~~~

Use the above command in your terminal window to install `lftp`:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewlftp1.png)

The process will begin and it can take some times. Be patient and wait for it to finish:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewlftp2.png)

Once it has finished you will have the prompt returned and be able to use `lftp`:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewlftp3.png)

Here is an example of using `lftp` to show the version installed:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewlftp4.png)

**aria2:**

~~~
brew install aria2
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewaria21.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewaria22.png)

Once it has successfully installed you can called it using the command:

~~~
aria2c
~~~

For example:

~~~
aria2c --version
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Other%20software/OSX%20-%20Homebrew/homebrewaria23.png)

Check out this FAQ for using `aria2c` - [aria2c](https://www.feralhosting.com/faq/view?question=236)



