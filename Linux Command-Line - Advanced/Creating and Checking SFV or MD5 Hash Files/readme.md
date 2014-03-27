
To check and create hash-check files on your slice use the `cfv` program. It works with, and creates standard `.sfv` and `.md5` files that many downloads come with. It should be installed on your server already, but if it's missing, please [open a ticket](https://www.feralhosting.com/manager/tickets/new) requesting it.

To check files, run this command in the folder that contains the `.sfv` file (it will look for the `.sfv` file automatically):

~~~
cfv
~~~

To create a hash file, run this command in the folder that contains the files you want to hash (it will create a `.sfv` file with the name of the folder you are currently in as its filename): 

~~~
cfv -C -t sfv *
~~~

`-C` — is for "create mode";
`-t` — sets the file type to create (`.sfv` in this case);
`*` — will select all files within the folder.

For more help with the cfv command, including which other file types it supports, please type this to get the build-in help:

~~~
cfv --help
~~~

or for more in depth guide:

~~~
man cfv
~~~



