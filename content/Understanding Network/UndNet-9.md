---
title: "UndNet: Week 9"
draft: false
---
#### Express.js
[**What is express.js**](https://expressjs.com/)
- Express.js (often called Express) is a fast, minimal, and flexible backend web application framework for Node.js.
- a library/package
- handle HTTP routing

#### microservice
To practice and get more undrestanding on API & HTTP request & server in general, I tried to set up another API. I found this [API](https://agify.io/).
For my kanye api, i am using route api/data, for this one, I will be setting it up with api/agify. Edit my server.js.(server.js)

<span style="color:rgb(192, 0, 0)">I am a bit confused about the bodyParser in the sample code. What is it for and it seems like it is never used after being declared? I am taking it away from my code for now</span>
![[Pasted image 20261110001056.png|470]]

Add function to server.js. And `server.get(proxyLocation+'/agify'+getAgify)`. 
![[Pasted image 20261110001604.png]]
Restart server with `pm2 restart server`. And test it with curl.
![[Pasted image 20261110094223.png]]
Make the directory for index.html for agify, var/www/joy-undnet.duckdns.org/html/agify.
<span style="color:rgb(192, 0, 0)">A bit confused about the most front forward-slash</span>
![[Pasted image 20261110095923.png]]
```
<!DOCTYPE html>
<html>
<head><title>agify</title></head>
<body>
  <h1>How old is that name?</h1>
  <input id="name" placeholder="type a name">
  <button onclick="estimate()">guess</button>
  <p id="result"></p>
  <p><a href="/"home</a></p>

  <script>
	async function estimate() { 
	const name = document.getElementById('name').value; 
	const r = await fetch('/api/agify?name=' + name); 
	const d = await r.json(); 
	document.getElementById('result').textContent = name + ' is about ' + d.age; }
  </script>
</body>
</html>
```

site running: [link](https://joy-undnet.duckdns.org/agify/)