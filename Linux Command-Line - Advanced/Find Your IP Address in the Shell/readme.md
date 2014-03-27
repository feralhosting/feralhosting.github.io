
Find your IP Address in SSH
---

**To find the IP address for your server, use this command:**

This command will show you your IPv4 address.`-i` is for IP addresses for the host name:

~~~
hostname -i
~~~

This shows the hostname and `IPv6` address:

~~~
host $(hostname)
~~~

External checks on the slot vis SSH
---

[http://icanhazip.com/](http://major.io/icanhazip-com-faq/)

This is an external check and will return your IPv4 address.

~~~
curl -4 icanhazip.com
~~~

This is an external check and will return your IPv6 address.

~~~
curl -6 icanhazip.com
~~~

Checking via IRC 
---

[https://www.feralhosting.com/chat](https://www.feralhosting.com/chat)

In IRC do this command:

~~~
$ip servername
~~~

Where `servername` is the name of your server.

~~~
$ip aphrodite
~~~

Returns:

~~~
aphrodite.feralhosting.com resolves to 185.21.216.161                                                                                                                                                                              
aphrodite.feralhosting.com resolves to 2a04:1980:3100:1aac:21b:21ff:feda:4d53 (IPv6)
~~~

Checking from your home location:
---

Alternatively, you can just simply use the **ping** command from any computer:

**Important note:** When running this command in Windows, press and hold the [windows logo key and press R](http://support.microsoft.com/kb/126449) to bring up the run dialogue then type `cmd`.

~~~
ping server.feralhosting.com
~~~

**Example:**

~~~
ping aphrodite.feralhosting.com
~~~

The output will be your server's IP address, and some other information.

Since this is GNU/Linux, there are many ways to to the same thing and here is one more way.

~~~
host server.feralhosting.com
~~~

 
Replace server with your server name.

**Example:**

~~~
host rabbit.feralhosting.com
rabbit.feralhosting.com has address 85.17.27.70
~~~

Notes:
---

Also, if you have OpenVPN installed on your slot, the IP given for OpenVPN on your [Software Status page](https://www.feralhosting.com/heron/manager/software/) is the IP address of your server.



