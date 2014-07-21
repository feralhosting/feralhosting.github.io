
Generic Software Guide Introduction:
---

**Important note:** Just because you can do something does not automatically mean you should. For example, custom python installations tend to cause more problems that they solve.  Also if you think the programs you want to install will interfere with other users or that Staff might not want you using them you should [open a ticket](https://www.feralhosting.com/manager/tickets/new) and ask first. Please use some common sense with the programs you try to install and use.

With your Feral slot you do not have `root` access to the server. Your account runs as user account in a Debian Linux environment. These are not dedicated servers which means you cannot use these commands on your slot:

~~~
apt-get
su
sudo
~~~

This does not mean you cannot install software on your slot. It does means that you will have to attempt to install it to your `HOME` directory, or below, manually. **There is no official support from Feral staff for users doing this**. You can open a ticket to ask for any standard dependencies to be installed to your slot that you may require. Again this comes down to common sense when looking at the nature of the application and dependencies.

For this guide we will look at the methods available to you to install software on your slot. The main methods for installing software are:

**1:** Pre-compiled binaries or scripts created by the developers or similar. Examples of this include:

- ffmpeg
- java
- Python programs like flexget

**2:** Source-code to compile the binary on your slot. Examples of this include:

- git
- znc

**3:** Some Debian packages via unpacking them to access the binary.

- Spideroak
-  filebot

It is important that you understand that no one of these methods is a guaranteed thing. There are many factors that will contribute to the success or failure of the attempt. These could be dependencies on other applications, binaries, libraries or additional requirements that you have no way to fulfil. This is just something you will have to accept before attempting to install any software on your slot. In this linked examples you will see various methods and solutions to such issues.

Installed Software locations:
---

Throughout the Feral FAQs you will see that all user installed programs are installed to a single location which is:

~~~
$HOME
~~~

This is effectively your home directory and will mimic the conventional directory structure used by Unix type platforms for installing software, where applicable. Then you will see that this location is added to the `PATH` (this is done automatically at login if the folder exists):

~~~
~/bin
~~~

When we add a location to the `PATH` in Linux it basically tells the SSH terminal to include this location when it looks for the binaries to execute. If a location is not in the `PATH` you would be required to use a full path to that program in order to execute it in your terminal. This method is used for simplicity. All files are installed to the `~/bin` folder and generally maintain a conventional directory structure.

This FAQ will use the same directory structure for any examples used, though once you understand the process you can install applications where ever you want. 

You could then manage your installations and have more than one version of a program.

CMAKE
---

Some applications do not use `configure` and instead require you use `cmake` to build them. You can use this guide to install and use `CMAKE`:

[CMAKE - Basic Setup](https://www.feralhosting.com/faq/view?question=270)

--prefix=$HOME
---

It is very common for source code application to come with an executable file called `configure`. When using this program to configure our source code for installation we can often pass it some arguments that tell it to do certain things or behave in a certain way. The most important of theses is the `--prefix` argument.

If you do not specify a `prefix` what happens is that `configure` will assume you want to use the standard file structure such as `/etc` and `/lib` for which you do not have permission to use. So what we do is specify a `--prefix` that tell `configure` where to install the application and subsequently where to find the files it needs to run.

So when we pass this argument to `configure`:

~~~
--prefix=$HOME
~~~

We are telling it to install the application to root of our slot using the variable `HOME`. For example, with the above `prefix` our application will use this as the root installation directory when configuring the application

~~~
/media/12345/home/username
~~~

**Important note:** You can read the `configure` file with a text editor. In this file you will be able to find and see the available arguments you can use with this installation when you encounter some errors. the `configure` script is a text file you can open with a text editor. Open it and search for `--prefix` to find the rest of the options that may help solve the issue.

In some cases `configure` does not exist or is not included with the files and you must refer to the developers documentation to see how the files are required to be processed. This may require you to run a `autogen` or `bootstrap` script first.

Alternative Software locations:
---

Say you wanted multiple versions of a program installed. If you installed them all to `$HOME` you would just overwrite the previous version as it installed. To avoid this you would use a different `--prefix` when configuring, for example:

~~~
--prefix=$HOME/python27
~~~

~~~
--prefix=$HOME/python30
~~~

Or if you wanted all custom software in a managed location:

~~~
--prefix=$HOME/applications/python/python27
~~~

~~~
--prefix=$HOME/applications/python/python30
~~~

PATH explained:
---

**Important note:** The location `~/bin` is automatically added to your system PATH if the folder exists, upon logging into your SSH session. This is done by loading a setting in the `~/.profile` file on your slot when you log in via SSH. The examples used in the explanation below are for demonstration purposes only.

The concept of the `PATH` for new users can be a difficult one to come to terms with so I will briefly explain it here.

Your terminal makes use of all kinds of variables when processing information. `PATH` is one of these variables. `PATH` is basically just a list of locations, in order of preference from left to right, that the shell will look at when searching for a binary to execute. So when I use certain command in the terminal like `cp` or `mv` or `rm` I don't have to use the full path to the binary each and every time. Being a variable is means we can modify those locations to suit our needs and this will in turn be reflected in the behaviour of our terminal. The command for doing this will be used and explained through the FAQ.

One thing to consider when adding locations to the `PATH` variable is the order in which you wish the locations to be checked. Here is a standard entry to include a location to the `PATH` variable and I will explain this by breaking it down:

~~~
PATH=~/bin:$PATH
~~~

This is the variable we are modifying by saying `PATH` equals something. Like this:

~~~
PATH=
~~~

This is the location we are including:

~~~
~/bin
~~~

This means that we want to come before, or on the left of the existing `PATH` locations

~~~
:$PATH
~~~

To have it come after you would do this:

~~~
PATH=$PATH:~/bin
~~~

An example of this in use:

Let us say when have installed the statically pre-compiled `ffmpeg` binary to our slot. How do we use this over the existing `ffmpeg` already installed on the slot?

If we have installed it to `~/bin` then we would use this `PATH` in our `~/.bashrc`:

~~~
PATH=~/bin:$PATH
~~~

If we instead did this, it would find the existing, installed `ffmpeg` before find our own installation since it will look in the existing `PATH` locations first and it will find the default installation of `ffmpeg`:

~~~
PATH=$PATH:~/bin
~~~

**Important note:** This also means that the order in which you add paths to your `~/.bashrc` can change the search result.

For more information see this page - [internal variables.](http://tldp.org/LDP/abs/html/internalvariables.html)

wget usage in this FAQ
---

In this FAQ and others you will see  this command format used. I will briefly explain what it is and why it is used.

~~~
wget -qO ~/node.js.tar.gz http://somesite/somefile.tar.gz
~~~

`wget` - is the command that we wish to use to download the file
`-qO ~/somefile.tar.gz` - are the argurments we pass to `wget` so it performs some specific behaviour.
`http://somesite/somefile.tar.gz` - is the example URL to the pre-compiled file we want.

`q` tells `wget` to be quiet about the download and not to show us in the terminal.

`O ~/somefile.tar.gz` tells `wget` to name this file `somefile.tar.gz` in the root of you slot. This is because I use `~/` prefixed to the name of the file I have specified. `~` known as a `tilde` is basically shorthand for the full path to our `HOME` directory when used in a `BASH` shell. This shell is the default shell you will be using with your Feral slot.

~~~
~
~~~

Is the same as the path to your HOME folder, which will look something like this:

~~~
/media/12345/username/home
~~~

So this means that:

~~~
~/somefile.tar.gz
~~~

Is the same as:

~~~
/media/12345/username/home/somefile.tar.gz
~~~

This method is used to ensure the files we want are placed in a specific location that we can use to continue the installation.

**Important notes:**

With some URLs you may need to quotes the URL when certain characters are used. For example, using single quotes:

~~~
'http://somesite/somefile.tar.gz'
~~~

Some URLs do not return the file we actually want and in this case you can try to use this argument with `wget`:

~~~
--content-disposition
~~~

1: Pre-compiled binaries
---

In this example we will look at two particular applications that both have existing FAQs here.

[node.js - How to install](https://www.feralhosting.com/faq/view?question=199)

### node

The first thing to do is to create the `~/bin` directory and reload the relevant files for the PATH setting to take effect using this command:

~~~
mkdir -p ~/bin && bash
~~~

Now download the required files:

~~~
wget -qO ~/node.js.tar.gz http://nodejs.org/dist/v0.10.29/node-v0.10.29-linux-x64.tar.gz
~~~

Now we have downloaded the archive to our `HOME` folder we can unpack it. In this case the archive is a tar archive to we will use `tar` to extract it.

~~~
tar xf ~/node.js.tar.gz
~~~

**Important note:** Effectively, once you have extracted the the contents of the archive, the program is ready to use by directly calling it via a full path in you terminal using `~/node-v0.10.29-linux-x64/bin/node` . For the purposes of this FAQ will continue to move the files to a desired location and add that location to our `PATH`, if required, for easy use and so you become more familiar with the overall process.

Now the contents of the archive has just been extracted to the `HOME` folder of our slot. It will generally be safe to assume the new folder name is the same as the archive's minus the extension, but to make sure, we can type this command in our terminal:

~~~
ls
~~~

As we can see the folder name is `node-v0.10.29-linux-x64`

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral Wiki/Software/Generic Software Installation Guide/lsnode.png)

The directory structure of the pre-compiled programs will commonly resemble the standard Unix directory structure, though this is not always true so it is good to check first.

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral Wiki/Software/Generic Software Installation Guide/nodedirectory.png)

So what we need to do is copy the contents of the folder to our desired location, being our server root (using the shorthand `~/`)  in this example:

~~~
cp -rf ~/node-v0.10.29-linux-x64/. ~/
~~~

Now installed `node` and it is ready for use by simple called `node` in the terminal.

~~~
node -v
~~~

And that is how you can install and use software that has be pre compiled to run on the linux platform. Now to tidy up a bit.

Use the `cd` command. Using just `cd` on its own will return you to the `HOME` directory.

~~~
cd
~~~

Now you can delete the files and folders we no longer require.

~~~
rm -rf node{-v0.10.29-linux-x64,.js.tar.gz}
~~~

We are using [bash brace expansion](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html) to remove the files.

**Important note:** Not every pre-compiled binary will conform to this FAQ and might have a unique directory structure that doe not quite fit in with what was described in this section. See the `filebot` example to see this.

2: Compiling from source
---

The first thing to do is to create the `~/bin` directory and reload the relevant files for the PATH setting to take effect using this command:

~~~
mkdir -p ~/bin && bash
~~~

When compiling from source you will need to follow this outline, we will use `curl` as the installation example. First, we download the software to a file named `curl.tar.gz` in our `HOME` directory using this command:

~~~
wget -qO ~/curl.tar.gz http://curl.haxx.se/download/curl-7.37.1.tar.gz
~~~

Now we need to extract the archive

~~~
tar xf ~/curl.tar.gz
~~~

Now the contents of the archive has just been extracted to the `HOME` folder of our slot. It will generally be safe to assume the new folder name is the same as the archive's minus the extension, but to make sure, we can type this command in our shell:

~~~
ls
~~~

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral Wiki/Software/Generic Software Installation Guide/lscurl.png)

As we can see the folder name is `curl-7.37.1`. So now we move into this folder using the `cd` command:

~~~
cd ~/curl-7.37.1
~~~

Now we will configure `curl` to use our desired installation location, which is `$HOME`:

~~~
./configure --prefix=$HOME
~~~

Once the configuration is complete you can `make` the file:

**Important note:** This stage can take a very long time. The time taken varies from one application to the other.

~~~
make
~~~

If this step completed successfully you can now `make install` the program to finish the process.

~~~
make install 
~~~

Once this command has completed you can leave the folder using the `cd` command. Using just `cd` on its own will return you to the `HOME` directory.

~~~
cd
~~~

You can now remove the downloaded files. As you can see in this command there is one folder `curl-7.37.1` and one archive `curl.tar.gz` being removed. You can chain more than one file or folder to be removed this way.

~~~
rm -rf  curl{-7.37.1,.tar.gz}
~~~

We are using [bash brace expansion](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html) to remove the files.

Do this command to call `curl` and check it's version.

~~~
curl -V
~~~

**Important note:** Not every source-code package will conform to this FAQ and might have unique requirements or hard coded settings that cannot be tweaked to suit the Feral slot with the scope of this FAQ. See the `git` FAQ for an example of this.

3: Debian packages
---

To explain is simply, a `deb` is an archive that contains folders and files using a standard directory structure. We can extract the `deb` and attempt to use the files.

First download the `deb` that you want to extract:

~~~
wget -qO ~/some.deb 'https://somesite/some.deb'
~~~

Now we will extract the `deb` using the `dpkg-deb` command. We will tell it where we want the files to be extracted to. It will create this location if it does not exist. In our example this location is `desired-location`. So we are going to extract `some.deb` to `desired-location`.

~~~
dpkg-deb -x ~/some.deb ~/desired-location
~~~

Now you will find that the contents of the `desired-location` contain a standard directory structure. This is because file would generally be extracted to the core system folders and not a subdirectory when installed using a `deb`. 

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral Wiki/Software/Generic Software Installation Guide/debdirectory.png)

