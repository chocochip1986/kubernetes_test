##Docker build
#===============================================
FROM node:latest

# ENV - defines the environment variables within the docker container
ENV APP_PORT=5000 APP_DIR=/fortune

# WORKDIR - means if the directory specified does not exists, Docker will create it and change directory to it.
WORKDIR ${APP_DIR}

# ADD - copies files from the current working directory where the Dockerfile resides into the docker container's APP_DIR
# ADD also can be used to copy a directory's subdirectories and files. But you have to specify the exact directory name you want to use in the docker container's APP_DIR
ADD main.js .
ADD package.json .
ADD public public
ADD views views

# RUN - install libraries from package.json. npm install is a linux command to install packages. If you have no arguments specified
# in the npm install command, it'll default to the working directories package.json file
RUN npm install


##Docker run
#===============================================
#EXPOSE tells docker that the application listens to port specified by the env var APP_PORT
# this is for documentation only
EXPOSE ${APP_PORT}

# --start_period=5s default is 5seconds.
# the backlash '\' is meant to break the command into 2 lines
# the CMD will execute a curl to the specified URL which will return some info. This implies that your application must
# create and expose this route for docker to use
HEALTHCHECK --interval=60s --timeout=30s --retries=3 \
	CMD curl -f -s http://localhost:${APP_PORT}/health || exit 1

# How should the image be exectued?
ENTRYPOINT ["node", "main.js"]