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
![[Pasted image 20261027124331.png]]


Look into:
- node.js
- express.js
- nginx

