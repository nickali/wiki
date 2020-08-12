---
description: Not exactly but sometimes a substitute can make life easier.
---

# Using Caddy as DNSMasq Replacment

My main laptop is 2013 Macbook Pro with 8GB of RAM. Using it as a dev environment on any sizeable project is ummm...challenging. But I love this Macbook and don't want to replace it.

 Unfortunately, there is already all sorts of crap installed that makes maintenance pure pain. VSCodium \(a couple of projects open\), Docker \(~10 containers\), and Firefox \(10 tabs / 2.8GB RAM\) are always up and grinding away.  Add more stuff seemed like nightmare. 

There was one environment issue that been driving me nuts. There are a couple of small docker containers that I need accessible when away from home. They host my calendars, contacts, bookmarks, todo lists, newsreader, and notebooks.

Now, assigning them a domain or subdomain using Duck DNS or a similar tool easily makes them accessible when away from home. But I wanted to use the same domain names while at home. This can get icky. Not all routers support devices needing talk to each other using their external addresses. The router needs to support either hairpinning or NAT loopbacks. 

There was also a second use case I needed to consider. I use a VPN to access the outside world when home. At the same time I want to access internal network machines. If I did nothing, when trying to access an internal machine while on VPN, everything would be routed through the VPN, back to Comcast, into my network, and come back in reverse. Crazy. There was already a Pi-hole container handling DNS internally. There must be a way to achieve traffic separation. What I needed was a WireGuard version of OpenVPN split tunelling. 

Let's just say my network layout is a hot mess with multiple VLANs routing traffic to different VLANs. Trying to set up hairpinning with the router sounded like a weekend of frustration that I didn't want to deal. 

So how do I deal with this? Searching, the most common and sensible solution was running dnsmasq locally. It could assign the local IPs I wanted to access and punt the rest of the DNS requests to the Pi-hole. Except, it meant keeping track of more environment changes and I didn't want to do that. 

Ok, how can I make this work without the fewest changes? What was the flow that needed to happen? The common denominator was internal name resolution needs to stay internal no matter what. So if I'm inside the network, I need to direct all DNS requests to the Pi-hole. The Pi-hole can translate the external IPs to internal IPs. The problem is the VPN. Once connected, the VPN will route DNS to its own servers. The only option I had with the VPN is that I could assign 127.0.0.1 as the nameserver. That is where dnsmasq could help.

Look at all the services I was already running in containers, it occurred to me that a reverse proxy would solve all my problems. Instead of using it as a front for web servers \(which I was already using it for\), I could have Caddy redirect DNS calls to my machine \(127.0.0.1 from the VPN\) to the Pi-hole. 

Easy peasy. Only a few lines need to be added to the Caddyfile\(\*\):

```text
127.0.0.1:53 {
   reverse_proxy <Pi-hole IP>:53
   keepalive 1h               // keep the connections open
   keepalive_idle_conns 10
}
```

Now the tunnel configuration file will probably require a small change. It should end up looking like:

```text
[Interface]
PrivateKey = <some random key>
Address = <CIDR version of IP>
DNS = 127.0.0.1 //<----- yup

[Peer]
PublicKey = <some random server key>
AllowedIPs = 8.0.0.0/7, 11.0.0.0/8, 12.0.0.0/6, 16.0.0.0/4, 32.0.0.0/3, 64.0.0.0/2, 128.0.0.0/3, 160.0.0.0/5, 168.0.0.0/6, 172.0.0.0/12, 172.32.0.0/11, 172.64.0.0/10, 172.128.0.0/9, 173.0.0.0/8, 174.0.0.0/7, 176.0.0.0/4, 192.0.0.0/9, 192.128.0.0/11, 192.160.0.0/13, 192.169.0.0/16, 192.170.0.0/15, 192.172.0.0/14, 192.176.0.0/12, 192.192.0.0/10, 193.0.0.0/8, 194.0.0.0/7, 196.0.0.0/6, 200.0.0.0/5, 208.0.0.0/4
Endpoint = <SERVER IP>:<SERVER PORT>
```

Two things to notice here. First, DNS gets set to the machine you are using.

Second, AllowedIPs is NOT set to the usual 0.0.0.0/0, ::/0. The zeros will forward all traffic, including DNS requests through tunnel. The VPN server won't be able to connect to itself to reply to DNS requests, so local requests can't be allowed through the tunnel. Unfortunately there is no exclude-type functionality, instead we have to list what IS allowed through the tunnel. Tedious, but it works. 

\_\_\_

\(\*\) If you haven't installed Caddy on a Mac using brew already, it can be hard to find where the Caddyfile is. It's located at /usr/local/etc/Caddyfile. 



