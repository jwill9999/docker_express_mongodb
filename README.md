# Docker with Express and Mongodb 

```
> git clone https://github.com/jwill9999/docker_express_mongodb.git 
> cd docker_express_mongodb
> npm install
> npm start port 3000
```
## Instructions

> Dockerfile and Docker-compose.yml file included

> Ensure docker is installed for your operating system [link](https://www.docker.com/)

> Within the Dockerfile included ensure the following details match your requirements
```
FROM node:7-alpine 
MAINTAINER $YOUR_NAME, $YOUR_EMAIL
RUN mkdir -p /src/app
WORKDIR /src/app
COPY package.json /src/app/package.json
RUN npm install
COPY . /src/app
EXPOSE 3000
CMD [ "npm", "start"]
```

> In the docker-compose.yml file check the details and file mapping are to your requirments mainly refering to the volume mapping for your host database files to container database files.

```
version: "2"
services:
  web:
    build: .
    ports:
      - "3000:3000"
    links:
      - mongo
  mongo:
    image: mongo
    volumes:
      - /data/mongodb/db:/data/db
    ports:
      - "27017:27017"
```

> In the command line navigate to your codes directory. Then in the command line type  

```
docker-compose build
```

> then once downloaded and complete

```
docker-compose up
```

> The website will load on [http://localhost:3000](http://localhost:3000)


> The express instance and Mongodb container are now connected and the data is also being saved by volume mounting to your host mongo database so persisting data.

> To check this connection out perform the following in the command line

```

** POST DATA **  

curl -X POST -H "Content-type: application/json" http://localhost:3000/data/into/db \
    -d '[ { "name": "jason" }, { "name": "John" }, { "name": "Sarah" } ]'
```

> This should save the data to your container and your local host database for development persistance 


> Navigate to [http://localhost:3000/data/from/db](http://localhost:3000/data/from/db) wher you will see your json data returned 


## Conclusion

This is an example docker container utilizing Express and Mongodb which uses docker-compose and container links behind the scenes. 
The database can be accessed for this example via curl  

> GET /data/from/db

> POST /data/into/db

```

**GET DATA **  

curl http://localhost:3000/data/from/db
```

