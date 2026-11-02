---
title: "UndNet: Week6"
draft: false
---
my server ip: 142.93.249.203
#### Setting up nginx
[link](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)
#### Others
- Websocket vs HTTP vs MQTT
	- All are network protocol
	- **HTTP**: 
		- Ask and answer
		- The client must explicitly ask for a piece of mail (send a request) for the server to send anything back (return a response)
		- Example: Loading a page, calling an API, anything where you ask when you want to know
	- **WebSocket**: 
		- Open phone line
		- Begins with an HTTP handshake, then upgrades the connection to a persistent, full-duplex TCP tunnel. Both client and server can push messages
		-  Both side is keeping up the connection, if one has failure, need to reconnect
		- Example: live dashboards, chat, multiplayer, anything where the browser needs to react to something happening on the server.
	- **MQTT**: 
		- A bulletin board
		- Devices do not talk to each other directly. Instead, they publish messages to a central MQTT Broker under specific "topics". Any device subscribed to that topic instantly receives the update.
		- Example: microcontrollers, battery-powered sensors, many devices talking at once. It’s the standard for IoT.
<div align= "center">
<img src = "und/protocal.png">
</div>

#### setting up nginx
Tutorial [link](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)
To access the default nginx landing page: `http://your_server_ip`
My page : [http://142.93.249.203/](http://142.93.249.203/)
![[media/und/http5.png]]
- To stop server: `sudo systemctl stop nginx`
- To start server: `sudo systemctl start nginx`
- To restart server: `sudo systemctl restart nginx`
- To reload: `sudo systemctl reload nginx`
- To disable auto configure when boot: `sudo systemctl disable nginx`
- To reenable auto config at boot: `sudo systemctl enable nginx`
- **Setting upServer Blocks**
	- Got my domain name from duckdns: [joy-undnet.duckdns.org](http://joy-undnet.duckdns.org/)
	- ![[http5 1.png|267]] ![[http2.png|354]]
	- ![[server.png|588]]

I am having a hard time figuring it out the repository system on my virtual host, and what are all the files live. So I asked Claude for this. Seems to be somewhat correct? With this visual, things make more sense to me now.
```
/
├── home/
│   └── joychang/                    ← you land here on login
│       ├── packetAnalysis_2.pcap
│       └── packetAnalysis_all.pcap
│
├── var/
│   ├── www/                         ← THE WEBSITES (content)
│   │   ├── html/
│   │   │   └── index.nginx-debian.html    ← default page, IP shows this
│   │   └── joy-undnet.duckdns.org/
│   │       └── html/
│   │           └── index.html             ← your page
│   │
│   └── log/
│       └── nginx/                   ← THE LOGS
│           ├── access.log           ← every request
│           └── error.log
│
└── etc/                             ← ALL CONFIG lives under /etc
    ├── nginx/
    │   ├── nginx.conf               ← master config
    │   ├── sites-available/         ← drafts: every config you've written
    │   │   ├── default
    │   │   └── joy-undnet.duckdns.org
    │   └── sites-enabled/           ← live: aliases to the active ones
    │       ├── default           ──┐
    │       └── joy-undnet...     ──┼─→ point back to sites-available
    │                                ┘
    ├── letsencrypt/
    │   └── live/joy-undnet.duckdns.org/
    │       ├── fullchain.pem        ← your certificate
    │       └── privkey.pem          ← private key, never share
    │
    └── ufw/                         ← firewall rules
```
- Checking my directory:
	![[node2.png|379]]
- To edit the html page
`nano /var/www/joy-undnet.duckdns.org/html/index.html`
- To check `curl https://joy-undnet.duckdns.org`
![[nginx1.png|189]]![[nginx2.png|236]]
#### HTTP analysis
**Checking access logs:**
Checking the logs: `ls -lh /var/log/nginx/`
resource: [NginX documentation](https://docs.nginx.com/waf/logging/access-logs/)


------------------
**Question for Tom**
- All the command, do i remember all of them??
- How do i implement the knowledge of network into creative project?
- Im lowkey struggling with this class LOL (so many acronym!)
- Every senstnec to explain something has other words i dont understand!
	- Node.js is an open-source and cross-platform JavaScript *runtime environment*. 
		- What is run-time environment!!

- Structure of server block and nginx?
- What does enable HTTPS mean exactly?
	- What does certbot do? 
	- What is the TLS certificate, do i just do it one time?
- Node.js & Express.js?

- There are so many web server, why choose nginx?
