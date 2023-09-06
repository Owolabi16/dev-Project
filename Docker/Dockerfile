# Dockerfile 

# pull the base image
FROM node:14.5-alpine

# set working directory
WORKDIR /app

# copy the application into the container
COPY package*.json ./

# install the dependencies
RUN npm install

# copy the rest of the application into the container
COPY . ./

# Expose the port application runs on.
EXPOSE 3000

# start the application when container is up
CMD [ "npm" , "start" ]