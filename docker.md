###### tags : `tutorial` `docker`

# Docker Cheat Sheet

## A. Image
- Pull image : `docker pull <image>`
- Images list : `docker images`
- Remove image : `docker rmi <image>`

## B. Container
- Container List : 
    - Active container : `docker ps` 
    - All container : `docker ps -a`
- Run container : `docker run <image>`
    - Background : `docker run --name <name> -p <published_port>:<docker_port> -d <image>`
        - `docker run --name mymongo -p 27017:27017 mongo`
        - `docker run --name mymongo -p 192.168.2.7:27017:27017 mongo`
    - Interactive : `docker run --name <name> -p <published_port>:<docker_port> -it <image>`
    - Volume mapping `docker run -v <custom_path>:<docker_path> <image>` 
        - `docker run --name mymongo -v /home/Documents/aditya/data:/data/db  mongo`
        - `docker run -d -v /home/sa/data/mongod.conf:/etc/mongod.conf -v /home/sa/data/db:/data/db mongo --config /etc/mongod.conf`
- Control Container
    - Start : `docker start <container>`
    - Stop : `docker stop <container>`
    - Restart : `docker restart <container>`
- Execute a new process in docker : `docker exec -it <container> <cmd>`
    - `docker exec -it mymongo bash`
- Delete Container : `docker rm <container>`

## C. Dockerfile
- Case 1 Deploy Express App
```
// package.json
{
  "name": "docker_web_app",
  "version": "1.0.0",
  "description": "Node.js on Docker",
  "author": "First Last <first.last@example.com>",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.16.1"
  }
}
```

```
// server.js
'use strict';

const express = require('express');

// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```

```
# Dockerfile
FROM node:14
# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 8080
CMD [ "node", "server.js" ]
- 
```

```
#.dockerignore
node_modules
npm-debug.log
```
