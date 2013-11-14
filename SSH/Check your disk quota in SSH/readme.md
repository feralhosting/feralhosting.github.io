
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)

### The easy way

Run the below command in SSH, it will output your disk usage.

~~~
du -s --si ~/
~~~

For a list, sorted by size, of the files/folders in the current directory use:

~~~
du -s --si * | sort -h
~~~

### The prettier way

![](http://idzr.org/w7tn?.png)

**Step 1:** SSH into your slot.

First, run the command the matches your slot type, then move to Step 2:
  
For instance, for a `Helium-4` run you would run `echo '400000' >> ~/.quotaspace`

Helium-3

~~~
echo -n '333000' > ~/.quotaspace
~~~

Helium-4
 
~~~
echo -n '400000' > ~/.quotaspace
~~~

Helium-5

~~~
echo -n '500000' > ~/.quotaspace
~~~

Neon-3

~~~
echo -n '500000' > ~/.quotaspace
~~~

Neon-4 

~~~
echo -n '600000' > ~/.quotaspace
~~~

Neon-5

~~~
echo -n '750000' > ~/.quotaspace
~~~

Argon-3

~~~
echo -n '666000' > ~/.quotaspace
~~~

Argon-4

~~~
echo -n '800000' > ~/.quotaspace
~~~

Argon-5

~~~
echo -n '1000000' > ~/.quotaspace
~~~

Xenon-3

~~~
echo -n '1000000' > ~/.quotaspace
~~~

Xenon-4

~~~
echo -n '1200000' > ~/.quotaspace
~~~

Xenon-5

~~~
echo -n '1500000' > ~/.quotaspace
~~~

Radon

~~~
echo -n '3000000' > ~/.quotaspace
~~~

**Step 2:** After SSHing into your slot, run the following the commands

~~~
mkdir -p ~/bin
wget -qO ~/bin/quota http://git.io/FolBxw
chmod 700 ~/bin/quota
source ~/.bashrc && source ~/.profile
~~~

Now running the command:

~~~
quota
~~~

In SSH will give you your disk quota.



