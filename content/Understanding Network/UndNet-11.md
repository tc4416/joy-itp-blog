---
title: "UndNet: Week 10"
draft: false
---
#### Other people's API
Jasmine's: I left messages on her service
<div align = "center">
<img src = "media/und/undnet7.png" width = 400px>
</div>
#### Microcontroller
**Finding Mac Address**
I only have a spare nano ESP32 on hand at this moment so I am using it as my device. I was having issue uploading my sketch to the board and it was driving me crazy lol. But after following the answer from the Arduino forum( connecting B1 and GN)

update: it still doesn't work and i had to use the Nano IOT 33 from shop i think my nano ESP32 is dead:((((

**Figured out the MAC address and register this Nano to the registration system**

<div align = "center">
<img src = "media/und/arduino1.png" width = 400px>
<img src = "media/und/undnet10.png" width = 400px>
</div>

**Try the HttpSimpleClient sketch**

<div align = "center">
<img src = "media/und/undnet3.png" width = 400px>
</div>

For the example code, I wasn't quite share where this html page came from.
I then tried to get request my server api but it returned an 403 error. I tried both sandbox & my phone hot spot, but it still wasn't working. I then checked the other wifi example files and found that they use WiFiSSLClient and port 443, so i gave it a try. And it worked! I got to display my API response on the IDE.

<div align = "center">
<img src = "media/und/undnet9.png" width = 400px>
</div>

**WiFiClient vs WiFiSSLClient**

#### ICANN
**What is DNS**
Domain Name System

- fetch is making a get request
- HTTPS request is also a get request
- nano 33 -> whfiNiNa -> wxample -> ScanNetwork
	- it will scan your available network
	- have your device registered to the 
	- computer.registratio.nyu.edu
	- -> register
	- -> put your mac address
	- -> if there is error, get rid of the colon
- oui lookup
- maclookup.app