So to make it more user like we can do this:

~~~
cp -rf ~/desired-location/usr/bin/. ~/desired-location
~~~

~~~
cd
~~~

~~~
rm -rf some.deb desired-location/{etc,usr}
~~~

Examples:
---

1: Pre-compiled examples
---

[node.js - How to install](https://www.feralhosting.com/faq/view?question=199)
[Java 1.7](https://www.feralhosting.com/faq/view?question=183)
[p7zip - basic installation](https://www.feralhosting.com/faq/view?question=245)
[BitTorrent Sync btsync - basic setup](https://www.feralhosting.com/faq/view?question=224)
[Mumble client and murmur server](https://www.feralhosting.com/faq/view?question=227)
[ffmpeg](https://www.feralhosting.com/faq/view?question=268)
[Plowshare - a download tool for file sharing websites - with auto captcha solving](https://www.feralhosting.com/faq/view?question=157)
[CouchPotato - An automatic NZB and torrent downloader for Films](https://www.feralhosting.com/faq/view?question=218)
[Dropbox - How to install](https://www.feralhosting.com/faq/view?question=205)

2: Source-code examples
---

[Icecast - streaming media server](https://www.feralhosting.com/faq/view?question=155)
[ImageMagick - Basic Setup](https://www.feralhosting.com/faq/view?question=266)
[Git - How to Install](https://www.feralhosting.com/faq/view?question=206)
[Ruby - Basic Setup](https://www.feralhosting.com/faq/view?question=265)
[Python - How to install](https://www.feralhosting.com/faq/view?question=204)
[ZNC - Basic Setup](https://www.feralhosting.com/faq/view?question=264)
[Curl - Basic Setup](https://www.feralhosting.com/faq/view?question=267)
[Mosh - Basic Setup](https://www.feralhosting.com/faq/view?question=269)
[Duplicity - Basic Setup](https://www.feralhosting.com/faq/view?question=255)

3: Debian packages examples
---

[SpiderOak](https://www.feralhosting.com/faq/view?question=203)
[FileBot CLI - Basic Setup](https://www.feralhosting.com/faq/view?question=256)



