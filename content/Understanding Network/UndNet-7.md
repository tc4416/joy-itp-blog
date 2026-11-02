---
title: "UndNet: Week7"
draft: false
---
#### Node.js
**[What is node.js?](https://nodejs.org/learn/getting-started/introduction-to-nodejs) **
- A run-time environemtn
- allows you to run JavaScript outside of a browser.
- Installing node.js
	![[node.png]]

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
My server.js:
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

![[kanye3.png|421]]


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


---------------------------
#### Hunter Q&A's
- Sonet - SDH
- planetarium defense network
- **AI psychosis**
- Overton window
- how to meaningfully disagree
-------------
#### RFC Editor Presentation
origin
- The cycle of writing -> approve -> publish?
