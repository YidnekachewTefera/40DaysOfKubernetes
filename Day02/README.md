Dockerize a project


In this scenario we will create a Dockefile that is gonna be used for build a simple to do app, test the image, push the image and pull and run the image on AWS EC2.

First of all let’s clone the application form the git repo


git clone https://github.com/docker/getting-started-app.git

after cloning change working directory to the cloned one which is getting-started-app

1.  Dockerfile: it is a script containing a series of instructions on how to build a Docker image.
create the Dockerfile by using the

<pre>
```
```
FROM node: 18-alpine #The base image is the first thing that is required for starting running our application
WORKDIR /app #it is a directory inside the container
COPY . . # We copied everything that makes our application to run to the workind directory of the container
RUN yarn install --production # we install the packages and the dependencies using the yarn package manager
CMD ["node","src/index.js"] #we are starting the application that is located inside the sr.
EXPOSE 3000 # we exposed the application on port 3000
```
```
</PRE>
2. Building an Image from a Docker file

Building an image from a Dockerfile is the process of creating a Docker image based on the instructions specified in the Dockerfile. This involves Docker reading the Dockerfile, executing the listed commands, and packaging the results into an image.

the following is the syntax for building an image
`docker build -t <image_name>:<tag> <path_to_dockerfile_directory>`
`docker build -t day02-todo .`

3. Pushing an Image in to a Docker Hub: it is the process of uploading a Docker image from your local machine to a remote Docker registry.

A. first you need to have a docker hub account if you don’t have one yet.

B. let’s login to the docker registry from the our terminal

C. let’s create the repo for this specific image on docker hub

copy the commands to push your image.

D. Push the image to the remote repo

now you can notice that we have an image that is ready to be pushed so we can push the image by using the following command

`docker push image-name:tag`

now we have successfully pushed the image

E. Pulling an image: it is the process of downloading a Docker image from a remote Docker registry to your local machine. This is essential for running containers based on images that are stored in registries like Docker Hub, Amazon ECR, Google Container Registry (GCR), or Azure Container Registry (ACR). The docker pull command is used to perform this action.

`docker pull yidnekachew/day02-todo:latest`

4. Creating a running instance of an image on specifi port

We can accomplish this by using the following command

`docker run -dp 80:3000 yidnekachew/day02-todo:latest`

we can access the app from the internet by using the ip address of your server on port 80

`http://your-public-ip-address:80`
