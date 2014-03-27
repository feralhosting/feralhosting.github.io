
Remove a folder:
---

To remove a whole folder, with files still in it, execute this command:

**Important note:** You will need to use quotes for folder names with spaces. for example `"some folder name/"`

~~~
rm -rfv foldername/
~~~

`-r` is for recursive
`-f` is for force removal
`-v` is for verbose - shows that is being deleted (can be omitted)

If the folder name has a space in it, use quotes around the folder name:

~~~
rm -rfv "some folder name"
~~~

Remove a file:
---

~~~
rm -fv filename
~~~

Notes:
---

The above commands are relative. This means that they will look for the file from where your current location in the shell is. Generally this is the safe way to remove files to prevent accidentally deleting important files or folders. The default after a successful login is your `$HOME` folder or slot root.

For example:

**Warning:** This command would delete the entire contents of your slot. because we used `~/`. That is bad, do not use this.

~~~
rm -rf ~/
~~~

So it is recommended you `cd` to a location then remove the files you want to delete.

For example:

~~~
cd ~/private/rtorrent/data
~~~

Then delete your files or folders

~~~
rm -rf "some folder name"
~~~



