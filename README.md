# DockerProject1
SingleContainer
Part-1: Create a container image including the website code from the above git repository and create container from that image. You may directly use nginx image as base image or use a base image such as ubuntu/debian

The root/document directory of nginx (where nginx read website/frontend files such as html, css, js, etc.):

/usr/share/nginx/html/    -> if you nginx as base image

/var/www/html/               -> if you install nginx on ubuntu/debian

Part-2: Configure nginx of your container to listen on port 8080 and recreate the image and container

The config file of nginx (that has nginx port configuration):

/etc/nginx/conf.d/default.conf           -> if base image is nginx

/etc/nginx/sites-availables/default     -> if you install nginx on ubuntu/debian



Tip: To view these configuration files, you may ssh (getting shell access) into a running container using `docker exec -it <container-id> bash` command

Step 1:Make a dockerfile
![image](https://github.com/suragsp/DockerProject1/assets/104720115/3134e500-4907-491c-835e-b682cdc7f5a5)
#dockerfile
# Use nginx as the base image
FROM nginx:latest

# Install Git
RUN apt-get update && apt-get install -y git

# Remove the existing html directory
RUN rm -rf /usr/share/nginx/html/*

# Clone the repository
RUN git clone https://github.com/cloudacademy/static-website-example.git /usr/share/nginx/html

# Expose port 80 (default for HTTP)
EXPOSE 80

Step 2 :Run Docker Desktop
Step 3 : Open Terminal in the folder you want to run this code.Note:It should be the same place where you have saved your dockerfile
Check Docker Version by = docker --version
use "docker ps" to see if any docker file is running"
Note if Running - Use Docker stop [container ID] (Container id can be achived by docker ps)
 Then use "docker rm <container_id>" ====This is for removing all resources allocated to the running container===
 
Now let us now run the docker file
Syntax =  "docker build -t <Your file name> ."
eg "docker build -t my_nginx_with_git ."

Then to see all the images.
"docker images"

Then to run your website use.
syntax " docker run -d -p 8080:80 <Your file name>"
eg " docker run -d -p 8080:80 my_nginx_with_website"

Now open Browser and check ===http://localhost:8080/===
This should be the output.
![image](https://github.com/suragsp/DockerProject1/assets/104720115/10729461-8fad-4d69-a479-a6094742ea22)


