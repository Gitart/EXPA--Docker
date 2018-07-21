# lets us specify which base image from Docker Hub we want to build from. 
# In our case, we are using the latest version of the official node image.
FROM mhart/alpine-node:base-10

# lets us execute a command, which in our case is to create a new directory.
# The -p flag will create nested directories, but only if they don't exist already.
RUN mkdir -p /usr/src/app

#  sets this newly created directory as the working directory
#  for any COPY, RUN and CMD instructions that follow in the Dockerfile.
WORKDIR /usr/src/app

# is pretty straightforward and lets us copy files or a whole directory from a source to a destination.
# We are going to COPY the package.json file over to our working directory.
# COPY package.json /usr/src/app/

# lets us execute the npm install command which will download all the dependencies defined in package.json.
# RUN npm install

#  lets us copy our entire local directory into our working directory to bundle our application source code.
COPY . /usr/src/app

# exposes a port which the container will listen on.
EXPOSE 8000

# sets the default command to execute our container.
CMD [ "node", "app" ]
