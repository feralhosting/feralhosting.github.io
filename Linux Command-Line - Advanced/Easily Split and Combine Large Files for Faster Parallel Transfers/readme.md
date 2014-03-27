
You need to SSH to your slot to start/complete this guide. Please see this [Basic SSH Guide](https://www.feralhosting.com/faq/view?question=12)

Once in there, type this:

~~~
split -b 5m ./yourlargefile.avi
~~~

This will split it into several 5 megabyte files so that you can transfer it faster using parallel connections with an FTP/SFTP client like FileZilla for significantly increased throughput. I prefer files around `5Mb`, but that's really just preference. You can replace the 5 in the above line with any other number of megabytes you'd like, and/or replace the `m` with a `k` for kilobytes.

The naming conventions will be three-letter names all beginning with `x` by default. If you'd like to change the naming convention to where it starts with, say the word `new`, just add that to the end of the command that you entered. I'd recommend creating a temporary local folder where you can store all of them so that nothing gets mixed up once you've downloaded them all.

Once you have the files on your computer, open Terminal and and cd into the directory where you put all of your files. Since they all begin with the letter `x`, you can type this, assuming you don't have anything else in the directory beginning with that letter:

~~~
cat x* > thenameofyourcompletefile.avi
~~~

Give it a minute, and you'll have a completely re-combined file.

If, after the first step, you get an error saying something about file naming conventions being exhausted, that means that your file required more than 676 smaller files to be split into, assuming you've used the default naming convention. Consider choosing a larger piece size.



