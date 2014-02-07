
Ghost Blogging Platform
---

**Important note:** You will need to have installed `node.js` to use Ghost. See this FAQ - [node.js - How to install](http://https://www.feralhosting.com/faq/view?question=199)

Installation:
---

~~~
wget -qO ~/ghost.zip https://ghost.org/zip/ghost-0.4.1.zip
unzip -qo ~/ghost.zip -d ~/ghost
cd ~/ghost
npm install --production
~~~

Configuration:
---

Now we need to edit this file:

~~~
~/ghost/config.example.js
~~~

Using SSH:

~~~
nano -w ~/ghost/config.example.js
~~~

The file is broken up into sections. The default section is the `Development` section. This is what we edit first.

Find this:

~~~
// The url to use when providing links to the site, E.g. in RSS and email.
url: 'http://my-ghost-blog.com',
~~~

Edit it to match your server URL and add the `/blog/` subdirectory

~~~
// The url to use when providing links to the site, E.g. in RSS and email.
url: 'http://server.feralhosting.com/username/blog/',
~~~

Find this:

~~~
server: {
    // Host to be passed to node's net.Server#listen()
    host: '127.0.0.1',
    // Port to be passed to node's net.Server#listen(), for iisnode set this to process.env.PORT
    port: '2368'
}
~~~

Change the host to `0.0.0.0` and choose a port between the ranges `6000` - `50000`

~~~
server: {
    // Host to be passed to node's net.Server#listen()
    host: '0.0.0.0',
    // Port to be passed to node's net.Server#listen(), for iisnode set this to process.env.PORT
    port: '23684'
}
~~~

Proxypass URLS with Apache or Nginx.
---

### Apache:

Create a new blank file using this command:

~~~
nano ~/.apache2/conf.d/ghost.conf
~~~

**Important note:** Do not forget to change the `PORT` to the same port as used by Ghost.

Now we will copy and paste the below code into this file, making sure to customise the `PORT` to match that used by Ghost:

~~~
Include /etc/apache2/mods-available/proxy.load
Include /etc/apache2/mods-available/proxy_http.load

ProxyRequests Off
ProxyPreserveHost On

ProxyPass /blog http://10.0.0.1:PORT/${USER}/blog
ProxyPassReverse /blog http://10.0.0.1:PORT/${USER}/blog
~~~

Once you have copied and pasted this then press and hold `CTRL` and then press `x` to save. Press `y` to confirm. Now you can reload the conf like this:

~~~
/usr/sbin/apache2ctl -k graceful
~~~

### Nginx:

~~~
nano ~/.nginx/conf.d/000-default-server.d/ghost.conf
~~~

We are going to copy and paste this once it is edited:

~~~
location ^~ /blog {
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header Host $http_x_host;
	proxy_set_header X-NginX-Proxy true;

	rewrite /(.*) /username/$1 break;
	proxy_pass http://10.0.0.1:PORT/;
	proxy_redirect off;
}
~~~

But before we do this we are required to edit these two lines:

~~~
rewrite /(.*) /username/$1 break;
proxy_pass http://10.0.0.1:PORT/;
~~~

Change:

1: `username` in the `rewrite /(.*) /username/$1 break;` to your Feral username 
2: `PORT` in the `proxy_pass http://10.0.0.1:PORT/;` to the port you configured in the `~/ghost/config.example.js`

Then copy and paste this into the file.

Press and hold `CTRL` and then press `x` to save. Press `y` to confirm.

Now reload the nginx conf files for the change to take effect using this command:

~~~
/usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf
~~~

Running Ghost:
---


Now we are ready to start Ghost:

~~~
screen -S ghost
cd ~/ghost
npm start
~~~

Now once it has loaded  you will see something like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Software/Ghost%20Blogging%20Platform/1.png)

Then press and hold `CTRL` and `a` then press `d` to detach from the screen. This leaves it running in the background.

You should now be able to visit the URL where `username` if your Feral username and `server` if the name of the server that the relevant slot is hosted on.

**Important note:** https works fine so you can use the https URL.

~~~
https://server.feralhosting.com/username/blog/
~~~

Visit this URL to configure your admin account.

~~~
https://server.feralhosting.com/username/blog/ghost
~~~



