docker run -it --name myubuntu -v my_volume:/container/directory/ubuntu ubuntu:latest bash
#This command will run a new container named myubuntu based on the ubuntu:latest image, and it will mount a Docker volume named my_volume to the /container/directory/ubuntu directory inside the container. The -v flag is used to specify the volume mount, where my_volume is the name of the volume and /container/directory/ubuntu is the path inside the container where the volume will be mounted. The bash command at the end will start an interactive shell inside the container.
docker volume ls  -->to list all the Docker volumes
docker volume inspect my_volume  -->to inspect the details of the my_volume volume, including its mount point and usage information
docker volume rm my_volume  -->to remove the my_volume volume. Be cautious when using this command, as it will permanently delete the volume and any data stored in it
<Bind is a different type of volume mount that allows you to mount a specific directory from the host machine into the container. The syntax for bind mounts is as follows: mane ki tui nije decide karbu ki kene set karbu storage ta>
Bind example:
mkdir mydata
echo "Hello, World!" > mydata/hello.txt
docker run -it --name myubuntu -v $(pwd)/mydata:/container/directory/ubuntu ubuntu:latest bash
#This command will run a new container named myubuntu based on the ubuntu:latest image, and it will mount the mydata directory from the host machine to the /container/directory/ubuntu directory inside the container. The $(pwd) command is used to get the current working directory on the host machine, and it is combined with /mydata to specify the full path to the mydata directory. The bash command at the end will start an interactive shell insidethe container.
then inside the container you will do 
cd /container/directory/ubuntu
cat hello.txt
#This will display the contents of the hello.txt file, which should output "Hello, World


<volume use karbu kanje ki container delete hei gale sbu delete hei jiba data logs all ta store karbar lagi volume use karbu >



<migrating postgress data to new psotstgres container using volume>
docker run -d --name postgres1 -e POSTGRES_PASSWORD=mysecretpassword -v pgdata:/var/lib/postgresql/data postgres:latest
#This command will run a new container named postgres1 based on the postgres:latest image, and it will set the POSTGRES_PASSWORD environment variable to mysecretpassword. It will also mount a Docker volume named pgdata to the /var/lib/postgresql/data directory inside the container, which is where PostgreSQL stores its data. The -d flag is used to run the container in detached mode, meaning it will run in the background. You can then use this container to store your PostgreSQL data, and the data will persist even if the container is stopped or removed, as it is stored in the pgdata volume. 

docker run -d --name postgres2 -e POSTGRES_PASSWORD=mysecretpassword -v pgdata:/var/lib/postgresql/data postgres:latest
#This command will run another container named postgres2 based on the postgres:latest image, and it will also set the POSTGRES_PASSWORD environment variable to mysecretpassword. It will mount the same Docker volume named pgdata to the /var/lib/postgresql/data directory inside the container. This means that both postgres1 and postgres2 containers will share the same data stored in the pgdata volume. You can use either container to access and manage the PostgreSQL data, and any changes made to the data in one container will be reflected in the other container since they are using the same volume. This allows you to easily migrate your PostgreSQL data between containers without losing any data, as the data is stored in the shared pgdata volume. 

docker volume create psql
docker run -d --name psql1 -e POSTGRES_PASSWORD=mypassword -v psql:/var/lib/postgresql/data postgres:15.1
docker logs psql1
docker stop psql1
docker run -d --name psql2 -e POSTGRES_PASSWORD=mypassword -v psql:/var/lib/postgresql/data postgres:15.2
docker logs psql2
docker stop psql2



# 1. Create volume
docker volume create pg-data

# 2. Run first container (psql1)
docker run -d \
  --name psql1 \
  -e POSTGRES_PASSWORD=pass \
  -v pg-data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres

# 3. Enter psql1 and create table + insert data
docker exec -it psql1 psql -U postgres -c "
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);
INSERT INTO users (name) VALUES ('Satya');
"

# 4. Stop and remove first container
docker stop psql1
docker rm psql1

# 5. Run second container with SAME volume
docker run -d \
  --name psql2 \
  -e POSTGRES_PASSWORD=pass \
  -v pg-data:/var/lib/postgresql/data \
  -p 5433:5432 \
  postgres

# 6. Access from second container
docker exec -it psql2 psql -U postgres -c "SELECT * FROM users;"