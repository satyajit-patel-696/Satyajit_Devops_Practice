docker container run -p 80:80 --name webhost nginx:alpine

docker container port webhost  -->output will be tcp://0.0.0.0:80                
#to check the port mapping of the container

docker container inspect webhost --format  '{{range .NetworkSettings.Networks}}{{IPAddress}}{{end}}'
-->output will be in json format and you can find the port mapping in the NetworkSettings section

docker network ls  -->to list all the networks
docker network inspect bridge  -->to inspect the default bridge network
#bridge is a virtual network that Docker creates on the host machine. It allows containers to communicate with each other and with the host machine.
docker network inspect host  -->to inspect the host network
#host network is a network that allows containers to share the host's network stack. This means that the container will have access to all the network interfaces and ports of the host machine.
docker network create mynetwork  -->to create a custom  virtual network

docker container run -d --name webhost1 --network mynetwork nginx:alpine

commnad to connect two container to the same network through connect command is as follows:

docker container run -d --name webhost2 nginx:alpine
docker network connect mynetwork webhost2   

to check it 
docker container run -it webhost1 ping webhost2
#to check the connectivity between the two containers

docker container run --rm  -it nginx:alpine bash
--rm  comand is used to remove the container after it exits


docker image inspect nginx this will give you the details of the nginx image 
 you can rename a image by using tag
 docker tag nginx:alpine mynginx:latest
#this will create a new image named mynginx with the latest tag based on the nginx:alpine image. You can then use mynginx:latest to run containers instead of nginx:alpine.




docker image build -t mynginx:latest . #here . means build in this repo
#this command will build a new image named mynginx with the latest tag based on the Dockerfile in the current directory. You can then use mynginx:latest to run containers based on this image.



docker system df  -->to check the disk usage of Docker images, containers, and volumes
docker system prune  -->to remove all unused Docker objects (images, containers, volumes, and networks) to free up disk space. Be cautious when using this command, as it will remove all unused objects, including those that may still be needed. You can use the --volumes flag to also remove unused volumes.
docker image prune  -->to remove all unused Docker images to free up disk space. Be cautious when using this command, as it will remove all unused images, including those that may still be needed. You can use the --filter flag to specify criteria for which images to remove, such as dangling images or images that are not tagged.
