---
title: "UndNet: Week 8 Node.js"
draft: false
---
#### Express.js
[**What is express.js**](https://expressjs.com/)
- Express.js (often called Express) is a fast, minimal, and flexible backend web application framework for Node.js.
- a library/package
- handle HTTP routing

#### Node.js
[**What is node.js?**](https://nodejs.org/learn/getting-started/introduction-to-nodejs)
- A run-time environemtn
- allows you to run JavaScript outside of a browser.
- Installing node.js
	![[node.png]]
---------------------
#### Configure Host for Microservices
> Configure your host for microservices. Experiment with a simple service, like sending the time from the server, or a randomly generated text. Document the API for your service and explain how to access it. In the next assignment, one of your classmates will access your site via your REST API.

[**What is REST API??**](https://www.geeksforgeeks.org/node-js/rest-api-introduction/)
REST (Representational State Transfer) API 
- An API that follows REST principles that allows communication between clients and servers using standard HTTP methods.
- An architectural style for designing APIs that allows different applications to communicate over a network.
	- Uses a client-server architecture to separate the user interface from server-side processing.
	- Treats data and functionality as resources that can be accessed through unique URLs.
	- Uses standard HTTP operations such as GET, POST, PUT, PATCH, and DELETE to work with resources.![[rest.png|399]]

For choosing my API, I looked into [this Github API list](https://github.com/public-apis/public-apis#photography) and find some fun one to test it out.
The first one I want to try is [this Kanye West Quote api](https://kanye.rest/), I have used it for other project so i think it should be easy to setup. 

![[request.png|341]]

I made a directory under root call ~/api, and create a server.js that deal with request data from api. Ran the `node server.js`, then check in another terminal tab with curl to see if I got data back.
![[kanye1.png]]
My directory now look like this: 
```
/
├── home/
│   └── joychang/
│       ├── api/                                  THE PROGRAM
│       │   ├── server.js                         ← your API code
│       │   ├── package.json
│       │   ├── package-lock.json
│       │   └── node_modules/                     ← express, body-parser
│       ├── .pm2/                                 ← pm2's files (if you ran it)
│       ├── packetAnalysis_2.pcap
│       └── packetAnalysis_all.pcap
│
├── var/
│   ├── www/                                      THE PAGES
│   │   ├── html/
│   │   │   └── index.nginx-debian.html           ← default, shown at the IP
│   │   └── joy-undnet.duckdns.org/
│   │       └── html/
│   │           ├── index.html                    ← landing page
│   │           └── kanye/
│   │               └── index.html                ← quote page
│   │
│   └── log/nginx/                                THE LOGS
│       ├── access.log
│       └── error.log
│
└── etc/                                          THE CONFIG
    ├── nginx/
    │   ├── nginx.conf
    │   ├── sites-available/
    │   │   ├── default
    │   │   └── joy-undnet.duckdns.org            ← location / + location /api
    │   └── sites-enabled/
    │       ├── default                  → alias
    │       └── joy-undnet.duckdns.org   → alias
    │
    ├── letsencrypt/live/joy-undnet.duckdns.org/
    │   ├── fullchain.pem
    │   └── privkey.pem
    │
    └── ufw/                                      ← 22, 80, 443 open; 8080 closed
```
So to edit my server.js, i do `nano ~/api/server.js` My server.js:
```
const express = require('express');          // include express
const bodyParser = require('body-parser');   // include body-parser
const server = express();                    // make a server using express
const proxyLocation = '/api';                // the proxy location from nginx

server.use(bodyParser.json());               // parse JSON in request bodies

// GET the base path
function handleRequest(request, response) {
  response.send('Hello! Try ' + proxyLocation + '/data');
}

// GET one quote
async function getData(request, response) {
  let result = await fetch('https://api.kanye.rest/');
  let data = await result.json();
  response.json(data);
}

// GET the current date
function getDate(request, response) {
  let now = new Date();
  response.json({ date: now });
}

// POST a count, get that many quotes
async function postData(request, response) {
  let count = request.body.count;
  let quotes = [];
  for (let i = 0; i < count; i++) {
    let result = await fetch('https://api.kanye.rest/');
    let data = await result.json();
    quotes.push(data.quote);
  }
  response.json({ count: count, quotes: quotes });
}

// what to do when the server starts
function serverStart() {
  console.log('Server listening on port ' + this.address().port);
}

// the routes
server.get(proxyLocation, handleRequest);
server.get(proxyLocation + '/data', getData);
server.get(proxyLocation + '/date', getDate);
server.post(proxyLocation + '/data', postData);

// start the server
server.listen(8080, serverStart);
```
In /`etc/nginx/sites-available/joy-undnet.duckdns.org`, add location /api
![[proxylocation.png]]
Check [https://joy-undnet.duckdns.org/api/data](https://joy-undnet.duckdns.org/api/data) and it shows the quote in json format:
![[kanye2.png]]
Then I set up the HTML page `nano /var/www/joy-undnet.duckdns.org/html/kanye/index.html`
```
<!DOCTYPE html>
<html>
<head><title>kanye</title></head>
<body>
  <h1>Words of wisdom (by Ye)</h1>
  <p id="quote">loading…</p>
  <button onclick="getQuote()">another</button>
  <p><a href="/">home</a></p>

  <script>
    function getQuote() {
      fetch('/api/data')
        .then(r => r.json())
        .then(d => {
          document.getElementById('quote').textContent = d.quote;
        });
    }
    getQuote();
  </script>
</body>
</html>


```
My pages:
[main page](https://joy-undnet.duckdns.org/)
[kanye quote page](https://joy-undnet.duckdns.org/kanye/)
![[kanye3.png|421]]
I learned that if you close the ssh, the node session will be terminated as well. To restart node server, navigate to `~/api` and do `node server.js`. For it to keep running after closing use `nohup node server.js > server.log 2>&1 &`
#### pm2 
pm2 keep the server running
` sudo npm install pm2`
`pm2 start server.js`

-----------------------------
#### [Server's Static Files](https://itp.nyu.edu/networks/setting-up-restful-web-services-with-nginx/)
- Access config file: `sudo nano /etc/nginx/sites-available/yourserver`
	- adding default code block
```
server {
        root /var/www/html;
        
        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html;

        server_name yourserver.com;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }
}
```
- Make pointer from the sites-available directory to the sites-enabled directory `$ sudo ln -s /etc/nginx/sites-available/yourserver /etc/nginx/sites-enabled/`
- Restart after configuring `$ sudo service nginx restart`



`curl -v -L http://joy-undnet.duckdns.org/`
`pwd`