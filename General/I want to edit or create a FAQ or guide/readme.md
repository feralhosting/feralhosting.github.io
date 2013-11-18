
How do I create a FAQ?
---

Click on this link: [Add a Question](https://www.feralhosting.com/faq/add) and paste in your formatted text as the answer. Your question is the Title of the FAQ or guide. Open a ticket as outlined below to inform staff of the new FAQ.

See below for formatting guidelines

How do I edit a FAQ?
---

Simply **click on edit at the bottom of the FAQ** and submit your edited version along with reason for the change.

You can use Markdown to edit or create a FAQ if you wish. You will have to convert it to Feral BBCode using this tool:

[Markdown to BBCode](http://feralhosting.github.io/convert/m2b/index.html)

**Important note:** Please use fenced code blocks and in-line URLs (not the type linked at the bottom of the page). See formatting guidelines below for more info

Here are some good on-line Markdown editors.

[stackedit.io](https://stackedit.io/)

[markable.in](http://markable.in/editor/) 

[dillinger.io](http://dillinger.io/)

There is also a BBCode to Markdown tool for porting an existing FAQ so it can be edited or updated in Markdown and then converted back.

[BBCode to Markdown](http://feralhosting.github.io/convert/b2m/index.html)

Copy and paste the returned text into a new FAQ or an edit. The layout and formatting will be correct, there is no need to change it.

Please don't get too creative with the tags. These tools are very specific to the tags used here at Feral, which are documented below.

These are some Tags that work for formatting. They all need to be properly closed using `[/tag]`.
For example you would close code like this: `[/code]`

Title tags
---

h1

~~~
[h1] Title h1 [/h1]
~~~

Here is the markdown equivalent:

~~~
Markdown Title h1
===
~~~

h2

~~~
[h2] Title h2 [/h2]
~~~

Here is the markdown equivalent:

~~~
Markdown Title h2
---
~~~

h3

~~~
[h3] Title h3 [/h3]
~~~

Here is the markdown equivalent:

~~~
### Markdown Title h3
~~~

h4

~~~
[h4] Title h4 [/h4]
~~~

Here is the markdown equivalent:

~~~
#### Markdown Title h4
~~~

h5

~~~
[h5] Title h5 [/h5]
~~~

Here is the markdown equivalent:

~~~
##### Markdown Title h5
~~~

h6

~~~
[h6] Title h6 [/h6]
~~~

Here is the markdown equivalent:

~~~
###### Markdown Title h6
~~~

Code blocks
---

For single lines:

~~~
[code]Standard code blocks with a single line[/code]
~~~

For multiple lines:

~~~
[code]Standard
code 
blocks
with
multiple
lines[/code]
~~~

Here is the markdown equivalent:

For single lines:

    ~~~
    Standard code blocks with a single line
    ~~~

For multiple lines:

    ~~~
    Standard
    code 
    blocks
    with
    multiple
    lines
    ~~~

In-line code blocks:

~~~
[code single]in-line code[/code]
~~~

Here is the markdown equivalent:

~~~
`in-line code`
~~~

CODE blocks specifics
---

For formatted code blocks follow this rule below:

When using the code tag use this rule for formatting regarding new lines please.

~~~
Blank line above

[code]Some code wrapped in code tags[/code]
No new/blank line below.
~~~

This rule also applies for tags that also apply formatting above and below the line like the `H2` and `H3` tag do, but not the Bold tag for example. You can leave a blank line below the `b`,`i`,`img`,`url` tags.

This rule does not apply when using markdown and the converter to format the document.

Bold and Italic tags
---

Bold:

~~~
[b] bold [/b]
~~~

Here is the markdown equivalent:

~~~
** bold **
~~~

Strong:

~~~
[strong] strong (will be manually replaced by bold) [/strong]
~~~

Here is the markdown equivalent:

~~~
** strong **
~~~

Italic:

~~~
[i] italic [/i]
~~~

Here is the markdown equivalent:

~~~
* italic *
~~~

Emphasis:

~~~
[em] emphasis (will be manually replaced by italic) [/em]
~~~

Here is the markdown equivalent:

~~~
* emphasis *
~~~

Image tags
---

Use this opening and closing tag for direct links to images.

This example tag usages will give us:

~~~
[img]http://i.imgur.com/pRfcyAi.jpg[/img]
~~~

This result:

![](http://i.imgur.com/pRfcyAi.jpg)

Here is the markdown equivalent:

~~~
![](http://i.imgur.com/pRfcyAi.jpg)
~~~

URL and URL tags
---

URLs are automatically detected and do not need a tag, so this:

~~~
http://i.imgur.com/pRfcyAi.jpg
~~~

This URL will be automatically detected and give you a click-able link, for example:

http://i.imgur.com/pRfcyAi.jpg

URLs with a description - should be used in a specific way using the URL tag.

~~~
[url=http://i.imgur.com/pRfcyAi.jpg]Link description[/url]
~~~

Will give us this result:

[Link description](http://i.imgur.com/pRfcyAi.jpg)

Here is the markdown equivalent:

~~~
[Link description](http://i.imgur.com/pRfcyAi.jpg)
~~~

Custom Software
---

Custom software installations that have a typical structures, such as `~/something/bin` should be installed to `~/programs`. The use this command to add it to the `PATH` if needed. This will fall in line with other software installation FAQs.

~~~
[[ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'export PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

Exceptions to the rule?

1: Programs like AeroFS and Spideroak that do not have a directory structure that would work for the `~/programs` location or other self contained applications.

2: Programs that might conflict with slot operations such as Python. Then use a custom location for this software. Try not to use a very complex or needlessly deep directory structure.

Python and user mods.
---

When a `--user` mod is installed using the slot's included Python, it will always go to the location:

~~~
~/.local/bin
~~~

So in this case, use this command to add the `PATH` to the `~/.bashrc`. This will fall in line with other Python FAQs.

~~~
[[ ! "$(grep '~/.local/bin' ~/.bashrc)" ]] && echo 'export PATH=~/.local/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc
~~~

File Hosting
---

**IMAGES**

When needed some images will be re-hosted, so use whatever you need/can when editing the faq.

[http://imgur.com/](http://imgur.com/) is a popular choice.

**FILES**

Important files will be re-hosted on a more permanent platform when needed. If this is important include this info in the ticket.

[http://www.mediafire.com/](http://www.mediafire.com/) is a good choice.

Closing: At the end of the FAQ
---

Please leave 4 blank lines at the end of any question you edit or submit. This is a visual thing.

Credit will be attributed to the original author(s) where needed manually. So do not worry about this.

**Attention:** After you have edited the guide please submit a ticket using the title format `FAQ Edit - FAQ name - Category`

In the body submit a link to the FAQ you edited. So for example:

**Title:** FAQ Edit - I want to edit a FAQ or guide - General

**Body:** https://www.feralhosting.com/faq/view?question=122 I fixed a broken link.

Feral FAQ Cheat Sheet
---

What is this? this is a list of preferred formatting when adding certain info. Feel free to add to this.

Use `$(whoami)` and `$(hostname)` to automatically insert a users info.

~~~
cd ~/www/$(whoami).$(hostname)/public_html/
~~~

The following command in SSH to see the `hostname` and IP:

~~~
host $(hostname)
~~~

The following command in SSH to see the IP only:

~~~
hostname -i
~~~

The following command to get your external IP:

~~~
curl -s icanhazip.com
~~~

[wget](http://linux.die.net/man/1/wget)

`-q` quiet
`-N` Overwrite if newer or different (timestamps)
`-O` Save to file.
`-P` Set directory prefix to prefix. Is the directory where all other files and subdirectories will be saved to

~~~
wget -q www.somelink.com/script.sh -O thisfile.sh
~~~

You will see most FAQs use this format:

~~~
wget -qO ~/thisfile.sh www.somelink.com/script.sh
~~~

This basically just puts the file in the slot root with the use of `~/` using the filename specified.

[tar](http://linux.die.net/man/1/tar)

`-c` create
`-x` extract
`-z` .gz or .tgz
`-j` .bz2
`-f` file
`-v` verbose
`-C` to directory

**Important note:** `tar` can detect the compression used so it is not actually required to specify it. This means the use of `z` and `j` are optional.

~~~
tar xf archive.tar.gz
~~~

~~~
tar xf archive.tar.gz -C some/directory/
~~~

[unzip](http://linux.die.net/man/1/unzip)

`-q` quiet
`-o` overwrite
`-d` extract to directory 

~~~
unzip -qo archive.zip
~~~

~~~
unzip -qo archive.zip -d some/directory/
~~~

### screen

Send a command to a running screen and window of choice.

~~~
screen -S screen-name -p 0 -X exec your-command-goes-here
~~~

`-S` screen-name you want to match
`-p` number of the screen window, 0 in this case sends it to the first.
`exec` some-command

When using **screen** give the window a name by using **-S** for easier management. The word after the **-S** is the name of the window, in this case rtorrent.

This will attach to a screen with this name:

~~~
screen -S rtorrent rtorrent
~~~

This will attach to a screen with this name or create it if it doesn't:

~~~
screen -R rtorrent rtorrent
~~~

Will start the selected process in the background as a daemon and detach from it immediately:

~~~
screen -dmS rtorrent rtorrent
~~~

[kill](http://linux.die.net/man/1/kill)

~~~
kill -9 PID
~~~

[killall](http://linux.die.net/man/1/killall)

~~~
killall -9 -u $(whoami) processname
~~~

### TAB autocomplete

Use `TAB` to autocomplete parts of your SSH commands.

For example: if I am in my home folder and I wish to go to my 

~~~
~/private/rtorrent
~~~

I can do this

~~~
cd ~/p TAB
~~~

Which will give me this:

~~~
~/private/
~~~

Unless I have more than one folder starting with **p**. then I must give a second or third letter depending on how they conflict. In this case I do not have a conflicting folder name.

Then if I do:

~~~
cd ~/private/r TAB
~~~

I will end up with this:

~~~
cd ~/private/rtorrent/
~~~

So now I press enter. I have now used TAB to auto-complete parts of my **cd** command.

### github url shortening

[http://git.io/](http://git.io/)

[git-io-github-url-shortener](https://github.com/blog/985-git-io-github-url-shortener)

You can do it in SSH using this command.

~~~
curl -i http://git.io -F "url=YOU.URL.HERE"
~~~

### Chaining Commands

The use of `&&` will move to the next command if the previous command was successful.

~~~
cd ~/private && mkdir test && cd test
~~~

So if the directory `~/private` did not exist the command would stop at the point where a single command did not execute successfully.

The use is `;` will just chain a series of commands. 

~~~
cd ~/private; mkdir test; cd test
~~~

Here it will just do command one then execute the next until it reaches the end. So if `~/private` did not exist the command would create the `test` folder in the wrong place.

**Run a process and send it to the background.**

if you add a `&` to the end of your command it will be sent to the background as your run it.

~~~
./some/path/to/a/binary &
~~~

### Crontab

**Important note:** It is generally best practice to use full paths to the programs you wish to execute. To get the full path do this in SSH:

Use the `whereis` command to find the binary locations:

~~~
whereis cp
~~~

Will return something like this:

~~~
cp: /bin/cp /usr/share/man/man1/cp.1.gz
~~~

Here the path we need is:

~~~
/bin/cp
~~~

To edit your crontab:

~~~
crontab -e
~~~

To execute a bash script from crontab you need to use this command:

~~~
bash -l
~~~

For example:

~~~
@reboot bash -l ~/myscript.sh
~~~

You can use this command to easily create a cronjob for users in some sort of support capacity:

~~~
(crontab -l ; echo "* * * * * some/cron/thing") | uniq - | crontab -
~~~

This will create a specified cronjob while also checking to make sure it is not created more than once. So with a single command you can have create and insert a cronjob for a user. It only checks vs the last entry though.



