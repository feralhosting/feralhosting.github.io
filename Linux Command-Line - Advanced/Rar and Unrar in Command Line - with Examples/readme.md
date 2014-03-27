
Here are some useful examples of `rar` and `unrar` usage under Linux shell. 

To create a rar archive `archive.rar` containing directory called `folder_to_be_rared`, use the following command:

~~~
rar a archive.rar folder_to_be_rared/
~~~

To create a rar archive `archive.rar` containing files `file1.dat, file2.dat, file3.dat`, use:

~~~
rar a archive.rar file1.dat file2.dat file3.dat
~~~

or, more general:

~~~
rar a archive.rar file?.dat
~~~

 or 
 
~~~
rar a archive.rar *.* 
~~~

To create a password protected `rar` archive `archive.rar` with password set to `password`, use:

~~~
rar a -ppassword archive.rar folder_to_be_rared/ 
~~~

To create a password protected `rar` archive `archive.rar` with password set to `password`, where even file lists are encrypted, use:

~~~
rar a -hppassword archive.rar folder_to_be_rared/ 
~~~

To create a `rar` archive that splits the file/files into multiple parts of equal size, use:

~~~
rar a -v50M -R archive.rar folder_to_be_rared/
~~~

`-v50M` : determine the size of each file in split archive, in this example you get files with size `50MB` (if you wanted files of `512kB` size you would write `-v512k`)

To create a `rar` archive with a specified compression level (0-5):

~~~
rar a -m0 archive.rar folder_to_be_rared/
~~~

`-m0` : use a compression level of 0 (store only)
This will save a significant amount of time and processing power for you and other users on your server. 
`-m3`: this is the default compression level

To create a rar archive with files of `200MB` and with some other compression settings (got this from a scener)

~~~
rar a filename.rar -r -snd -m0 -vn -md4096 -ep1 -v200000000b $DIR
~~~

`-r` : Recurse subdirectories.
`-snd`: (no idea)
`-m0` : compression level (`0-store` / `3-default` / `5-best`)
`-vn`: Use the old style volume naming scheme, where the first volume file in a multi-volume set has the extension .rar, following volumes are numbered from `.r00` to `.r99`.
`-md4096` : dictionary size in Kb (`64`,`128`,`256`,`512`,`1024`,`2048`,`4097`  or `a`,`b`,`c`,`d`,`e`,`f`,`g`)
`-ep1`:  Exclude base dir from names
`-v200000000b` : split rar files in `200000000b` (`200mb`) files

To extract `rar` archive `archive.rar`, use:

~~~
unrar e archive.rar 
~~~
 
This will uncompress the archive in the current directory, without creating a new folder. If you want to uncompress the archive with a full path, use the option `x`:

~~~
unrar x archive.rar 
~~~

To find and extract all `rar` archives in `.` path and redirect outputs to `unrar.log` log file, use:

~~~
find . -name '*.rar' -print0 | xargs -I{} -0 -n 1 unrar e -y '{}' >unrar.log 2>&1
~~~

You can read the manual for more options:

~~~
man rar
~~~

Press `q` to exit and arrows to scroll up/down.



