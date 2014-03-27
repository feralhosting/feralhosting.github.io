
The listing below will recursively convert flac to mp3 and tags using flac, metaflac and lame. 

It is written in Perl and creates the files in a seperate directory tree and also copies across any artwork, so will handle multi discs and compilations. Probably not very elegant but it works :)

Script URL: 

~~~
wget -qO ~/convert.pl http://git.io/V1P_Dg
~~~

Now you can use the script like this:

**Important note:** Folder names with spaces will require that your wrap them in quotes, for example `"folder name"`.

~~~
perl convert.pl foldername bitrate
~~~

`foldername` should be the full path as found in your ftp client, if it contains spaces it must be enclosed in quotes. 

`bitrate` can be any legitimate `bitrate` from `128` to `320` for constant `bitrates` and `V2`,`V0` for a variable bitrate.

Constant bitrate options:

`128`
`164`
`192`
`224`
`256`
`320`

Variable bitrate options:

`V2`
`V0`

Usage example
---

~~~
perl convert.pl "private/rtorrent/data/my music folder" 320
~~~





