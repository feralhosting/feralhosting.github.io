What is flask? [http://flask.pocoo.org/](http://flask.pocoo.org/)

This tutorial will help you to upgrade from Apache to Nginx. Install uWSGI and make a flask test app.

**Step 1:** Upgrade to nginx: [https://www.feralhosting.com/faq/view?question=231](https://www.feralhosting.com/faq/view?question=231)

**Step 2:** Run the following commands to install Pip, Flask and uWSGI:

~~~
easy_install --user pip
~/.local/bin/pip install --user flask uwsgi
~~~

**Step 3:** Create file and put the following code into it.

Create this file: `~/.nginx/conf.d/000-default-server.d/**uwsgi**.conf`

~~~
echo -n '' > ~/.nginx/conf.d/000-default-server.d/**uwsgi**.conf
~~~

Put the following code into the file:

~~~
location = /**foo** { rewrite ^ /**foo**/; }
location /**foo** { try_files $uri @theapp; }
location @theapp {
   include /etc/nginx/uwsgi_params;
   uwsgi_param SCRIPT_NAME /**foo**;
   uwsgi_modifier1 30;
   uwsgi_pass unix:/media/**<your diskname>**/home/**<your username>**/**foo**.sock;
}
~~~

Remember to put in your username and change from `foo` to your projectname

Restart the nginx server:

~~~
/usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf
~~~

**Step 4:** Make uWSGI start automatically each time the server boots.

Run the following code in the terminal:

~~~
crontab -e
~~~

This will open up or create your Crontab config file. Now add this line:

~~~
@reboot uwsgi --socket /media/**<your diskname>**/home/**<your username>**/**foo**.sock --wsgi-file /media/**<your diskname>**/home/**<your username>**/**foo**/**main.py** --master --processes 4 --threads 0 --enable-threads 1 --callable app --daemonize2 /media/**<your diskname>**/home/**<your username>**/.nginx/uwscgi.log
~~~

Then run the following code to start it instantly:

~~~
uwsgi --socket /media/**<your diskname>**/home/**<your username>**/**foo**.sock --wsgi-file /media/**<your diskname>**/home/**<your username>**/**foo**/**main.py** --master --processes 4 --threads 0 --enable-threads 1 --callable app --daemonize2 /media/**<your diskname>**/home/**<your username>**/.nginx/uwscgi.log
~~~

**Step 5:** Make the flask project testfile.

Create this file (mentioned in step4): `/media/**<your diskname>**/home/**<your username>**/**foo**/**main.py**` then put in the following flask code (python):

~~~
#!/usr/bin/env python2
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
  return "Hello World!"

if __name__ == "__main__":
  app.run()
~~~

**Step 5:** Open your favorite browser and go to `http://**<your username>**.gaia.feralhosting.com/**foo/**`

**IRC help:**

Questions regarding your slot: #Feral @ irc.what-network.net
Questions regarding Flask: #Pocoo @ Freenode
Questions regarding uWSGI: #uWSGI @ Freenode
Questions regarding nginx: #nginx @ Freenode



