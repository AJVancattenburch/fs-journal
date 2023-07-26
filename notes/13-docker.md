# DOCKER

## **Using Docker to run a project**

* Docker is the most popular containerization tool in the world.
* It is used to `create, deploy, and run applications` by using containers.
* `Containers` allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package.
* Thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code.
 + **NOTE -**  `Docker Hub` is essentially the GitHub of `Docker images and containers.`
* `Container Orchestration` is the process of automating the deployment, management, scaling, networking, and availability of container-based applications.
* To write a docker file, we need to know the following:
  + The base image to use; *this could be a Linux distribution or another image that has the tools we need already installed*
  + The commands to run; *these are the commands that will be run when the container starts*
  + The port to expose; *this is the port that the container will listen on*
  + The command to run when the container starts; *this is the command that will be run when the container starts*
* `Dockerfile` is a text file that contains all the commands a user could call on the command line to assemble an image.
* To assemble the image on the command line, we use the `docker build` command.
<br>
<br>


* ***STEPS***

* To install docker, run the following commands:
  + `sudo apt-get update`
  + `sudo apt-get install docker-ce docker-ce-cli containerd.io`

* To check if docker is installed, run the following command:
  + `docker --version`

* Curl is a command-line tool for transferring data and supports about 22 protocols including HTTP.

* To install curl and get the APT key for the official Docker repository, run the following commands:
  + `sudo apt-get install curl`
  + `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
  
* To add the Docker repository to APT sources, run the following command:
  + `sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"`

* To check if the Docker repository was added in the case of Ubuntu, run the following command:
  + `apt-cache policy docker-ce`

* To ensure docker is up and running, run the following command:
  + `sudo systemctl status docker`

* With docker running, to show its containers -- run the following command:
  + `docker ps`

* To show all containers, run the following command:
  + `docker ps -a`

* To show all images, run the following command:
  + `docker images`

* To remove a container, run the following command:
  + `docker rm <container_id>`

* To pull and download an image or container, run the following command:
  + `docker pull <image_name>`

* To run the container in the background, restart it if it crashes, and map port 80 on the host to port 3000 in the container, run the following command:
 + `sudo docker run -d --restart unless-stopped -p 80:3000 -p 443:3001 <image_name>`

* To run this command the following steps need to be taken:
  + Create a `Dockerfile` in the root of the project
  + Run `docker build .` in the root of the project
  + Run `docker run -p 8080:8080 <image_id>` to run the image

* How to create a `Dockerfile` in the root of your dotnet project:
  + `COPY . ./` - **NOTE -** copies the current directory into the container
  + `RUN dotnet publish -c Release -o out` - **NOTE -** runs the dotnet publish command
  + `FROM mcr.microsoft.com/dotnet/aspnet:5.0` - **NOTE -** sets the base image
  + `WORKDIR /app` - sets the working directory
  + `COPY --from=build-env /app/out .` - **NOTE -** copies the output of the build-env into the current directory
  + `EXPOSE 80` - **NOTE -** exposes port 80
  + `ENTRYPOINT ["dotnet", "yourAppName.dll"]` - **NOTE -** sets the entrypoint for the container

* In the ec2 instance, if you want to run your docker image, you need to run the following commands:
  + `docker build .` - **NOTE -** builds the docker image
  + `docker run -p 8080:80 <image_id>` - **NOTE -** runs the docker image

* To hit port 3000 in the container, run the following command:
  + `curl localhost:3000`
* If the connection refuses, run the following command:
  + `sudo ufw allow 3000`

<br>
<br>

* To set up your nginx configuration, run the following commands:
  + `sudo apt-get install nginx` - **NOTE -** installs nginx
  + `sudo nano /etc/nginx/sites-available/default` - **NOTE -** opens the default file in the sites-available directory
  + `sudo nginx -t` - **NOTE -** tests the nginx configuration
  + `sudo systemctl restart nginx` - **NOTE -** restarts nginx so that the changes can take effect with a respin
  + `sudo ufw allow 'Nginx HTTP'`  - **NOTE -** allows http traffic from nginx

  <br>
  <br>

* Do not be fooled that you have to pay for an SSL certificate. You can get a free SSL certificate from `Let's Encrypt` by running the following commands:
  + `sudo apt-get install certbot python3-certbot-nginx`
  + `sudo certbot --nginx -d <your_domain> -d www.<your_domain>`
  + `sudo certbot renew --dry-run`

* It comes preinstalled with `snap` on Ubuntu 20.04. To install snap, run the following command:
  + `sudo snap install core; sudo snap refresh core`

* To choose how you would like to run `certbot`, run the following command:
  + `sudo snap install --classic certbot`

* `certbot` creates a public key and a private key. The public key is used to encrypt the data and the private key is used to decrypt the data. To create a public key and a private key, run the following command:
  + `sudo certbot certonly --nginx`

* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 
* 


  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 

* 
  + 

* 
  + 


* Steps
  + Create a new project