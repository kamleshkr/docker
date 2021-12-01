# docker
# Notes and examples
Start Docker Service
---------------------
sudo dockerd

Image and Containers
--------------------
docker image ls

docker container run --publish 80:80 --detach nginx
docker container run --publish 80:80 --detach --name webhost nginx

// What's going on?
docker container top webhost //List running processes in a container
docker container stats webhost
docker container inspect webhost
docker container logs webhost

// Remove
docker container rm <id>

// Shell inside running container
// while starting
docker container run -it --name proxy nginx bash // i -> interactive. t -> tty
docker container start -ai name_of_stopped_container
docker container exec -it name_of_running_container bash

// Some Containers
docker container run --publish 80:80 --detach --name webserver nginx
docker container run --publish 8080:80 --detach --name webhost httpd
docker container run --publish 3306:3306 --detach --name dbserver --env MYSQL_RANDOM_ROOT_PASSWORD=yes mysql

Networking
----------------

docker container port name_of_running_container 

docker network ls
docker network inspect network_name
docker network create my_new_network
docker container run -d --name new_nginx --network my_app_net nginx
nginx:alpine


Volumes
-----------------
docker volume ls

Specify volumes
1. In docker file
VOLUMN /var/lib/mysql

2. Using -v
docker container run -d --new mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=true -v /var/lib/mysql mysql


3. Named volume
docker container run -d --new mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=true -v mysql-db:/var/lib/mysql mysql

Check Volumes
docker container inspect <name>
Look for volumes, Mounts in the json

4. Before creating any container
