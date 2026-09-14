---
title: UndNet-1
---
### Lecture
#### [Network Definition and Dynamics](https://itp.nyu.edu/classes/undnet/geography-of-the-internet/)
A network is a collection of things connected to each other, The internet is just one of many networks.
##### Topologies of Networks
<div align="center">
<img src="/media/network1.png" width="200">
<img src="/media/network2.png" width="200">
<img src="/media/network3.png" width="200">
</div>

##### Link Density
"The greater the density of links in a network, the more possible paths there are for the message to get through to the end point, and the less critical any node is to the functioning of the network. "
Complete networks: <br> $$links = (n^2-n)/2 $$
##### OSI Model
<div align="center">
<img src="/media/osichart.png" width="400">
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

**IPTABLE Firewall**
not sure changing device ip how + my router ip

<div align="center">
<img src="/media/firewall_IP.png" width="400">
</div>
I took out `-A INPUT -s _192.168.0.1_/32 -i tcp -p tcp -m tcp --dport 22 -j DROP` because I'm not sure I understand it. *"This prevents ssh logins from outside your local network. Change the IP address to the address of your router.  If you’re operating in an institution with multiple networks like ITP, this rule might prevent you from logging into your device, if your computer and your device are on different local networks. If so, delete it."*
![[Pasted image 20260913165940.png]]


<div

### What is the internet?
- Autonomous System
- Inter-Exchange Providers(IXP)
		<br>Meet me room
- Network Types
	- Centralized 
	- Decentralied
	- Distributed
- Network Topologies
	- Fully-connected
	- star
	- Bus
	- Ring
- Link Density
	- Complete networks: <br> $$links = (n^2-n)/2 $$
- Open Systems Interconnect (OSI) Network Model
	<br>"Please do not throw sausage pizza away"
	- Application
		- Uses or generates network data from user activitis
	- Presentation
		- Handle the formatting and presentation of incoming data to application
	- session
		- manage the connection sender and receiver
	- Transport
		- manage type of transmission, order of packets recid
	- Network
		- Handle address and trafic management between networks
	- Data Link
		- manages traffic on the physical transmission
	- Phyiscal
		- fiber optics, cipper, radio etc.

##### Other Links
[ieee.org](ieee.org) : IEEE802.3

