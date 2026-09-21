---
title: "UndNet: Week2, Traceroute"
draft: false
---
#### Lecture
- AS number vs IP Number
- [BGP(# Border Gateway Protocol)](https://itp.nyu.edu/networks/border-gateway-protocol-bgp/)
- check inet address at `ifconfig en0`, does it change everyday?
- traceroute: [traceroute mapper](https://stefansundin.github.io/traceroute-mapper/), works by multiple pings
- check out `curl`,`-v`, `-l`, `man`
- saving firewall log to file
copy from sever to local mochine
`scp  joychang@ipaddress: home/joychang/test/txt`

#### Reading

#### Traceroute Analysis (WIP)
For this assignment, I am only using my laptop terminal and not going into ssh. Definition in terminal manual: 
> **traceroute** – print the route packets take to network host

I am using traceroute for the following websites that I frequently visit:
- google.com
- instagram.com
- airbnb.com
- nyu.edu
- are.na
- youtube.com
- pinterest.com
I was stalking Nasif's blog for this class and noticed that he was using `traceroute -a` to analyze the network hopping. After searching it up, I learned that AS number (ASN) are **unique identifier to a network or collection of networks under a single administrative control** , which is good know.
<div align = "center">
<img src = "/media/traceroute1.png">
<img src = "/media/traceroute2.png">
</div>

So I decided to extract both the ASN and IP address for analyzing the AS provider and for mapping the network hops. I use `traceroute -an google.com | grep -oE '\[AS[0-9]+\] [0-9.]+'` and it gives me something like this: 
![[traceroute3.png]]