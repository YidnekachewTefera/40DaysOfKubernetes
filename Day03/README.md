40DaysOfKubernetes 03

Multi-Stage 

Multi-stage Docker builds are a way to create Docker images efficiently by using multiple FROM statements in a single Dockerfile. Each FROM instruction starts a new build stage. This approach allows you to keep your images small and manageable by separating the build environment from the runtime environment.

clone the following git repo.

`git clone https://github.com/piyushsachdeva/todoapp-docker.git`

1. multi-stage Dockerfile Script
For this scenario we will be using a docker multi stage script for simple to do app, the script is as following:

<pre>

```
```
FROM node:18-alpine AS installer

WORKDIR /app

COPY package-lock.json ./

COPY package.json ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx:latest AS deployer

COPY --from=installer /app/build /usr/share/nginx/html

```
```
</pre>

Installer Stage
A. Base Image

` FROM node:18-alpine AS installer `

This line specifies the base image for the first stage of the build. node:18-alpine is a lightweight version of the Node.js 18 runtime, which is based on the Alpine Linux distribution. The AS installer part gives a name to this stage, which can be referenced later.

B. Working Directory

`WORKDIR /APP`

This sets the working directory inside the container to /app. All subsequent commands will be run in this directory.

C. Copying the packages

<pre>
```
COPY package-lock.json ./
COPY pakacge.json ./

```
</pre>

This copies the package.json and package-lock.json from your local machine to the /app directory in the container. These files contain the metadata and dependencies for your Node.js project.

D. Installing the Dependencies

` RUN npm install `
This runs npm install to install all the dependencies specified in the package.json file. This ensures that the necessary packages are available to build the project.

E. Copying the App code

` COPY . .`
This copies the rest of the application code from your local machine to the /app directory in the container.

F. Compile the script

`RUN npm run build`

This runs the build script defined in your package.json. Typically, this script compiles the source code into a production-ready format (e.g., transpiling JavaScript, bundling files, etc.), and the output is usually placed in a build directory.


Deployer Stage
A. Base Image

`FROM nginx:latest AS deployer`
This line specifies the base image for the second stage of the build. nginx:latest is the latest version of the Nginx web server. The AS deployer part gives a name to this stage, which can be referenced later.

B. Copying the build directory
`COPY --from=installer /app/build /usr/share/nginx/html`
This line copies the contents of the build directory from the installer stage to the Nginx default document root (/usr/share/nginx/html). The --from=installer part indicates that the source files are coming from the installer stage.
2. Building the Image from the Dockerfile

us the following command to build the image
`docker build -t the_name_of_the_image the_directory_to_which_the_Dockerfile_is_locate`
`docker build -t day03-todo-app .`
3. Running the docker image

run the following command to run the container on a specific port
`docker run -dp the_server_port_number:the_container_port_number image-name`
`docker run -dp 80:80 day03-todo-app`
The reason I used 80:80 as a port number is because I want the container to be accessible on port 80 and the Nginx is running on port 80 by default.
4. Running Commands inside a docker image

use the following command in order to be able to run commands inside the container
`docker exec -it container_name sh_or_bash`
`docker exec -it day03-todo-app sh`
5. Viewing the content inside a docker container

Use the following command to view the contents inside your container
`docker inspect container-name`

Thank you very much !!!
