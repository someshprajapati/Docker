# Dockerfile to take alpine image and run the redis server

## Basic Dockerfile to create the redis server image
S😎MESH~[redis-image (master)]-$ **cat Dockerfile**
```
───────┬────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: Dockerfile
───────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ # Use an existing docker image as base
   2   │ FROM alpine
   3   │
   4   │ # Download and install depedency
   5   │ RUN apk add --update redis
   6   │
   7   │ # Tell the image what to do when start as container
   8   │ CMD ["redis-server"]
───────┴────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

## Build the redis server image using Dockerfile
S😎MESH~[redis-image (master)]-$ **docker build .**
```
Sending build context to Docker daemon   2.56kB
Step 1/3 : FROM alpine
 ---> a24bb4013296
Step 2/3 : RUN apk add --update redis
 ---> Using cache
 ---> 516962f8dd66
Step 3/3 : CMD ["redis-server"]
 ---> Using cache
 ---> 843ce5b95574
Successfully built 843ce5b95574
```

## Run the redis-server container
S😎MESH~[redis-image (master)]-$ **docker run 843ce5b95574**
```
1:C 05 Jul 2020 13:05:53.145 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C 05 Jul 2020 13:05:53.147 # Redis version=5.0.9, bits=64, commit=869dcbdc, modified=0, pid=1, just started
1:C 05 Jul 2020 13:05:53.147 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M 05 Jul 2020 13:05:53.154 * Running mode=standalone, port=6379.
1:M 05 Jul 2020 13:05:53.154 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
1:M 05 Jul 2020 13:05:53.154 # Server initialized
1:M 05 Jul 2020 13:05:53.154 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
1:M 05 Jul 2020 13:05:53.155 * Ready to accept connections
^C1:signal-handler (1593954369) Received SIGINT scheduling shutdown...
1:M 05 Jul 2020 13:06:09.254 # User requested shutdown...
1:M 05 Jul 2020 13:06:09.255 * Saving the final RDB snapshot before exiting.
1:M 05 Jul 2020 13:06:09.257 * DB saved on disk
1:M 05 Jul 2020 13:06:09.257 # Redis is now ready to exit, bye bye...
```

## Tag the image created using Dockerfile
S😎MESH~[redis-image (master)]-$ **docker build -t somesh/redis-image:latest .**
```
Sending build context to Docker daemon   2.56kB
Step 1/3 : FROM alpine
 ---> a24bb4013296
Step 2/3 : RUN apk add --update redis
 ---> Using cache
 ---> 516962f8dd66
Step 3/3 : CMD ["redis-server"]
 ---> Using cache
 ---> 843ce5b95574
Successfully built 843ce5b95574
Successfully tagged somesh/redis-image:latest
```

## Check the containers
😎MESH~[redis-image (master)]-$ **docker ps -all**
```
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                      PORTS               NAMES
1c7583d98acd        843ce5b95574        "redis-server"      About a minute ago   Exited (0) 45 seconds ago                       optimistic_hugle
```

## Run the image using the created tag
S😎MESH~[redis-image (master)]-$ **docker run somesh/redis-image:latest**
```
1:C 05 Jul 2020 13:07:32.462 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C 05 Jul 2020 13:07:32.462 # Redis version=5.0.9, bits=64, commit=869dcbdc, modified=0, pid=1, just started
1:C 05 Jul 2020 13:07:32.462 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M 05 Jul 2020 13:07:32.464 * Running mode=standalone, port=6379.
1:M 05 Jul 2020 13:07:32.464 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
1:M 05 Jul 2020 13:07:32.464 # Server initialized
1:M 05 Jul 2020 13:07:32.465 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
1:M 05 Jul 2020 13:07:32.465 * Ready to accept connections
^C1:signal-handler (1593954455) Received SIGINT scheduling shutdown...
1:M 05 Jul 2020 13:07:35.129 # User requested shutdown...
1:M 05 Jul 2020 13:07:35.129 * Saving the final RDB snapshot before exiting.
1:M 05 Jul 2020 13:07:35.133 * DB saved on disk
1:M 05 Jul 2020 13:07:35.133 # Redis is now ready to exit, bye bye...
```