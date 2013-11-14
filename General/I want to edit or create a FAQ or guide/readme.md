
[h3]How do I create a FAQ?[/h3]
Click on this link: [url=https://www.feralhosting.com/faq/add]Add a Question[/url] and paste in your formatted text as the answer. Your question is the Title of the FAQ or guide. Open a ticket as outlined below to inform staff of the new FAQ.

See below for formatting guidelines

[h3]How do I edit a FAQ?[/h3]
Simply [b]click on edit at the bottom of the FAQ[/b] and submit your edited version along with reason for the change.

You can use Markdown to edit or create a FAQ if you wish. You will have to convert it to Feral BBCode using this tool:

[url=http://feralhosting.github.io/convert/m2b/index.html]Markdown to BBCode[/url]

[b]Important note:[/b] Please use fenced code blocks and in-line URLs (not the type linked at the bottom of the page). See formatting guidelines below for more info

Here are some good on-line Markdown editors.

[url=http://benweet.github.io/stackedit/]http://benweet.github.io/stackedit/[/url]

[url=http://markable.in/editor/]http://markable.in/[/url] 

[url=http://dillinger.io/]http://dillinger.io[/url]

There is also a BBCode to Markdown tool for porting an existing FAQ so it can be edited or updated in Markdown and then converted back.

[url=http://feralhosting.github.io/convert/b2m/index.html]BBCode to Markdown[/url]

Copy and paste the returned text into a new FAQ or an edit. The layout and formatting will be correct, there is no need to change it.

Please don't get too creative with the tags. These tools are very specific to the tags used here at Feral, which are documented below.

These are some Tags that work for formatting. They all need to be properly closed using [code single][[][/[]/tag][/code].
For example you would close code like this: [code single][[][/[]/code][/code]

[code single][[][/[]h1][/code] Title h1 [code single][/h1][/code]

Here is the markdown equivalent:

Markdown Title h1
[code single]===[/code]

[code single][[][/[]h2][/code] Title h2 [code single][/h2][/code]

Here is the markdown equivalent:

Markdown Title h2
[code single]---[/code]

[code single][[][/[]h3][/code] Title h3 [code single][/h3][/code]

Here is the markdown equivalent:

[code single]###[/code] Markdown Title h3

[code single][[][/[]h4][/code] Title h4 [code single][/h4][/code]

Here is the markdown equivalent:

[code single]####[/code] Markdown Title h4

[code single][[][/[]h5][/code] Title h5 [code single][/h5][/code]

Here is the markdown equivalent:

[code single]#####[/code] Markdown Title h5

[code single][[][/[]h6][/code] Title h6 [code single][/h6][/code]

Here is the markdown equivalent:

[code single]######[/code] Markdown Title h6

[code single][[][/[]b][/code] bold [code single][/b][/code]

Here is the markdown equivalent:

[code single]**[/code] bold [code single]**[/code]

[code single][[][/[]code][/code] Standard code blocks [code single][[][/[]/code][/code]

Here is the markdown equivalent:

[code single]~~~[/code]
Standard code blocks
[code single]~~~[/code]

[code single][[][/[]code single][/code] in-line code [code single][[][/[]/code][/code]

Here is the markdown equivalent:

[code single]`[/code] in-line code [code single]`[/code]

[code single][[][/[]strong][/code] strong (can/will be manually replaced by italic) [code single][/strong][/code]

Here is the markdown equivalent:

[code single]**[/code] strong [code single]**[/code]

[code single][[][/[]i][/code] italic [code single][/i][/code]

Here is the markdown equivalent:

[code single]*[/code] italic [code single]*[/code]

[code single][[][/[]em][/code] italic (can/will be manually replaced by italic) [code single][/em][/code]

Here is the markdown equivalent:

[code single]*[/code] italic [code single]*[/code]

[h3]Image tags[/h3]
Use this opening and closing tag for direct links to images.

This example tag usages will give us:

[code][[][/[]img]http://i.imgur.com/pRfcyAi.jpg[/img][/code]
This result:

[img]http://i.imgur.com/pRfcyAi.jpg[/img]

Here is the markdown equivalent:

[code]![http://i.imgur.com/pRfcyAi.jpg](http://i.imgur.com/pRfcyAi.jpg)[/code]
[h3]URL and URL tags[/h3]
URLs are automatically detected and do not need a tag, so this:

[code]http://i.imgur.com/pRfcyAi.jpg[/code]
This URL will be automatically detected and give you a click-able link, for example:

http://i.imgur.com/pRfcyAi.jpg

[b]URLs with a description[/b] - should be used in a specific way using the URL tag.

[code][[][/[]url=http://i.imgur.com/pRfcyAi.jpg]Link description[/url][/code]
Will give us this result:

[url=http://i.imgur.com/pRfcyAi.jpg]Link description[/url]

Here is the markdown equivalent:

[code][Link description](http://i.imgur.com/pRfcyAi.jpg)[/code]
[h3]CODE blocks specifics[/h3]
For [code single]pre[/code] formatted code blocks follow this rule below:

When using the code tag use this rule for formatting regarding new lines please.

[code]Blank line above

[[][/[]code]Some code wrapped in code tags[[][/[]/code]
No new/blank line below.[/code]
This rule also applies for tags that also apply formatting above and below the line like 
the [code single]H2[/code] and [code single]H3[/code] tag do, but not the Bold tag for example. You can leave a blank line below
the [code single]b[/code],[code single]i[/code],[code single]img[/code],[code single]url[/code] tags.

[h3]Custom Software[/h3]
Custom software installations that have a typical structures, such as [code single]~/something/bin[/code] should be installed to [code single]~/programs[/code]. The use this command to add it to the [code single]PATH[/code] if needed. This will fall in line with other software installation FAQs.

[code][[][/[][ ! "$(grep '~/programs/bin' ~/.bashrc)" ]] && echo 'PATH=~/programs/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc[/code]
Exceptions to the rule?

1: Programs like AeroFS and Spideroak that do not have a directory structure that would work for the [code single]~/programs[/code] location or other self contained applications.

2: Programs that might conflict with slot operations such as Python. Then use a custom location for this software. Try not to use a very complex or needlessly deep directory structure.

[h3]Python and user mods.[/h3]
When a [code single]--user[/code] mod is installed using the slot's included Python, it will always go to the location:

[code]~/.local/bin[/code]
So in this case, use this command to add the [code single]PATH[/code] to the [code single]~/.bashrc[/code]. This will fall in line with other Python FAQs.

[code][[][/[][ ! "$(grep '~/.local/bin' ~/.bashrc)" ]] && echo 'PATH=~/.local/bin:$PATH' >> ~/.bashrc ; source ~/.bashrc[/code]

[h3]File Hosting[/h3]
[b]IMAGES[/b]

When needed some images will be re-hosted, so use whatever you need/can when editing the faq.

[url=http://imgur.com/]http://imgur.com/[/url] is a popular choice.

[b]FILES[/b]

Important files will be re-hosted on a more permanent platform when needed. If this is important include this info in the ticket.

[url=http://www.mediafire.com/]http://www.mediafire.com/[/url] is a good choice.

[b]Closing: At the end of the FAQ[/b]

Please leave 4 blank lines at the end of any question you edit or submit. This is a visual thing.

Credit will be attributed to the original author(s) where needed manually. So do not worry about this.

[b]After you have edited the guide please submit a ticket called:[/b]

[b]FAQ Edit - FAQ name - Category[/b]

In the body submit a link to the FAQ you edited. So for example:

[b]Title:[/b] FAQ Edit - I want to edit a FAQ or guide - General

[b]Body:[/b] https://www.feralhosting.com/faq/view?question=122 I fixed a broken link.

[h3]Feral FAQ Cheat Sheet[/h3]
What is this? this is a list of preferred formatting when adding certain info. Feel free to add to this.

[b]Use [code single]$(whoami)[/code] and [code single]$(hostname)[/code] to automatically insert a users info.[/b]

[code]cd ~/www/$(whoami).$(hostname)/public_html/[/code]
[b]The following command in SSH to see the hostname and IP[/b]

[code]host $(hostname)[/code]
[b]The following command in SSH to see the IP only[/b]

[code]hostname -i[/code]
The following command to get your external IP

[code]curl -s icanhazip.com[/code]
[b][url=http://linux.die.net/man/1/wget]wget[/url][/b]

-q quiet
-N Overwrite if newer or different (timestamps)
-O Save to file.
-P Set directory prefix to prefix. Is the directory where all other files and subdirectories will be saved to

[code]wget -q www.somelink.com/script.sh -O thisfile.sh[/code]
You will see most FAQs use this format:

[code]wget -qO ~/thisfile.sh www.somelink.com/script.sh[/code]
This basically just puts the file in the slot root with the use of [code single]~/[/code]

[b][url=http://linux.die.net/man/1/tar]tar[/url][/b]

-c create
-x extract
-z .gz or .tgz
-j .bz2
-f file
-v verbose
-C to directory

[code]tar -xzf archive.tar.gz[/code]
[code]tar -xzf archive.tar.gz -C some/directory/[/code]
[b][url=http://linux.die.net/man/1/unzip]unzip[/url][/b]

-q quiet
-o overwrite
-d extract to directory 

[code]unzip -qo archive.zip[/code]
[code]unzip -qo archive.zip -d some/directory/[/code]
[b]screen[/b]

Send a command to a running screen and window of choice.

[code]screen -S screen-name -p 0 -X exec your-command-goes-here[/code]
[code single]-S[/code] screen-name you want to match
[code single]-p[/code] number of the screen window, 0 in this case sends it to the first.
[code single]exec[/code] some-command

When using [b]screen[/b] give the window a name by using [b]-S[/b] for easier management. The word after the [b]-S[/b] is the name of the window, in this case rtorrent.

This will attach to a screen with this name:

[code]screen -S rtorrent rtorrent[/code]
This will attach to a screen with this name or create it if it doesn't:

[code]screen -R rtorrent rtorrent[/code]
Will start the selected process in the background as a daemon and detach from it immediately:

[code]screen -dmS rtorrent rtorrent[/code]
[b][url=http://linux.die.net/man/1/kill]kill[/url][/b]

[code]kill -9 PID[/code]
[b][url=http://linux.die.net/man/1/killall]killall[/url][/b]

[code]killall -9 -u $(whoami) processname[/code]
[b]Use [b]TAB[/b] to autocomplete parts of your SSH commands.[/b]

For example: if I am in my home folder and I wish to go to my 

[code]~/private/rtorrent[/code]
I can do this

[code]cd ~/p [b]TAB[/b][/code]
Which will give me this:

[code]~/private/[/code]
Unless I have more than one folder starting with [b]p[/b]. then I must give a second or third letter depending on how they conflict. In this case I do not have a conflicting folder name.

Then if I do:

[code]cd ~/private/r [b]TAB[/b][/code]
I will end up with this:

[code]cd ~/private/rtorrent/[/code]
So now I press enter. I have now used TAB to auto-complete parts of my [b]cd[/b] command.

[b]github url shortening[/b]

[url=http://git.io/]http://git.io/[/url]

[url=https://github.com/blog/985-git-io-github-url-shortener]git-io-github-url-shortener[/url]

You can do it in SSH using this command.

[code]curl -i http://git.io -F "url=YOU.URL.HERE"[/code]
[b]Chaining Commands[/b]

The use of [code single]&&[/code] will move to the next command if the previous command was successful.

[code]cd ~/private && mkdir test && cd test[/code]
So if the directory [code single]~/private[/code] did not exist the command would stop at the point where a single command did not execute successfully.

The use is [code single];[/code] will just chain a series of commands. 

[code]cd ~/private; mkdir test; cd test[/code]
Here it will just do command one then execute the next until it reaches the end. So if [code single]~/private[/code] did not exist the command would create the [code single]test[/code] folder in the wrong place.

[b]Run a process and send it to the background.[/b]

if you add a [code single]&[/code] to the end of your command it will be sent to the background as your run it.

[code]./some/path/to/a/binary &[/code]
[h3]Crontab[/h3]
To edit your crontab:

[code]crontab -e[/code]
To execute a bash script from crontab you need to use this command:

[code]bash -l[/code]
For example:

[code]@reboot bash -l ~/myscript.sh[/code]
You can use this command to easily create a cronjob for users in some sort of support capacity:

[code](crontab -l ; echo "* * * * * some/cron/thing") |uniq - | crontab -[/code]
This will create a specified cronjob while also checking to make sure it is not created more than once. So with a single command you can have create and insert a cronjob for a user. It only checks vs the last entry though.



