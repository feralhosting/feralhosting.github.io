
**Important note:** Feral uses powers of 1000 to calculate your usage!

`1000` = `kB` / `MB` / `GB` / `TB`

`1024` = `KiB` / `MiB` / `GiB` / `TiB`

To check the amount of space used in your slice, type this command:

~~~
du -sB GB ~/
~~~

`-s` is for summarize, instead of each folder size listed separately

`-B` is for block size. In this case it is `GB`

There might be a delay before any response is displayed — it may possibly take up to 3 minutes for the system to calculate the amount of data in your slice.

To check the size of a folder you can do:

~~~
du -sB GB ~/private/rtorrent/data
~~~

### Tip

You can create an alias for the above command (or any command) in your `.bash_aliases` file, which is located in your `~/` (home) directory. Just edit the `.bash_aliases` file, and add this line to it:

~~~
alias space='du -sB GB ~/'
~~~

You can name it whatever you want - I happen to call it `space`, because it's easy for me to remember.



