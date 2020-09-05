# docker-google-cadvisor
A deep dive into the resource usage of containers using Google's cAdvisor tool

## Install docker
$ brew cask install docker
### Next, launch the Docker Desktop. Give privileged access.

## Check versions of Docker Engine, Compose, and Machine.
$ docker --version\
$ docker-compose --version\
~~$ docker-machine --version~~

## Run a Dockerized web server to make sure everything works:
$ docker run -d -p 80:80 --name webserver nginx
### Do you see nginx webserver running on port 80? Try typing `localhost` on your browser.

## Pull and run hello-world container from docker hub
$ docker pull hello-world\
$ docker run hello-world
### The hello-world container exits after printing a `Hello from Docker!` message.

## List all Docker containers:
$ docker ps -a

## Pull and run cAdvisor:
$ docker pull google/cadvisor\
$ docker run --volume=/var/run:/var/run:rw --volume=/sys:/sys:ro \--volume=/var/lib/docker:/var/lib/docker:ro --publish=8080:8080 \--detach=true --name=cadvisor google/cadvisor:latest
### You should see cAdvisor running on port 8080.

## Open your web browser and browse the following location:
http://localhost:8080

## Lets create a container named “ubuntu1” that intentionally causes a spike on core 0:
$ docker run -d --cpuset-cpus=0 --name=ubuntu1 ubuntu /bin/dd if=/dev/zero of=/dev/null
### See the spike?
$ docker stop ubuntu1
### You should observe that ubuntu1 has exited. And, isn't CPU core usage back to normal now?

## Let’s create and run a container named “ubuntu2” that will sleep for 60 seconds, then exit:
$ docker run -d --name=ubuntu2 ubuntu /bin/sleep 60

## List all Docker containers and observe their states:
$ docker ps -a

## You cannot remove a running container, so stop the container before attempting removal:
$ docker stop cadvisor

## Remove the stopped containers:
$ docker rm ubuntu2 cadvisor
