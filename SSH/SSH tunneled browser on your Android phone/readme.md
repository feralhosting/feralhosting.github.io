Android users probably know that setting up SSH tunnels on non-rooted Android phones is a pain in the ass and more trouble than it is worth. I've found a relatively simple method that allows you to secure your browsing. A few notes before we start:

a) You cannot setup an all-encompassing SSH tunnel without rooting your phone. This guide explains how to configure a browser (Firefox) to use your SSH session opened with a free app (ConnectBot) without incurring the risk of rooting. This will only protect your browsing.

b) If you already have a rooted phone, there are easier ways of getting this done. Google it up.

Here are the steps.

1: Install Firefox 

~~~
https://play.google.com/store/apps/details?id=org.mozilla.firefox
~~~

2: Install ConnectBot 

[Set up Connect Bot private/public keys](http://michaelchelen.net/articles/android-connectbot-ssh-key-auth-howto.html)

~~~
https://play.google.com/store/apps/details?id=org.connectbot
~~~

3: Login into your server through ConnectBot. Press your menu button and access Port Forwards. Setup a port forward with a destination of 127.0.0.1 (localhost doesn't seem to work) and with a higher port than normal, as you are running without root, and most ports are restricted. A good number is 9000-10000.

4: Open Firefox, and type `about:config` into the destination bar. Access and modify the following properties:

~~~
network.proxy.socks = 127.0.0.1
network.proxy.socks_port = <whatever port you chose>
network.proxy.type = 1
network.proxy.socks_remote_dns = “true” (press toggle to change the value)
~~~

5: Restart Firefox, and open any IP identifying website (http://www.whatismyip.com/ for instance). If all is correct, you should see your server IP instead of whatever your phone is using. Congrats.

