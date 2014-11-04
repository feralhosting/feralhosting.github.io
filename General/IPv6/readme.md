
We have begun testing IPv6 on our network and have introduced it to our servers. It runs alongside IPv4 and most of the time, will pick quietly whichever version is available.

The following services should be available: HTTP, FTP, SSH (including SFTP and SOCKS proxies) and DNS.

IPv6 is important as there is an [IP shortage](https://www.ripe.net/internet-coordination/news/announcements/ripe-ncc-begins-to-allocate-ipv4-address-space-from-the-last-8) preventing everyone from connecting to the Internet. Those most hit by this are providers such as ourselves who are relatively small and late to the IP-game; we are limited to 1,024 IPs for life. IPv6 allows us to expand this to practically, as many as required.

Once IPv6 is fully tested on our services, IPv6 will perform better than IPv4. In addition, if you only have a IPv4 address, you can get access IPv6 services by using a tunnel broker; then, if a particular broker causes speed issues, you can choose another.

This effectively allows you to actively workaround routing or congestion issues.

Getting connected
---

To get connected via IPv6 you should first check to see if your ISP supports IPv6. Some ISPs have begun rolling it out in a usable form.

Here are a list of ISPs that can get IPv6 with minimal fuss:

- AT&T: https://www.att.com/ipv6 / http://www.att.com/esupport/article.jsp?&sid=KB409112
- Comcast: http://comcast6.net/
- Free SAS
- QWest / CenturyLink: http://internethelp.centurylink.com/internethelp/modem-pk5001z-ipv6rd.html
- Videotron: http://support.videotron.com/residential/internet/ipv6

The list is short because it's new. If you find that your ISP provides IPv6, please [open a support ticket](https://www.feralhosting.com/manager/tickets/new) and we'll update this list.

Tunnel brokers
---

If your ISP does not offer any support for IPv6 then a tunnel broker can be set up instead. Tunnels are a way of sending IPv6 traffic over IPv4 but provides the flexibility of choosing which tunnel offers the best speeds.

Here are a few [tunnel brokers](https://en.wikipedia.org/wiki/List_of_IPv6_tunnel_brokers):

### Freenet6 (gogo6): http://www.gogo6.com/freenet6/tunnelbroker

* Multiple locations spread out across the world for alternative connectivity.
* Client is a simple download and run.
* Website is difficult to navigate.

### SixXS: https://www.sixxs.net/main/

* Provides a step-by-step guide (with pictures): https://www.sixxs.net/faq/account/?faq=10steps
* Many locations available for alternative connectivity.
* Requires a waiting period of at least a week to get activated.

### Hurricane Electric: https://tunnelbroker.net/

* Tier 1 ISP who are providing us with IPv6 connectivity.
* No activation time.
* Requires your router to forward protocol 41.

These services are essentially providing a free proxy to promote and increase IPv6 connectivity. They do ask for a lot of information prior to the set up to help avoid abuse of their service.

Welcome to the future
---

By connecting to IPv6 you greatly help us and the wider Internet out. In the future, IPv6 set up will be faster than IPv4.

Please let us know if you run into problems (setting up, poor speeds, etc) and we'll try to help.



