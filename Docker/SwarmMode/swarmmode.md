# some commands for docker swarm services

docker swarm init
## this command will intiate the docker swarm

docker service create alpine ping 8.8.8.8
## this command will create a service named alpine and it will run the ping command to ping the google dns server
docker service ls
## this command will list all the services in the swarm
docker service ps alpine
## this command will list all the tasks of the alpine service
docker service  update --replicas 3 alpine
## this command will update the alpine service to have 3 replicas
docker service ps alpine
## this command will list all the tasks of the alpine service and you will see that there are 3 replicas of the alpine service running
docker service rm alpine
## this command will remove the alpine service from the swarm
