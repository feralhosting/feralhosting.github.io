
Find files
---

To find specific files by name in your home folder, use this command:

~~~
find ~ -name "name_of_file"
~~~

`~` stands for your home folder, the same as `$HOME` or `/home/username`

Example:

~~~
find ~ -name blueray
~~~

This will find all files with the word `blueray` in the name. You can use wildcards like * to search a partial name, like `blue*`

To find files by extension, use this command:

~~~
find ~ -name "*.given_extension"
~~~

Example:

~~~
find ~ -name "*.jpg"
~~~

This will show you all files, with the `.jpg` extension.

There are many more uses and examples [here](http://www.go2linux.org/usages-examples-of-find-command).



