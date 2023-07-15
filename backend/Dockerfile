#====lets CONFIGURE==========

#let use Node 16 base imagee

FROM node:16-alpine

# Set the working directory to /app inside the container

WORKDIR /app
#copy app files
COPY . .
#====BUILD==========
#install dependecies (npm ci )
RUN npm ci
#set the env to"production"
ENV NODE_ENV production

#expose the port on which the app will be running (5000 is the default that 'serve')

EXPOSE 5000

#Start the app
CMD [ "npm","start" ]