
Definition of Symlinks
---

What is a Symbolic Link?

If you've ever made a "Shortcut" to a file in Windows, you will easily be able to understand the Linux equivalent (where "aliases" and "shortcuts" came from in the first place!), called a "Symbolic Link". The easiest definition to understand is directly from the man page, A Symbolic Link is useful for maintaining multiple copies of a file in many places at once without using up storage for the 'copies'; instead, a link 'points' to the original copy.

(If you want to read more about it, type `man ln` in the Terminal.)

Let's say you have a folder you need to get to and it is buried deep in your folders. You can simply type:

~~~
cd /some/folder/name/deep/inside/other/folders
~~~

For a real example on feral servers:

~~~
cd ~/www/flatlinebb.mauve.feralhosting.com/public_html/
~~~

It can get annoying to type the long path every time.  A symbolic link will solve the problem.

To create the link, simply type the following:

~~~
cd ~
~~~

(this will put you in your home folder)

~~~
ln -s ~/www/flatlinebb.mauve.feralhosting.com/public_html/ web_folder
~~~

That's it. `ln -s` makes a new file called `web_folder` which points to the deeply buried folder `~/www/flatlinebb.mauve.feralhosting.com/public_html/`.
I used an underscore, because Linux doesn't like spaces, and then you can also complete the name of the folder just by typing we and hitting tab to have the system auto-complete it for you.

To see that this worked, you can simply type:

~~~
ls -l
~~~

You should see a line with the following text:

~~~
web_folder -> ~/www/flatlinebb.mauve.feralhosting.com/public_html/
~~~

The arrow shows you exactly what you did... A file named `web_folder` points to `~/www/flatlinebb.mauve.feralhosting.com/public_html/`.

**Important note:** While this method can be used to put a data folder in the web directory, for http sharing with others, please use this faq to setup password protection for that folder:

[Putting your WWW folder to use](https://www.feralhosting.com/faq/view?question=20)
[Password protect your WWW folder](https://www.feralhosting.com/faq/view?question=22)

**Acknowledgment:**

Parts of this tutorial have been inspired by [this site](http://www.macosxhints.com/article.php?story=2001110610290643).



