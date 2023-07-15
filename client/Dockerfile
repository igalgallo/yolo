#====lets CONFIGURE==========

#let use Node 16 base imahe

FROM node:16-alpine

# Set the working directory to /app inside the container

WORKDIR /app
#copy app files
COPY . .
#====BUILD==========
#install dependecies (npm ci )
RUN npm ci

#Build the app
RUN npm run build

#====RUN====
#set the env to"production"
ENV NODE_ENV production

#expose the port on which the app will be running (3000 is the default that 'serve')

EXPOSE 3000

#Start the app
CMD [ "npx","serve","build" ]