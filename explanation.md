# IP 2 PROJECT 
## Creating a Basic Micro-service
### 1. Choice of the base image on which to build each container.

The client and backend applications runs on Node 16-Alphine images as base for each container.

Mango DB lastest version image used.
Alpine image version of node is small ins ize and helps reduce the size of built images.

### 2.Dockerfile directives used in the creation and running of each container.

### Client Container
FROM node:16-alpine : used Node 16 as base image

WORKDIR /app : Set the working directory to /app inside the container
COPY . . : copy app files to the working directory
RUN npm ci : install dependecies (npm ci )
RUN npm run build : Build the app
ENV NODE_ENV production : set the env to"production"
EXPOSE 3000 : expose the port on which the app will be running (3000 is the default that 'serve')
CMD [ "npx","serve","build" ] : command to Start the app when container run


### Backend Container
FROM node:16-alpine : use Node 16 base image
WORKDIR /app : Set the working directory to /app inside the container
COPY . . : copy app files
RUN npm ci : install dependecies (npm ci )
ENV NODE_ENV production : set the env to"production"
EXPOSE 5000: expose the port on which the app will be running (5000 is the default that 'serve')
CMD [ "npm","start" ] : Start the app



### 3. Docker-compose Networking (Application port allocation and a bridge network implementation) where necessary.

Networking in docker-compose has been implemented using port mapping and a bridge network for secure communication between containers:

Port Mapping -  this is mapping between conatiner and host to  enable application to be accessed outside the docker environment , see below

Client  ports:3000:3000
Backend ports:5000:5000

Bridge Network is defined and attached to all servoces to enable containers communication. see below from our docker compose yaml
networks:
  app-network:
    driver: bridge

### 4. Docker-compose volume definition and usage (where necessary).

    A volume was defined in docker compose as shown below;
    volumes:
      dbdata:
    Usage - they used to persist data across the container shutdown and startup, see below script from docker compose.

    mongodb:
    image: mongo
    restart: always
    ports:
      - 27017:27017
    volumes:
      - dbdata:/data/db
    networks:
      - app-network

###  5.Git workflow used to achieve the task.
Git branch flow as shown below:

Forking : the repository was forked and created a copy from original copy.

Cloning: the forked repository was  cloned to locat laptop.

Commit: all changes made to code was commited to local repository.

Push: the changes commited pushed to remote repository

### 6. Successful running of the applications and if not, debugging measures applied.
Run docker compose-up  : this bring up application successful
Re-build images : incase of changes made in dockerfile. images were re-built and container restarted.

### 7. Good practices such as Docker image tag naming standards for ease of identification of images and containers. 
The built container were named and tagged 

