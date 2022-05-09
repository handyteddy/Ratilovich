---
layout: post
title:  "Securely Self-Hosting a Website"
date:   2020-12-21
categories: guide pfsense hosting security
---
## Securely Self-Hosting a Website
I'm using [Github Pages](https://pages.github.com/) to host this site for a few reasons, but namely that:
 - Since this is a static site, using Github is free and reliable
 - I don't want to expose my home network any more than I have to
 - It's about time I learned how Git works
 
Admittedly, however, I *am* hosting a few unrelated basic websites from my server in my home network. After some trial and error I made a setup secure enough for me to feel confident in keeping it running. It's nothing too complicated, but it helps me sleep better at night.
<br>
## 1. Cloudflare

I'm a huge fan of Cloudflare, and it isn't hard to see why for anyone remotely interested in self-hosting. Their free protection will proxy my IP address, that way any DNS query will go through Cloudflare's servers without directly revealing my public IP address. This will allow me to make sure a simple DNS query won't give someone the info they need to port scan my router or geolocate me. (Not make it impossible! But at least more difficult.) However, Cloudflare alone won't prevent the site from being accessed directly by my public IP address. It does a great job with proxying my DNS, but when it comes to protecting my actual home network, I'm not in the clear just yet.
<br>
## 2. Nginx 

With DNS secured, it's time to make sure I'm adequately defending my home network from an adversary that already has or has found my home network's public IP address. I'll start with my web server.

I will always use Nginx over Apache given the choice, in part because of how much simpler I find configuration. Disallowing access to my websites from an IP address is as easy as a simple server block.

{% highlight nginx %}
server {
    listen      80 default_server;
    listen      [::]:80 default_server;
    server_name "";
    return      444;
}
{% endhighlight %}

With this new directive, the client never sees the 444 error and Nginx will close a connection from a direct IP address, or really, anything that isn't specifically identified in a different server block. However, I could still do better than having the connection closed at my server. I'll take this one step further and adjust my pfSense settings.
<br>
## 3. pfSense

All of the traffic coming in to my network to a web server will be coming from Cloudflare. So why not *only allow Cloudflare source IP addresses access to these ports*? This way, the only way to access my website will be to use public DNS servers to go through Cloudflare's proxied DNS. 
<br>
This too is pretty simple. In pfSense, I simply create an alias with Cloudflare's IP addresses (which they [so generously provide](https://www.cloudflare.com/ips/)) and [adjust my NAT port forwarding rules for TCP port 80 and 443]({% link /assets/images/20201221_1.jpg %}) to specify that only those source IPs can connect to my WAN address. And just like that, now if I try to go to my public IP address from my phone on mobile data, my router drops the connection as opposed to trusting Nginx to.
<br>
Without this configuration, in theory, if someone suspected both my public IP address and a domain I'm hosting, they could configure their hosts file to point my domain directly to my IP address. Nginx wouldn't know any different and would serve the website, thus revealing to the adversary that that is, in fact, my IP. This may be a bit of a stretch; the real practical reason for doing this is that I want to end a connection that I want nothing to do with as far away from my actual devices as possible, and it doesn't get much further than my public-facing firewall.
<br>
It could be argued that this makes the Nginx setup moot, but hey, isn't that a sign of good defense in depth?
<br>
## Conclusion

At the end of the day, the most secure way to host for my home network will be to rent a cheap Vultr or Linode VPS. However, when I have the hardware, the patience for sysadmin-ing, and plenty of quarantine time to put it all together, it's worth it to me to save a few bucks and self-host with plenty of security precautions.