# docker-google-cadvisor
Deep dive into the resource usage of containers using Google's cAdvisor tool

# Install docker - see whale in your status bar?
$ docker --version
$ docker-compose --version
$ docker-machine --version

# Run a Dockerized web server to make sure everything works:
$ docker run -d -p 80:80 --name webserver nginx

# Pull and run hello-world container from docker hub
$ docker pull hello-world
$ docker run hello-world

# You can specify a name for the container. “hello-world” above is the image name.
$ docker pull --name=hello-world hello-world

# List all Docker containers:
$ docker ps -a

# Pull and run cAdvisor:
$ docker pull google/cadvisor
$ docker run --volume=/var/run:/var/run:rw --volume=/sys:/sys:ro \--volume=/var/lib/docker:/var/lib/docker:ro --publish=8080:8080 \--detach=true --name=cadvisor google/cadvisor:latest

# Open Firefox web browser and browse the following location:
http://localhost:8080

# Lets create a container named “ubuntu1” that intentionally causes a spike on core 0:
$ docker run -d --cpuset-cpus=0 --name=ubuntu1 ubuntu /bin/dd if=/dev/zero of=/dev/null
## See the spike?
$ docker stop ubuntu1
## Back to normal now?

# Let’s create and run a container named “ubuntu2” that will sleep for 60 seconds, then exit:
$ docker run -d --name=ubuntu2 ubuntu /bin/sleep 60

# You cannot remove a running container, so stop the container before attempting removal:
$ docker stop ubuntu2 cadvisor

# Remove the stopped containers:
$ docker rm ubuntu2 cadvisor
