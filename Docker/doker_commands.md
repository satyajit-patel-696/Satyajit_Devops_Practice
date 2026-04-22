**docker container run -d --name my-nginx-container -p 80:80 nginx**
same as 
**docker run -d --name my-nginx-container -p 80:80 nginx**
here -d means detached mode, --name is to give a name to the container, -p is to map the host port to the container port, and nginx is the image we are using to create the container.
**docker container ls**
This command lists all the running containers. If you want to see all containers including the stopped ones, you can use:
**docker container ls -a** this will show you all containers with their status (running, exited,stopped etc.).
**docker container stop my-nginx-container**
This command stops the running container named my-nginx-container. You can also use the container ID
instead of the name to stop the container.
**docker container rm my-nginx-container**
This command removes the stopped container named my-nginx-container. You can also use the container ID
instead of the name to remove the container. Note that you cannot remove a running container, you need to stop it first before removing it. If you want to force remove a running container, you can use the -f flag:
**docker container rm -f my-nginx-container**
This will stop and remove the container in one command. 
**docker container logs my-nginx-container**
This command shows the logs of the container named my-nginx-container. You can see the output of the container's processes and any error messages that may have occurred. This is useful for debugging and monitoring the container's activity. You can also use the -f flag to follow the logs in real-time:
**docker container logs -f my-nginx-container**
This will continuously display the logs as they are generated, allowing you to monitor the container's activity in real-time. You can stop following the logs by pressing Ctrl+C.
**docker container exec -it my-nginx-container bash**
This command allows you to execute a command inside the running container named my-nginx-container. The -it flags are used to run the command in an interactive mode, which means you can interact with the container's shell. In this case, we are opening a bash shell inside the container. You can run any command inside the container by replacing bash with the desired command. For example, if you want to check the contents of the /usr/share/nginx/html directory inside the container, you can use:
**docker container exec -it my-nginx-container ls /usr/share/nginx/html**
This will list the files in the specified directory inside the container. You can also use this command to run other commands or scripts inside the container as needed.    
also one more example is that  suppose you have a postgress container running and you want to access the psql shell inside the container, you can use:
**docker container exec -it my-postgres-container psql -U postgres**
This will open the psql shell inside the my-postgres-container, allowing you to interact with the PostgreSQL database using the postgres user. You can run SQL commands and manage your database directly from the container's shell.       suppose nginx container is running and you want to check the nginx configuration file inside the container, you can use:
**docker container exec -it my-nginx-container cat /etc/nginx/nginx.conf**
This command will display the contents of the nginx.conf file inside the my-nginx-container. You can use this command to check the configuration settings of nginx and troubleshoot any issues related to the configuration.
suppsoe you want to debug a running container and you want to check the environment variables set inside the container, you can use:
**docker container exec -it my-nginx-container env**
This command will display all the environment variables set inside the my-nginx-container. This can be useful for debugging purposes, as you can check if the necessary environment variables are set correctly for the application running inside the container. You can also use this command to check for any sensitive information that may be stored in environment variables, such as database credentials or API keys.

**docker container inspect my-nginx-container**
This command provides detailed information about the container named my-nginx-container in JSON format. It includes information such as the container's configuration, network settings, volumes, and more. This is useful for troubleshooting and understanding the container's setup. You can also use this command to check the container's IP address, which can be helpful for networking purposes. For example, if you want to check the IP address of the my-nginx-container, you can use:
**docker container inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' my-nginx-container**
This command will extract and display the IP address of the my-nginx-container from the inspection output. This can be useful for connecting to the container from other containers or from the host machine.   


ps -aux | grep nginx
This command is used to check if the nginx process is running on the host machine. It lists all the processes and filters the output to show only the lines that contain "nginx". If you see the nginx process in the output, it means that nginx is running on the host machine. However, if you are running nginx inside a Docker container, you will not see the nginx process in the host machine's process list. Instead, you need to check the processes running inside the container using the**docker container exec -it my-nginx-container ps -aux** command. This will show you the processes running inside the my-nginx-container, including the nginx process if it is running. This is important to understand because when you run applications inside Docker containers, they are isolated from the host machine, and you need to use Docker commands to interact with the container and check its processes, logs,and other details.
**docker container stats my-nginx-container**
This command provides real-time statistics about the resource usage of the my-nginx-container. It shows information such as CPU usage, memory usage, network I/O, and block I/O. This is useful for monitoring the performance of the container and identifying any resource bottlenecks. You can also use this command to compare the resource usage of multiple containers by running it without specifying a container name, which will display the stats for all running containers. For example:
 **-it** means interactive terminal, which allows you to interact with the container's shell. This is useful for running commands inside the container and troubleshooting issues. When you use the -it flags with the docker container exec command, it opens an interactive session inside the container, allowing you to run commands and see their output in real-time. This is particularly helpful when you want to debug a running container or check its configuration and environment variables.


 **-d**means detached mode, which allows you to run the container in the background. When you use the -d flag with the docker container run command, it starts the container and immediately returns control to the terminal, allowing you to continue using it while the container runs in the background. This is useful for running applications that do not require interactive input and can run independently without blocking the terminal.


 **-dit** is a combination of the -d, -i, and -t flags. It allows you to run a container in detached mode while still providing an interactive terminal. This means that the container will run in the background, but you can still interact with it if needed. This is useful for running applications that may require occasional interaction or monitoring while still allowing you to use the terminal for other tasks.

 **docker container top my-nginx-container**
This command shows the running processes inside the my-nginx-container. It provides a snapshot of the processes running in the container, similar to the ps command on a Linux system. This is useful for checking the processes that are currently active inside the container and troubleshooting any issues related to process management. You can also use this command to check if the expected processes are running inside the container, such as the nginx process in this case. If you see the nginx process in the output, it means that nginx is running properly inside the container. If you do not see the nginx process, it may indicate that there is an issue with the container or the application running inside it, and further investigation may be needed


**docker container stats**
This command provides real-time statistics about the resource usage of all running containers. It shows information such as CPU usage, memory usage, network I/O, and block I/O for each container. This is useful for monitoring the performance of multiple containers at once and identifying any resource bottlenecks across your containerized applications. You can also use this command to compare the resource usage of different containers and make informed decisions about scaling or optimizing your applications.

**docker container run -it --name my-nginx-container -p 80:80 nginx bash**
This command runs a new container named my-nginx-container using the nginx image and opens an interactive bash shell inside the container. The -it flags allow you to interact with the container's shell, and the -p flag maps port 80 of the host machine to port 80 of the container. This is useful for debugging and troubleshooting, as you can directly access the container's shell and run commands to check the configuration, logs, and other details of the nginx application running inside the container. You can use this command to check the nginx configuration file, view logs, or run any other commands needed to manage the nginx application within the container.


once you exit from the container the container will stop because it was run in interactive mode. If you want to keep the container running even after exiting the shell, you can use the -d flag along with -it:
**docker container run -dit --name my-nginx-container -p 80:80 nginx bash**
This command will run the container in detached mode while still providing an interactive terminal. This means that the container will continue to run in the background even after you exit the shell, allowing you to keep the nginx application running while still being able to interact with the container when needed. You can use this command to run the nginx application in the background while still having the option to access the container's shell for debugging or management purposes.

but if you have given -it and then press exit and then restart the container then you can use the following command to restart the container:
**docker container start -ai my-nginx-container**
here -ai flags are used to start the container in interactive mode and attach to it, allowing you to interact with the container's shell again after restarting it. This is useful for resuming your work inside the container after it has been stopped.


