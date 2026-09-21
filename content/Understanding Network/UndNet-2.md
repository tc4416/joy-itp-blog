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
- china-airline.com
I was stalking [Nasif's blog](https://itp.nasif.co/classes/networks/) for this class and noticed that he was using `traceroute -a` to analyze the network hopping. After searching it up, I learned that AS number (ASN) are **unique identifier to a network or collection of networks under a single administrative control** , which is good know.
<div align = "center">
<img src = "/media/und/traceroute1.png">
<img src = "/media/und/traceroute2.png">
</div>

So I decided to extract both the ASN and IP address for analyzing the AS provider and for mapping the network hops. I use `traceroute -an google.com | grep -oE '\[AS[0-9]+\] [0-9.]+'` and it gives me something like this: 

<div align = "center">
<img src = "/media/und/traceroute3.png" width = 200px>
<figcaption>Traceroute output: google.com</figcaption>
<img src = "/media/und/traceroute4.png" width = 200px>
<figcaption>Traceroute Map: Google.com.</figcaption>
<img src = "/media/und/traceroute5.png" width = 200px>
<figcaption>Traceroute output: instagram.com</figcaption>
<img src = "/media/und/traceroute6.png" width = 200px>
<figcaption>Traceroute Map: instagram.com</figcaption>
<img src = "/media/und/traceroute7.png" width = 200px>
<figcaption>Traceroute output: airbnb.com</figcaption>
<img src = "/media/und/traceroute8.png" width = 200px>
<figcaption>Traceroute Map: airbnb.com</figcaption>
<img src = "/media/und/traceroute9.png" width = 200px>
<figcaption>Traceroute output: are.na</figcaption>
<img src = "/media/und/traceroute10.png" width = 200px>
<figcaption>Traceroute Map: are.na</figcaption>
<img src = "/media/und/traceroute11.png" width = 200px>
<figcaption>Traceroute output: china-airline.com</figcaption>
<img src = "/media/und/traceroute12.png" width = 200px>
<figcaption>Traceroute Map: china-airline.com</figcaption>
</div>

I found it a little odd that I had so many [AS0] across these traceroutes, and the routes seemed to end quite quickly. So I suspected my method was not working well and that it skipped the lines without an ASN. So I went back to see the full traceroute with just traceroute google.com and the other websites. Except for google.com and are.na, all the other websites got stuck at * * * and didn't reach the destination. Instagram and Airbnb stalled in lower Manhattan, and China Airlines got one hop to the Netherlands and stopped there.

<div align = "center">
<img src = "/media/und/traceroute13.png" width = 350px>
<figcaption>Traceroute output: google.com</figcaption>
<img src = "/media/und/traceroute14.png" width = 350px>
<figcaption>Traceroute output: are.na</figcaption>
</div>Then I also checked who own the AS from the ASN list that I got