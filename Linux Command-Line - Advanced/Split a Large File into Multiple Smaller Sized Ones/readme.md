This is a bash script that uses the Linux `dd` command to split files into several smaller files and then merge them together using the cat command.

First off, to be able to use the script from any directory you might be in, the catalog where the script is in should be included in the PATH environment variable. The easiest way to make that happen is actually to create a bin folder in your home catalog and then put the script there. 

Make sure you are in your home catalog. Quickest way to do that is typing cd and pressing enter at the command line. Then create the bin catalog.

~~~
mkdir -p ~/bin
source ~/.bashrc && source ~/.profile
~~~

~~~
nano –w ~/bin/fsplit
~~~

Copy and paste the following script into your nano:

~~~
#! /bin/sh
#
# splits a binary file into chunks.
# Written 1995 by Frank Pihofer <fp@fpx.de>
# Modified 2009 by Freilantzer
#
FILE=00
COUNT=0
INPUT=
SIZE=
NAME=
#
if [ $# != 2 ] ; then
    echo usage: $0 \[filename \| -\] \<size in kb\>
    exit 1
fi
#
if [ "$1" = "-m" ] ; then
    cat $2.part* > $2
    echo parts merged to $2
    exit 0
fi
#
if [ "$1" = "-" ] ; then
    INPUT=
else
    INPUT=if=$1
fi
#
NAME=$1
SIZE=$2
VALUE=0
#
while dd $INPUT bs=1k skip=$COUNT count=$SIZE of=$NAME.part$FILE 2> /dev/null ; do
#
if [ ! -s $NAME.part$FILE ] ; then
    break;
fi
#
if [ "$INPUT" != "" ] ; then
    COUNT=$(echo $COUNT + $SIZE | bc)
fi
#
FILE=$(echo $FILE + 1 | bc)
#
if [ "$(echo $FILE | cut -c 1)" = "$FILE" ] ; then
    FILE=0$FILE
fi
#
done
#
rm -f xx$FILE
#
~~~

Then press and hold `CTRL` and then press `x` to save. Press `y` to confirm. After that you have to make the file executable by doing:

~~~
chmod 700 ~/bin/fsplit
~~~

### To split a file:

~~~
fsplit filename filesize-in-kbytes
~~~

~~~
fsplit mylargefile.ext 50000
~~~

This command would split the file `mylargefile.ext` into several smaller files with a size about `50 MByte`. They will be named `mylargefile.ext.part00` and so on. 

**Important note:** There is currently no feedback on progress. A large file will take minutes or more to split.

**TIP**

To add the command to WinSCP Custom Commands, add this line:

~~~
fsplit "!" "!?File -S:?50000!"
~~~

It will give you a pop-box where you can change the split size. 
For more WinSCP Custom Commands, please see [this FAQ](https://www.feralhosting.com/faq/view?question=27).

To merge the files:

~~~
fsplit –m original filename
~~~

~~~
fsplit –m mylargefile.ext
~~~

This command will merge files named `mylargefile.ext.part00` and so on to a file named `mylargefile.ext`

### Using split

One more easy way is to use a command called `split` that is pre-installed command.

~~~
split -b 50 -d mylargefile.ext
~~~



