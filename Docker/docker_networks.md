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

