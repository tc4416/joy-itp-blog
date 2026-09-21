---
title: "UndNet: Week1"
---
### Lecture
#### [Network Definition and Dynamics](https://itp.nyu.edu/classes/undnet/geography-of-the-internet/)
A network is a collection of things connected to each other, The internet is just one of many networks.
##### Topologies of Networks
<div align="center">
<img src="/media/und/network1.png" width="200">
<img src="/media/und/network2.png" width="200">
<img src="/media/und/network3.png" width="200">
</div>

##### Link Density
"The greater the density of links in a network, the more possible paths there are for the message to get through to the end point, and the less critical any node is to the functioning of the network. "
Complete networks: <br> $$links = (n^2-n)/2 $$
##### OSI Model
<div align="center">
<img src="/media/und/osichart.png" width="400">
</div>

A router on an IP network is a device which defines the network and the range of addresses assigned to other devices when they’re connected to that network. In doing so, it also defines the maximum number of devices on the network. For example, a router might give itself the address 10.0.0.1, and then define that all other devices on that network get addresses from 10.0.0.2 to 10.0.0.255.

Routers use **Address Resolution Protocol (ARP)** to associate a device’s MAC address (from the datalink layer) with an available IP address. When a new device connects to a network, it announces its MAC address and requests an IP address.

----
### Setting up a host
Followed the [guide](https://itp.nyu.edu/networks/setting-up-a-virtual-host/) and everything went smoothly. I ran into this when i ran 
`sudo apt upgrade` I chose the highlight option because I think that was the default setting and perhaps the right things to do?

<div align="center">
<img src="/media/sudo-update.png" width="400">
</div>
Then set up the firewall by following [this guide](https://itp.nyu.edu/networks/setting-up-a-firewall-on-an-embedded-linux-device/)

<div align="center">
<img src="/media/firewall.png" width="400">
</div>

##### IPTABLE Firewall
not sure changing device ip how + my router ip

<div align="center">
<img src="/media/firewall_IP.png" width="400">
</div>
I took out `-A INPUT -s _192.168.0.1_/32 -i tcp -p tcp -m tcp --dport 22 -j DROP` because I'm not sure I understand it. *"This prevents ssh logins from outside your local network. Change the IP address to the address of your router.  If you’re operating in an institution with multiple networks like ITP, this rule might prevent you from logging into your device, if your computer and your device are on different local networks. If so, delete it."*

<div align="center">
<img src="/media/invalidIP.png" width="400">
</div>

I missed the line in the tutorial that said install both ufw and iptables can be troublesome, so I installedn them and was blocked out of my server. After some trouble shooting and recreate a droplet  and only install ufw, I was able to get it working.

### firewall log

<div align="center">
<img src="/media/firewall-log1.png" width="400">
<img src="/media/firewall-log2.png" width="400">
</div>


^ searching specific ip address
important command:

```
sudo ls /var/log    #check file
sudo wc -l /var/log/ufw.log
sudo tail -3 /var/log/ufw.log
sudo cat /var/log/ufw.log
sudo cat /var/log/ufw.log | grep '64.62.197.125'
sudo cat /var/log/ufw.log | grep '64.62.197.125' | wc -l
sudo tail -10 /var/log/ufw.log | sed -e 's/\s/\t/g'

sudo grep -o 'SRC=[0-9.]*' /var/log/ufw.log | sort -u | wc -l
```
I didn't figured out my server setup until Monday so only get to run it for a little bit before I do this analysis. Even though it is not run over 24 hour, there is still a lot of data. 

- **Blocked Connections:** 3003
- **Number of Unique IPs:** 1551 
- **Most attempts from one IP:** 62 attempts
- **Most attempt IP Address**: 77.239.124.128
- **Location of said IP:** Kerkrade, Limburg, The Netherlands (I tried a few online ip address lookup service and some of them gave me the location at Lauterbourg, France)
-  **Time:** all 62 attempts were made between 12am - 5am UTC time, September 15. The earliest was  12:34 AM and the last entry was 4:38 AM. 

Since my server is still pretty new, I couldn't really get to analyze if any ip adrress tried to access my server regularly. I tried to look up the organization name "ROCKET & MARINICA LTD" and found out that they are registered in London and was recently incorporated on 15, July 2026. The description the nature of business is "data processing, hosting and related activities". The company lookup website also show me a person Name Raul Gabriel Ghita as Director. I look him up and the first thing pop up is a post talking about this person might be a scammer LOL. [post link](https://lowendtalk.com/discussion/218476/concern-regarding-ghita-raul-the-scammer-nordic-vm-takehost-more-sponsorship-at-ronog) I am not hundred percent sure if I understand the whole situation about Raul and his shell companies, but it is interesting. I am guess the attempts were made by some sort of bot or scanner.

<div align="center">
<img src="firewall-log3.png" width="400">
<img src="firewall-log4.png" width="400">
<img src="firewall-log5.png" width="400">
<img src="firewall-log6.png" width="400">
</div>

------
### Reading

**_How Infrastructure Shapes Us_ by Deb Chachra**
> One definition of _infrastructure_ is that it’s all the underlying systems whose presence we take for granted when we start on something new.

> Networks are intrinsically collective

> It’s a myth that we make individual decisions about how we equip our buildings and homes; any decision we make is embedded in the social and technological standards of these shared systems, in other decisions that have already been made.

> Eliel Saarinen famously wrote, “Always design a thing by considering it in its next larger context—a chair in a room, a room in a house, a house in an environment, an environment in a city plan.” Focusing on individual-level action for infrastructural systems is a lot like considering a chair in isolation, or maybe like considering it in the context of a city plan: You might just end up with a bunch of chairs in an empty lot, purchased and placed there by the people who can afford to buy chairs.

**_Why Google Went Offline Today and a Bit about How the Internet Works_**
**_We finally know what caused the global tech outage – and how much it cost_**


##### Other Links
[ieee.org](ieee.org) : IEEE802.3