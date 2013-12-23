
The steps will similar for any other domain name provider. The DNS settings and tools may differ from place to place but the basic idea is the same anywhere you go.

**STEP 1:** Register Your Domain Name through a registrar.

The best option to it register a top level domain such a `.com` or `.co.uk` (depending on your region). If the privacy of domain registration is an issue that is something you must consider before linking your domain to your Feral account. Once you are in control of a valid domain proceed with the guide.

**STEP 2:** Obtain the IP of Your Feral Server to configure your DNS settings.

You need this IP of your Feral slot in order to configure the DNS settings/Records.

You can get this information using SSH. [SSH to your server](https://www.feralhosting.com/faq/view?question=12), and type:

~~~
hostname -i
~~~

or in IRC do, where `servername` is the name of your server:

~~~
$ip servername
~~~

For example:

~~~
$ip pontus
~~~

Take note of your server's IP address, as you will need in the next step.

**STEP 3:** Configure Your Domain Name using DNS settings:

The DNS settings of any domain are controlled by the host of the Name Servers. If you have changed the name servers at some point you must use their DNS manager to configure the DNS records. By default you names servers should be controlled by the registrar post registration.

**Important note:** Feral does not provide or manage name servers.

Optionally, for this FAQ I recommend using this DNS service: [http://rage4.com/](http://rage4.com/) - See this page for namerserver settings - [Nameservers](http://gbshouse.uservoice.com/knowledgebase/articles/107710-rage4-dns-frequently-asked-questions-faq-)

Your domain registrar or name server host will provide you with basic or advanced tools (a DNS records editor) to manage your DNS settings for each domain they are managing the name servers for. Find their DNS Settings Manager or similar and then we are going to two main records for this domain. The first is an `A` record for the main IP and the second will be a `cname` for the `www` version. Click on the domain name you'd like to configure, and then click the `Manage DNS` or similar options.

We are going to create two new records for our custom domain. 1: an `A` record linking to the server IP and 2: a `CNAME` to redirect the `www` subdomain to the main A record

**Important note:** Some hosting providers will automatically create a `CNAME` for your www version, such a GoDaddy. In this case you should only need to create Record 1, the `A` record. 

**Record 1 A record:** `example.co.uk` pointing to `123.123.123.123`

**Record 2 CNAME record:** `www.example.co.uk` pointing to `example.co.uk`

Here are the example records we use for the `example.co.uk` domain.

**Record 1 A record:**

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Host%20a%20virtual%20host%20on%20your%20Feral%20slot/1.png)

**Host**: `example.co.uk`

**TTL**: `1H` or `3600`

**Type**: `A`

**Value**: The IP of your Feral server

Add this new Record.

**Record 2 CNAME record:**

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Host%20a%20virtual%20host%20on%20your%20Feral%20slot/2.png)

**Host**: `www.example.co.uk`

**TTL**: `1H` or `3600`

**Type**: `CNAME`

**Value**: `example.co.uk`

Add this new Record.

**Important Note:** Activating domains can take up to 24 hours while the DNS propagates fully. This is beyond Feral's control and you should consider changing your DNS servers if your ISP is taking too long to acknowledge the changes.

[Google DNS](https://developers.google.com/speed/public-dns/)

[Comodo DNS](http://www.comodo.com/secure-dns/)

[OpenDNS](http://www.opendns.com/)

**STEP 4: Add it to the Server**

After you're done with the above steps, simply create a new folder with the same name as the domain inside the `~/www` directory on your slot. All slots have this directory in their root location.

**Folder name:** `example.co.uk`

So you will have something that looks like this:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Host%20a%20virtual%20host%20on%20your%20Feral%20slot/3.png)

It should be added almost immediately and when it is, another folder "public_html" should be created inside of each folder.

The final directory structure will look something like:

~~~
/media/12345/home/username/www/example.co.uk/public_html/
~~~

When you visit your domain's URL in a browser you will be seeing any files that are inside the `public_html` directory.

Now visit your website URL in a browser. You may need to clear your browser cache in some case to see the change.



