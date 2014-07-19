
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

CMAKE installation
---

Use these first two commands to create to do some pre requisite tasks:

~~~
mkdir -p ~/bin && bash
~~~

Install the program using these commands:

Using the pre-compiled binary:
---

**3.0.0 Latest version**

~~~
wget -qO ~/cmake.tar.gz http://www.cmake.org/files/v3.0/cmake-3.0.0-Linux-i386.tar.gz
tar xf ~/cmake.tar.gz
cp -rf ~/cmake-3.0.0-Linux-i386/. ~/
cd && rm -rf cmake{-3.0.0-Linux-i386,.tar.gz}
~~~

Using the source code:
---

~~~
wget -qO ~/cmake.tar.gz http://www.cmake.org/files/v3.0/cmake-3.0.0.tar.gz
tar xf ~/cmake.tar.gz && cd ~/cmake-3.0.0
./configure --prefix=$HOME
make && make install
cd && rm -rf cmake{-3.0.0,.tar.gz}
~~~

Usage:
---

You can use this prefix to specify the directory you wish to install the program to.

~~~
cmake -DPREFIX=$HOME
~~~

Issues with CURL:
---

When installing `weechat` for example, the curl location is not default so we must specify it. To do this though we must make sure it is not going to skip an important setting.

Inside the directory of the application you wish to install there should be a file called `CMakeLists.txt`. Open this file and check for the line:

~~~
SET(CMAKE_SKIP_RPATH ON
~~~

If this line exists then remove it.

This example is how `weechat` is installed on the slot when the script is used.

~~~
cmake -DCMAKE_INSTALL_RPATH=/opt/curl/current/lib -DPREFIX=$HOME -DCURL_LIBRARY=/opt/curl/current/lib/libcurl.so -DCURL_INCLUDE_DIR=/opt/curl/current/include
~~~



