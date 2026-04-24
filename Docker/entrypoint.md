# entry point same as cmd but it will run when the container starts and it will run only one time when the container starts and it will not run when the container is restarted or when the container is stopped and started again
#  main difffernce between entry point and cmd is that entry point will run when the container starts and it will run only one time when the container starts and it will not run when the container is restarted or when the container is stopped and started again but cmd will run every time when the container is started or restarted or when the container is stopped and started again

# 1. Create a Dockerfile with an entry point
FROM busybox:latest
CMD ["hostname"]

docker build -t hostname .
docker run hostname
#This will run the hostname command when the container starts, and it will output the hostname of the container. If you stop and start the container again, it will run the hostname command again and output the hostname of the container again. This is because the CMD instruction will run every time the container is started or restarted.
# docker  run  hostname date
this will give output the date of the container when it starts, and it will not run the hostname command because the CMD instruction will be overridden by the command specified in the docker run command. This is because the CMD instruction will run every time the container is started or restarted, but it can be overridden by the command specified in the docker run command.

# example of docker entry point
FROM busybox:latest
ENTRYPOINT ["hostname"]
docker build -t hostname .
docker run hostname
#This will run the hostname command when the container starts, and it will output the hostname of the container. If you stop and start the container again, it will not run the hostname command again because the ENTRYPOINT instruction will run only one time when the container starts and it will not run when the container is restarted or when the container is stopped and started again. This is because the ENTRYPOINT instruction will run only one time when the container starts and it will not run when the container is restarted
# docker run hostname date
#this will give you error as no cmd set only entry point is set and it will not run the date command because the ENTRYPOINT instruction will run only one time when the container starts and it will not run when the container is restarted or when the container is stopped and started again.

docker run --entrypoint date hostname
#This will run the date command when the container starts, and it will output the date of the container. This is because the --entrypoint flag will override the ENTRYPOINT instruction specified in the Dockerfile, and it will run the date command instead of the hostname command when the container starts.


##########  # example of docker entry point with cmd
FROM busybox:latest
ENTRYPOINT ["sh", "-c"]
CMD ["hostname && date"]
 #### entry point with cmd  image trat as entrypoint cmd
docker build -t hostname .
docker run hostname
#This will run the hostname and date commands when the container starts, and it will output the hostname and date of the container. If you stop and start the container again, it will not run the hostname and date commands again because the ENTRYPOINT instruction will run only one time when the container starts and it will not run when the container is restarted or when the container is stopped and started again.
