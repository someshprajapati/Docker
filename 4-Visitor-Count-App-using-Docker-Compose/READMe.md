# Use the docker-compose command to run the container using docker-compose file

S😎MESH~[visit-counts (master)]-$ **  docker-compose up ** 
```
Creating network "visit-counts_default" with the default driver
Building node-app
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR /app
 ---> Using cache
 ---> ef49b8be9f94
Step 3/6 : COPY ./package.json ./
 ---> Using cache
 ---> 41f80f6fa0de
Step 4/6 : RUN npm install
 ---> Using cache
 ---> d6aa9ddb3e7f
Step 5/6 : COPY ./ ./
 ---> 1a19cd40a80e
Step 6/6 : CMD ["npm", "start"]
 ---> Running in 5db5701a3e30
Removing intermediate container 5db5701a3e30
 ---> 479e59bca49e
Successfully built 479e59bca49e
Successfully tagged visit-counts_node-app:latest
WARNING: Image for service node-app was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating visit-counts_redis-server_1 ... done
Creating visit-counts_node-app_1     ... done
Attaching to visit-counts_node-app_1, visit-counts_redis-server_1
redis-server_1  | 1:C 05 Jul 2020 14:24:38.960 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis-server_1  | 1:C 05 Jul 2020 14:24:38.960 # Redis version=6.0.5, bits=64, commit=00000000, modified=0, pid=1, just started
redis-server_1  | 1:C 05 Jul 2020 14:24:38.960 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
redis-server_1  | 1:M 05 Jul 2020 14:24:38.961 * Running mode=standalone, port=6379.
redis-server_1  | 1:M 05 Jul 2020 14:24:38.961 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
redis-server_1  | 1:M 05 Jul 2020 14:24:38.961 # Server initialized
redis-server_1  | 1:M 05 Jul 2020 14:24:38.961 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
redis-server_1  | 1:M 05 Jul 2020 14:24:38.962 * Ready to accept connections
node-app_1      |
node-app_1      | > @ start /app
node-app_1      | > node index.js
node-app_1      |
node-app_1      | Listening on port 8085
^CGracefully stopping... (press Ctrl+C again to force)
Stopping visit-counts_node-app_1     ... done
Stopping visit-counts_redis-server_1 ... done
```

# Check the running container
S😎MESH~[visit-counts (master)]-$ ** docker ps **
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

# Run the containers in background using the docker-compose command
S😎MESH~[visit-counts (master)]-$ ** docker-compose up -d **
```
Starting visit-counts_redis-server_1 ... done
Starting visit-counts_node-app_1     ... done
```

# Check the running container again
# two containers are running with name: visit-counts_node-app and redis
S😎MESH~[visit-counts (master)]-$ ** docker ps **
```
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                    NAMES
d9f896fa7ef9        visit-counts_node-app   "docker-entrypoint.s…"   20 minutes ago      Up 3 seconds        0.0.0.0:4080->8085/tcp   visit-counts_node-app_1
98622d904b8c        redis                   "docker-entrypoint.s…"   20 minutes ago      Up 3 seconds        6379/tcp                 visit-counts_redis-server_1
```

# Putting the running container down using the docker-compose command
S😎MESH~[visit-counts (master)]-$ ** docker-compose down **
```
Stopping visit-counts_node-app_1     ... done
Stopping visit-counts_redis-server_1 ... done
Removing visit-counts_node-app_1     ... done
Removing visit-counts_redis-server_1 ... done
Removing network visit-counts_default
```

# Check the running container again
S😎MESH~[visit-counts (master)]-$ ** docker ps **
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

# Listing directory
S😎MESH~[visit-counts (master)]-$ ** ls -l **
```
total 96
-rw-rw-r--@ 1 someshprajapati  staff    202 Jul  5 19:43 Dockerfile
-rw-r--r--  1 someshprajapati  staff    136 Jul  5 19:53 docker-compose.yml
-rw-r--r--  1 someshprajapati  staff    160 Jul  5 21:50 docker-compose_auto_restart.yml
-rw-r--r--@ 1 someshprajapati  staff    448 Jul  5 19:52 index.js
-rw-r--r--@ 1 someshprajapati  staff    117 Nov 15  2018 package.json
-rw-r--r--@ 1 someshprajapati  staff  27129 Jul  5 20:00 visit_counts.png
```

# Check the container status running with docker-compose 
# Make sure docker-compose ps command should run inside 
# the directory where the docker-compose.yml exist
# Otherwise get the ERROR
S😎MESH~[visit-counts (master)]-$ ** docker-compose ps **
```
Name   Command   State   Ports
------------------------------
```

# Run the containers in background using the docker-compose command
S😎MESH~[visit-counts (master)]-$ ** docker-compose up -d **
```
Creating network "visit-counts_default" with the default driver
Creating visit-counts_node-app_1     ... done
Creating visit-counts_redis-server_1 ... done
```

# Check the container status running with docker-compose 
# Make sure docker-compose ps command should run inside 
# the directory where the docker-compose.yml exist
# Otherwise get the ERROR
S😎MESH~[visit-counts (master)]-$ ** docker-compose ps **
```
           Name                          Command               State           Ports
---------------------------------------------------------------------------------------------
visit-counts_node-app_1       docker-entrypoint.sh npm start   Up      0.0.0.0:4080->8085/tcp
visit-counts_redis-server_1   docker-entrypoint.sh redis ...   Up      6379/tcp
```

# Try the same command outside the directory
S😎MESH~[visit-counts (master)]-$ ** cd .. **
```
S😎MESH~[4-Visitor-Count-App-using-Docker-Compose (master)]-$ docker-compose ps
ERROR:
        Can't find a suitable configuration file in this directory or any
        parent. Are you in the right directory?

        Supported filenames: docker-compose.yml, docker-compose.yaml
```