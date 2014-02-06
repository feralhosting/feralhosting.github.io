
etherpad-lite install
---

Prerequisites of using etherpad-lite

1: You will need to have updated to [nginx](https://www.feralhosting.com/faq/view?question=231)

2: You have installed [node.js](https://www.feralhosting.com/faq/view?question=199)

Once you have done these two thing then you can install and use Ghost.

Installation:
---

~~~
npm install sqlite3
git clone https://github.com/ether/etherpad-lite.git
~~~

~~~
cp -f ~/etherpad-lite/settings.json.template ~/etherpad-lite/settings.json
~~~

Now edit this file:

~~~
nano -w ~/etherpad-lite/settings.json
~~~

Find and make these changes:

**1:**

~~~
//IP and port which etherpad should bind at
"ip": "0.0.0.0",
"port" : 9001,
~~~

Change the port. Anything between `6000` to `50000`

~~~
//IP and port which etherpad should bind at
"ip": "0.0.0.0",
"port" : 12874,
~~~

**2:**

~~~
"sessionKey" : "",
~~~

Add a session key. Just generate some letters and numbers.

~~~
"sessionKey" : "NGTpvziaR5SZQ2jqd7Vf",
~~~

**3:**

~~~
"dbType" : "dirty",
//the database specific settings
"dbSettings" : {
               "filename" : "var/dirty.db"
             },
~~~

Change the database settings. I use sqlite3, but you can use redis:

~~~
"dbType" : "sqlite",
//the database specific settings
"dbSettings" : {
               "filename" : "var/sqlite.db"
             },
~~~

**4:**

~~~
  /*
  "users": {
    "admin": {
      "password": "changeme1",
      "is_admin": true
    },
    "user": {
      "password": "changeme1",
      "is_admin": false
    }
  },
  */
~~~

Uncomment this section and change the passwords:

~~~
  "users": {
    "admin": {
      "password": "fwe5235f3",
      "is_admin": true
    },
    "user": {
      "password": "EGFSD215TF",
      "is_admin": false
    }
  },
~~~

Start etherpad

~~~
screen -S etherpad ~/etherpad-lite/bin/run.sh
~~~

If all goes well then press and hold `CTRL` and `a` then press `d` to detach from the screen. This leaves it running in the background.

Update etherpad
---

~~~
screen -r etherpad
~~~

Then press and hold `CTRL` and then press `c` to quit.

~~~
cd ~/etherpad-lite
git pull origin
screen -dmS etherpad ~/etherpad-lite/bin/run.sh
cd
~~~

### Optional 

**Apache**

To use https you create your own certs, then uncomment the relevant section in the `settings.json`. Then add the relative paths to your certs.

~~~
mkdir -p ~/etherpad-lite/ssl
openssl req -new -x509 -nodes -days 365 -subj '/C=GB/ST=none/L=none/CN=none' -newkey rsa:2048 -keyout ~/etherpad-lite/ssl/etherpad.key.pem -out ~/etherpad-lite/ssl/etherpad.cert.pem
~~~


~~~
  /*  
  // Node native SSL support
  // this is disabled by default
  //
  // make sure to have the minimum and correct file access permissions set
  // so that the Etherpad server can access them

  "ssl" : {
            "key"  : "/path-to-your/epl-server.key",
            "cert" : "/path-to-your/epl-server.crt"
          },

  */
~~~

Becomes:

~~~
  // Node native SSL support
  // this is disabled by default
  //
  // make sure to have the minimum and correct file access permissions set
  // so that the Etherpad server can access them

  "ssl" : {
            "key"  : "ssl/etherpad.key.pem",
            "cert" : "ssl/etherpad.cert.pem"
          },
~~~

**Nginx**

In ngnix we can use proxypass to work with the existing and valid SSL URL format. These two lines must be edited in the template conf below:

~~~
rewrite ^/ether$ https://$http_x_host/username/ether/ permanent;
proxy_pass http://10.0.0.1:PORT/username/ether/;
~~~

Change the `username` in two places and `PORT` in one, to match yours. Where `username` if your Feral username and the port is the same port configured in the `~/etherpad-lite/settings.json`

~~~
location /ether {
    proxy_set_header        Host            $http_x_host;
    proxy_set_header        X-Real-IP       $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    rewrite ^/ether$ https://$http_x_host/username/ether/ permanent;
    rewrite /ether/(.*) /$1 break;
    proxy_pass http://10.0.0.1:PORT/username/ether/;
    proxy_redirect / /ether/;
    proxy_redirect off;
    proxy_buffering off;
}
~~~

Once you have saved this file use this command to reload nginx:

~~~
/usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf
~~~

**Admin**

~~~
https://server.feralhosting.com/username/ether/admin/plugins
~~~