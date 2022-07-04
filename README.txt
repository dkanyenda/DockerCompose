TABLE OF CONTENTS
1. Docker commands
2. Docker files used
2. Docker errors

1. Docker commands
=====================
#the pool is in Container 75e04f2ab52c
#the pool is in /usr/app/pool/bin

#starting docker container
sudo docker container start 75e04f2ab52c

#login to docker container
sudo docker container exec -it 75e04f2ab52c bash

#check docker containers running
sudo docker ps 

#Check all docker container on the server
sudo docker ps -a

admin01@testadmin06:~/DockerCompose$ sudo docker ps -a
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS              PORTS      NAMES
9b6b315cd465   nginx               "/docker-entrypoint.…"   2 minutes ago   Up About a minute   80/tcp     dockercompose_nginx_1_58062786f7d4
cb3b22033bfc   redis:2.8           "docker-entrypoint.s…"   2 minutes ago   Up About a minute   6379/tcp   dockercompose_redis_1_d7edfbbe07ed
75e04f2ab52c   dockercompose_web   "/usr/app/build/bin/…"   2 minutes ago   Created                        dockercompose_web_1_3d6000dc2e70
admin01@testadmin06:~/DockerCompose$

2. Docker files used
======================
The files used for the configuration are in the location below


admin01@testadmin06:~$
admin01@testadmin06:~$ pwd
/home/admin01
admin01@testadmin06:~$ tree DockerCompose
DockerCompose
├── docker-compose.yml
├── nodejs
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   └── server.js
├── node_modules
├── README.txt
└── src
    └── app

4 directories, 6 files
admin01@testadmin06:~$


 

3. Docker errors
==================
On bulding/ running the docker-compose.yml, the container with the pool had read timeout errors

admin01@testadmin06:~/DockerCompose$ sudo docker-compose up --build
Building web
Step 1/13 : FROM ubuntu
 ---> 27941809078c
Step 2/13 : WORKDIR /usr/app/src/app
 ---> Using cache
 ---> 948070d2c5ae
Step 3/13 : COPY package*.json ./
 ---> Using cache
 ---> a2b1043e9cfc
Step 4/13 : RUN apt-get update && apt-get install -y curl
 ---> Using cache
 ---> b7b48ed211c1
Step 5/13 : RUN apt install -y   curl
 ---> Using cache
 ---> a0fd18d50085
Step 6/13 : RUN apt install -y   nodejs
 ---> Using cache
 ---> 7a08396d0fd8
Step 7/13 : RUN apt-get install -y   npm
 ---> Using cache
 ---> 3a41982d9a2f
Step 8/13 : RUN echo "Node: " && node -v
 ---> Using cache
 ---> edb12588a5a3
Step 9/13 : RUN echo "NPM: " && npm -v
 ---> Using cache
 ---> 83f601c0d879
Step 10/13 : RUN npm install
 ---> Using cache
 ---> 882e87948b4e
Step 11/13 : COPY . .
 ---> Using cache
 ---> 1f8dcb8f4aa5
Step 12/13 : EXPOSE 8080
 ---> Using cache
 ---> ba10bf0b1f77
Step 13/13 : CMD [ "node", "server.js" ]
 ---> Using cache
 ---> 5e5cb41af050
Successfully built 5e5cb41af050
Successfully tagged dockercompose_web:latest
Creating dockercompose_web_1_c938f47462fa ...
Creating dockercompose_redis_1_b3b3d663bf4d ... done
Creating dockercompose_nginx_1_fd3d0b7f11d9 ... done

ERROR: for dockercompose_web_1_c938f47462fa  UnixHTTPConnectionPool(host='localhost', port=None): Read timed out. (read timeout=60)

ERROR: for web  UnixHTTPConnectionPool(host='localhost', port=None): Read timed out. (read timeout=60)
ERROR: An HTTP request took too long to complete. Retry with --verbose to obtain debug information.
If you encounter this issue regularly because of slow network conditions, consider setting COMPOSE_HTTP_TIMEOUT to a higher value (current value: 60).
admin01@testadmin06:~/DockerCompose$
admin01@testadmin06:~/DockerCompose$
admin01@testadmin06:~/DockerCompose$
admin01@testadmin06:~/DockerCompose$
admin01@testadmin06:~/DockerCompose$
admin01@testadmin06:~/DockerCompose$