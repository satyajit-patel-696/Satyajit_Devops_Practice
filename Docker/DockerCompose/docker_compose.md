# template of docker compose file

version: '3' #if no version is specified, it will take v1 as default version,v2 is recommended for production use and v3 is recommended for development use
services:
  service1:
    image: select the image you want to use for the service
    commands: specify the commands you want to run when the container starts
    ports: specify the ports you want to expose for the service
    volumes: specify the volumes you want to mount for the service
    environment: specify the environment variables you want to set for the service
    networks: specify the networks you want to connect the service to
  service2:
    image: select the image you want to use for the service
    commands: specify the commands you want to run when the container starts
    ports: specify the ports you want to expose for the service     
    volumes: specify the volumes you want to mount for the service
    environment: specify the environment variables you want to set for the service
    networks: specify the networks you want to connect the service to
networks:
volumes:
