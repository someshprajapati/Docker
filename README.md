# Build the Fibonacci Series App using multi containers with the help of below tech stack:
1. Postgres
2. Redis
3. Nginx
4. Node

## Run the multi containers Fibonacci Series App using docker-compose
S😎MESH~[fibonacci_series_app (master)]-$ **docker-compose up --build**
```
Creating network "fibonacci_series_app_default" with the default driver
Building api
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> ef49b8be9f94
Step 3/6 : COPY ./package.json ./
 ---> Using cache
 ---> ac98fff8272e
Step 4/6 : RUN npm install
 ---> Using cache
 ---> 36425e3acfdc
Step 5/6 : COPY ./ ./
 ---> Using cache
 ---> 585f8b899056
Step 6/6 : CMD ["npm", "run", "dev"]
 ---> Using cache
 ---> 0ab6931838aa
Successfully built 0ab6931838aa


Successfully tagged fibonacci_series_app_api:latest
Building client
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> ef49b8be9f94
Step 3/6 : COPY ./package.json ./
 ---> Using cache
 ---> b43ddfaaa595
Step 4/6 : RUN npm install
 ---> Using cache
 ---> 6a7f0a4f7acf
Step 5/6 : COPY ./ ./
 ---> Using cache
 ---> 16883c7288ae
Step 6/6 : CMD ["npm", "run", "start"]
 ---> Using cache
 ---> 723f5eb3fa59
Successfully built 723f5eb3fa59


Successfully tagged fibonacci_series_app_client:latest
Building nginx
Step 1/2 : FROM nginx
 ---> 2622e6cca7eb
Step 2/2 : COPY ./default.conf /etc/nginx/conf.d/default.conf
 ---> 94c24bb2c9bb
Successfully built 94c24bb2c9bb
Successfully tagged fibonacci_series_app_nginx:latest
Building worker
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> ef49b8be9f94
Step 3/6 : COPY ./package.json ./
 ---> Using cache
 ---> e1443602b22a
Step 4/6 : RUN npm install
 ---> Using cache
 ---> ac390f25fa07
Step 5/6 : COPY ./ ./
 ---> Using cache
 ---> 39f3a56669ff
Step 6/6 : CMD ["npm", "run", "dev"]
 ---> Using cache
 ---> 6c89cb5c0500
Successfully built 6c89cb5c0500


Successfully tagged fibonacci_series_app_worker:latest
Creating fibonacci_series_app_redis_1    ... done
Creating fibonacci_series_app_client_1   ... done
Creating fibonacci_series_app_worker_1   ... done
Creating fibonacci_series_app_postgres_1 ... done
Creating fibonacci_series_app_api_1      ... done
Creating fibonacci_series_app_nginx_1    ... done
Attaching to fibonacci_series_app_redis_1, fibonacci_series_app_postgres_1, fibonacci_series_app_worker_1, fibonacci_series_app_api_1, fibonacci_series_app_client_1, fibonacci_series_app_nginx_1
api_1       |
api_1       | > @ dev /app
api_1       | > nodemon
api_1       |
api_1       | [nodemon] 1.18.3
api_1       | [nodemon] to restart at any time, enter `rs`
api_1       | [nodemon] watching: *.*
postgres_1  | The files belonging to this database system will be owned by user "postgres".
postgres_1  | This user must also own the server process.
postgres_1  |
postgres_1  | The database cluster will be initialized with locale "en_US.utf8".
postgres_1  | The default database encoding has accordingly been set to "UTF8".
postgres_1  | The default text search configuration will be set to "english".
postgres_1  |
postgres_1  | Data page checksums are disabled.
postgres_1  |
postgres_1  | fixing permissions on existing directory /var/lib/postgresql/data ... ok
postgres_1  | creating subdirectories ... ok
postgres_1  | selecting dynamic shared memory implementation ... posix
api_1       | [nodemon] starting `node index.js`
client_1    |
client_1    | > client@0.1.0 start /app
client_1    | > react-scripts start
client_1    |
postgres_1  | selecting default max_connections ... 100
postgres_1  | selecting default shared_buffers ... 128MB
redis_1     | 1:C 08 Jul 2020 06:09:17.855 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis_1     | 1:C 08 Jul 2020 06:09:17.855 # Redis version=6.0.5, bits=64, commit=00000000, modified=0, pid=1, just started
redis_1     | 1:C 08 Jul 2020 06:09:17.855 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
postgres_1  | selecting default time zone ... Etc/UTC
redis_1     | 1:M 08 Jul 2020 06:09:17.867 * Running mode=standalone, port=6379.
redis_1     | 1:M 08 Jul 2020 06:09:17.868 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
redis_1     | 1:M 08 Jul 2020 06:09:17.868 # Server initialized
api_1       | Listening
worker_1    |
worker_1    | > @ dev /app
worker_1    | > nodemon
worker_1    |
worker_1    | [nodemon] 1.18.3
redis_1     | 1:M 08 Jul 2020 06:09:17.869 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
worker_1    | [nodemon] to restart at any time, enter `rs`
redis_1     | 1:M 08 Jul 2020 06:09:17.870 * Ready to accept connections
postgres_1  | creating configuration files ... ok
nginx_1     | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
nginx_1     | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
nginx_1     | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
worker_1    | [nodemon] watching: *.*
postgres_1  | running bootstrap script ... ok
postgres_1  | performing post-bootstrap initialization ... ok
postgres_1  | syncing data to disk ... initdb: warning: enabling "trust" authentication for local connections
postgres_1  | You can change this by editing pg_hba.conf or using the option -A, or
postgres_1  | --auth-local and --auth-host, the next time you run initdb.
worker_1    | [nodemon] starting `node index.js`
postgres_1  | ok
postgres_1  |
postgres_1  |
postgres_1  | Success. You can now start the database server using:
postgres_1  |
postgres_1  |     pg_ctl -D /var/lib/postgresql/data -l logfile start
postgres_1  |
postgres_1  | waiting for server to start....2020-07-08 06:09:19.224 UTC [47] LOG:  starting PostgreSQL 12.3 (Debian 12.3-1.pgdg100+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 8.3.0-6) 8.3.0, 64-bit
postgres_1  | 2020-07-08 06:09:19.226 UTC [47] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres_1  | 2020-07-08 06:09:19.245 UTC [48] LOG:  database system was shut down at 2020-07-08 06:09:18 UTC
postgres_1  | 2020-07-08 06:09:19.252 UTC [47] LOG:  database system is ready to accept connections
postgres_1  |  done
postgres_1  | server started
postgres_1  |
postgres_1  | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
postgres_1  |
postgres_1  | 2020-07-08 06:09:19.312 UTC [47] LOG:  received fast shutdown request
postgres_1  | waiting for server to shut down....2020-07-08 06:09:19.317 UTC [47] LOG:  aborting any active transactions
postgres_1  | 2020-07-08 06:09:19.319 UTC [47] LOG:  background worker "logical replication launcher" (PID 54) exited with exit code 1
postgres_1  | 2020-07-08 06:09:19.321 UTC [49] LOG:  shutting down
postgres_1  | 2020-07-08 06:09:19.345 UTC [47] LOG:  database system is shut down
postgres_1  |  done
postgres_1  | server stopped
postgres_1  |
postgres_1  | PostgreSQL init process complete; ready for start up.
postgres_1  |
postgres_1  | 2020-07-08 06:09:19.436 UTC [1] LOG:  starting PostgreSQL 12.3 (Debian 12.3-1.pgdg100+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 8.3.0-6) 8.3.0, 64-bit
postgres_1  | 2020-07-08 06:09:19.436 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
postgres_1  | 2020-07-08 06:09:19.436 UTC [1] LOG:  listening on IPv6 address "::", port 5432
postgres_1  | 2020-07-08 06:09:19.439 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres_1  | 2020-07-08 06:09:19.474 UTC [56] LOG:  database system was shut down at 2020-07-08 06:09:19 UTC
postgres_1  | 2020-07-08 06:09:19.484 UTC [1] LOG:  database system is ready to accept connections
nginx_1     | 10-listen-on-ipv6-by-default.sh: Getting the checksum of /etc/nginx/conf.d/default.conf
nginx_1     | 10-listen-on-ipv6-by-default.sh: /etc/nginx/conf.d/default.conf differs from the packaged version, exiting
nginx_1     | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
nginx_1     | /docker-entrypoint.sh: Configuration complete; ready for start up
client_1    | Starting the development server...
client_1    |
client_1    | Compiled successfully!
client_1    |
client_1    | You can now view client in the browser.
client_1    |
client_1    |   Local:            http://localhost:3000/
client_1    |   On Your Network:  http://172.29.0.6:3000/
client_1    |
client_1    | Note that the development build is not optimized.
client_1    | To create a production build, use npm run build.
client_1    |
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:44 +0000] "GET / HTTP/1.1" 200 836 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:44 +0000] "GET /static/js/bundle.js HTTP/1.1" 200 472761 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:44 +0000] "GET /static/media/logo.5d5d9eef.svg HTTP/1.1" 200 1320 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:44 +0000] "GET /api/values/current HTTP/1.1" 200 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
postgres_1  | 2020-07-08 06:09:45.035 UTC [63] ERROR:  relation "values" does not exist at character 15
postgres_1  | 2020-07-08 06:09:45.035 UTC [63] STATEMENT:  SELECT * from values
api_1       | (node:29) UnhandledPromiseRejectionWarning: error: relation "values" does not exist
api_1       |     at Connection.parseE (/app/node_modules/pg/lib/connection.js:581:48)
api_1       |     at Connection.parseMessage (/app/node_modules/pg/lib/connection.js:380:19)
api_1       |     at Socket.<anonymous> (/app/node_modules/pg/lib/connection.js:116:22)
api_1       |     at Socket.emit (events.js:314:20)
api_1       |     at addChunk (_stream_readable.js:304:12)
api_1       |     at readableAddChunk (_stream_readable.js:280:9)
api_1       |     at Socket.Readable.push (_stream_readable.js:219:10)
api_1       |     at TCP.onStreamRead (internal/stream_base_commons.js:188:23)
api_1       | (Use `node --trace-warnings ...` to show where the warning was created)
api_1       | (node:29) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 1)
api_1       | (node:29) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:45 +0000] "GET /static/js/bundle.js.map HTTP/1.1" 200 473131 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:45 +0000] "GET /sockjs-node/info?t=1594188585155 HTTP/1.1" 200 90 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:45 +0000] "GET /favicon.ico HTTP/1.1" 200 3473 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:45 +0000] "GET /manifest.json HTTP/1.1" 200 317 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:09:56 +0000] "POST /api/values HTTP/1.1" 200 16 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:05 +0000] "POST /api/values HTTP/1.1" 200 16 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
worker_1    | [nodemon] app crashed - waiting for file changes before starting...
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:23 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:23 +0000] "GET /api/values/all HTTP/1.1" 499 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:23 +0000] "GET /sockjs-node/198/d5zkgv4z/websocket HTTP/1.1" 101 167 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /static/js/bundle.js HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /static/js/bundle.js.map HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /static/media/logo.5d5d9eef.svg HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /api/values/current HTTP/1.1" 200 37 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /api/values/all HTTP/1.1" 200 27 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /sockjs-node/info?t=1594188624183 HTTP/1.1" 200 89 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /manifest.json HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:10:24 +0000] "GET /favicon.ico HTTP/1.1" 200 3473 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:15 +0000] "POST /api/values HTTP/1.1" 200 16 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /sockjs-node/895/ybpfxbh0/websocket HTTP/1.1" 101 169 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /static/js/bundle.js HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /static/js/bundle.js.map HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /static/media/logo.5d5d9eef.svg HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /api/values/current HTTP/1.1" 200 56 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /api/values/all HTTP/1.1" 200 40 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /sockjs-node/info?t=1594188679578 HTTP/1.1" 200 89 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /manifest.json HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:19 +0000] "GET /favicon.ico HTTP/1.1" 200 3473 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:32 +0000] "GET / HTTP/1.1" 200 836 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:32 +0000] "GET /static/js/bundle.js HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:32 +0000] "GET /static/media/logo.5d5d9eef.svg HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:32 +0000] "GET /api/values/current HTTP/1.1" 200 56 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:32 +0000] "GET /api/values/all HTTP/1.1" 200 40 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:33 +0000] "GET /sockjs-node/info?t=1594188693037 HTTP/1.1" 200 90 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:36 +0000] "POST /api/values HTTP/1.1" 200 16 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:38 +0000] "GET /sockjs-node/152/kfq4iohu/websocket HTTP/1.1" 101 165 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:38 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:38 +0000] "GET /static/js/bundle.js HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:38 +0000] "GET /static/media/logo.5d5d9eef.svg HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:38 +0000] "GET /api/values/current HTTP/1.1" 200 76 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:38 +0000] "GET /api/values/all HTTP/1.1" 200 54 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:11:38 +0000] "GET /sockjs-node/info?t=1594188698798 HTTP/1.1" 200 89 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:54 +0000] "POST /api/values HTTP/1.1" 200 16 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:56 +0000] "GET /sockjs-node/242/qxbwbvlh/websocket HTTP/1.1" 101 179 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:56 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:56 +0000] "GET /static/js/bundle.js HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:56 +0000] "GET /static/media/logo.5d5d9eef.svg HTTP/1.1" 304 0 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:56 +0000] "GET /api/values/current HTTP/1.1" 200 96 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:56 +0000] "GET /api/values/all HTTP/1.1" 200 68 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:14:56 +0000] "GET /sockjs-node/info?t=1594188896546 HTTP/1.1" 200 90 "http://localhost:4000/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0" "-"
nginx_1     | 172.29.0.1 - - [08/Jul/2020:06:15:06 +0000] "GET /sockjs-node/421/t1rdlkzy/websocket HTTP/1.1" 101 183 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36" "-"
```

## Stopping the containers using docker-compose
S😎MESH~[fibonacci_series_app (master)]-$ **docker-compose down**
```
WARNING: Found orphan containers (fibonacci_series_app_server_1) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
Removing fibonacci_series_app_nginx_1    ... done
Removing fibonacci_series_app_api_1      ... done
Removing fibonacci_series_app_worker_1   ... done
Removing fibonacci_series_app_postgres_1 ... done
Removing fibonacci_series_app_client_1   ... done
Removing fibonacci_series_app_redis_1    ... done
Removing network fibonacci_series_app_default
```

## Run the app again
S😎MESH~[fibonacci_series_app (master)]-$ **docker-compose up --build**
```
Creating network "fibonacci_series_app_default" with the default driver
WARNING: Found orphan containers (fibonacci_series_app_server_1) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
```

## Remove the WARNING: Found orphan containers. Add the option: --remove-orphans
S😎MESH~[fibonacci_series_app (master)]-$ **docker-compose down --remove-orphans**
```
Removing orphan container "fibonacci_series_app_server_1"
Removing fibonacci_series_app_nginx_1    ... done
Removing fibonacci_series_app_api_1      ... done
Removing fibonacci_series_app_worker_1   ... done
Removing fibonacci_series_app_client_1   ... done
Removing fibonacci_series_app_redis_1    ... done
Removing fibonacci_series_app_postgres_1 ... done
Removing network fibonacci_series_app_default
```