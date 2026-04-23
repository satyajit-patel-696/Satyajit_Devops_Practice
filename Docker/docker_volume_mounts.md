docker run -it --name myubuntu -v my_volume:/container/directory/ubuntu ubuntu:latest bash
#This command will run a new container named myubuntu based on the ubuntu:latest image, and it will mount a Docker volume named my_volume to the /container/directory/ubuntu directory inside the container. The -v flag is used to specify the volume mount, where my_volume is the name of the volume and /container/directory/ubuntu is the path inside the container where the volume will be mounted. The bash command at the end will start an interactive shell inside the container.
docker volume ls  -->to list all the Docker volumes
docker volume inspect my_volume  -->to inspect the details of the my_volume volume, including its mount point and usage information
docker volume rm my_volume  -->to remove the my_volume volume. Be cautious when using this command, as it will permanently delete the volume and any data stored in it
<Bind is a different type of volume mount that allows you to mount a specific directory from the host machine into the container. The syntax for bind mounts is as follows: mane ki tui nije decide karbu ki kene set karbu storage ta>

mkdir mydata
echo "Hello, World!" > mydata/hello.txt
docker run -it --name myubuntu -v $(pwd)/mydata:/container/directory/ubuntu ubuntu:latest bash
#This command will run a new container named myubuntu based on the ubuntu:latest image, and it will mount the mydata directory from the host machine to the /container/directory/ubuntu directory inside the container. The $(pwd) command is used to get the current working directory on the host machine, and it is combined with /mydata to specify the full path to the mydata directory. The bash command at the end will start an interactive shell insidethe container.
then inside the container you will do 
cd /container/directory/ubuntu
cat hello.txt
#This will display the contents of the hello.txt file, which should output "Hello, World