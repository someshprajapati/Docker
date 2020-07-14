# Build the React App and Integrate with Travis-CI and push the images on Docker Hub.

## Build the React App using multi containers with the help of below tech stack. 
1. Postgres
2. Redis
3. Nginx
4. Node

## Run the multi containers App using docker-compose
S😎MESH~[multi-container-application-production (master)]-$ **docker-compose up --build**
```
Building api
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> 860a16c733d9
Step 3/6 : COPY ./package.json ./
 ---> 5005635c5782
Step 4/6 : RUN npm install
 ---> Running in 8b7a64dea098
npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade to fsevents 2.
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated

> nodemon@1.18.3 postinstall /app/node_modules/nodemon
> node bin/postinstall || exit 0

Love nodemon? You can now support the project via the open collective:
 > https://opencollective.com/nodemon/donate

npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.2.7 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN app No description
npm WARN app No repository field.
npm WARN app No license field.

added 305 packages from 191 contributors and audited 306 packages in 11.965s
found 0 vulnerabilities

Removing intermediate container 8b7a64dea098
 ---> 8ec5b6ec75bd
Step 5/6 : COPY ./ ./
 ---> 634d4cab29f6
Step 6/6 : CMD ["npm", "run", "start"]
 ---> Running in c86f1c5ab5ee
Removing intermediate container c86f1c5ab5ee
 ---> dff70a14c24f
Successfully built dff70a14c24f
Successfully tagged multi-container-application-production_api:latest
Building client
Step 1/10 : FROM node:alpine as builder
 ---> 5d97b3d11dc1
Step 2/10 : WORKDIR '/app'
 ---> Using cache
 ---> 860a16c733d9
Step 3/10 : COPY ./package.json ./
 ---> 0ed122621ed3
Step 4/10 : RUN npm install
 ---> Running in 9c18aa02debb
npm WARN deprecated extract-text-webpack-plugin@3.0.2: Deprecated. Please use https://github.com/webpack-contrib/mini-css-extract-plugin
npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade to fsevents 2.
npm WARN deprecated browserslist@2.11.3: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.
npm WARN deprecated sw-precache@5.2.1: Please migrate to Workbox: https://developers.google.com/web/tools/workbox/guides/migrations/migrate-from-sw
npm WARN deprecated chokidar@1.7.0: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
npm WARN deprecated sw-toolbox@3.6.0: Please migrate to Workbox: https://developers.google.com/web/tools/workbox/guides/migrations/migrate-from-sw
npm WARN deprecated browserslist@1.7.7: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated circular-json@0.3.3: CircularJSON is in maintenance only, flatted is its successor.
npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated

> core-js@2.6.11 postinstall /app/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon:
> https://opencollective.com/core-js
> https://www.patreon.com/zloirock

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)


> uglifyjs-webpack-plugin@0.4.6 postinstall /app/node_modules/uglifyjs-webpack-plugin
> node lib/post_install.js

npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.1.3 (node_modules/react-scripts/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN notsup Unsupported engine for watchpack-chokidar2@2.0.0: wanted: {"node":"<8.10.0"} (current: {"node":"14.5.0","npm":"6.14.5"})
npm WARN notsup Not compatible with your version of node/npm: watchpack-chokidar2@2.0.0
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.1.2 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN ajv-keywords@3.5.1 requires a peer of ajv@^6.9.1 but none is installed. You must install peer dependencies yourself.

added 1367 packages from 749 contributors and audited 1369 packages in 45.944s

24 packages are looking for funding
  run `npm fund` for details

found 44 vulnerabilities (32 low, 6 moderate, 6 high)
  run `npm audit fix` to fix them, or `npm audit` for details
Removing intermediate container 9c18aa02debb
 ---> 68b4ed4c461b
Step 5/10 : COPY ./ ./
 ---> 63e7af6496c3
Step 6/10 : RUN npm run build
 ---> Running in 5c4b2fe44897

> client@0.1.0 build /app
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  61.84 KB  build/static/js/main.ff1180e4.js
  299 B     build/static/css/main.c17080f1.css

The project was built assuming it is hosted at the server root.
You can control this with the homepage field in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage" : "http://myname.github.io/myapp",

The build folder is ready to be deployed.
You may serve it with a static server:

  npm install -g serve
  serve -s build

Find out more about deployment here:

  http://bit.ly/2vY88Kr

Removing intermediate container 5c4b2fe44897
 ---> 022cf026be88
Step 7/10 : FROM nginx
 ---> 2622e6cca7eb
Step 8/10 : EXPOSE 3000
 ---> Running in d30399d58ac4
Removing intermediate container d30399d58ac4
 ---> e16534a731b8
Step 9/10 : COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
 ---> f40fe8ee3f4c
Step 10/10 : COPY --from=builder /app/build /usr/share/nginx/html
 ---> 2ce27bb3e426
Successfully built 2ce27bb3e426
Successfully tagged multi-container-application-production_client:latest
Building nginx
Step 1/2 : FROM nginx
 ---> 2622e6cca7eb
Step 2/2 : COPY ./default.conf /etc/nginx/conf.d/default.conf
 ---> 94691ecf08ff
Successfully built 94691ecf08ff
Successfully tagged multi-container-application-production_nginx:latest
Building worker
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> 860a16c733d9
Step 3/6 : COPY ./package.json ./
 ---> b76a12ef230a
Step 4/6 : RUN npm install
 ---> Running in 1b136c73a408
npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade to fsevents 2.
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated

> nodemon@1.18.3 postinstall /app/node_modules/nodemon
> node bin/postinstall || exit 0

Love nodemon? You can now support the project via the open collective:
 > https://opencollective.com/nodemon/donate

npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.2.7 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN app No description
npm WARN app No repository field.
npm WARN app No license field.

added 228 packages from 139 contributors and audited 229 packages in 6.917s
found 0 vulnerabilities

Removing intermediate container 1b136c73a408
 ---> d152c4a449c0
Step 5/6 : COPY ./ ./
 ---> b07c5d7094a4
Step 6/6 : CMD ["npm", "run", "start"]
 ---> Running in 8b18aece356c
Removing intermediate container 8b18aece356c
 ---> bc7eeaceb14d
Successfully built bc7eeaceb14d
Successfully tagged multi-container-application-production_worker:latest
Creating multi-container-application-production_worker_1   ... done
Creating multi-container-application-production_client_1   ... done
Creating multi-container-application-production_redis_1    ... done
Creating multi-container-application-production_postgres_1 ... done
Creating multi-container-application-production_api_1      ... done
Creating multi-container-application-production_nginx_1    ... done
Attaching to multi-container-application-production_redis_1, multi-container-application-production_postgres_1, multi-container-application-production_worker_1, multi-container-application-production_client_1, multi-container-application-production_api_1, multi-container-application-production_nginx_1
client_1    | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
client_1    | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
api_1       |
api_1       | > @ start /app
api_1       | > node index.js
api_1       |
nginx_1     | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
nginx_1     | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
redis_1     | 1:C 09 Jul 2020 10:14:10.969 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis_1     | 1:C 09 Jul 2020 10:14:10.970 # Redis version=6.0.5, bits=64, commit=00000000, modified=0, pid=1, just started
redis_1     | 1:C 09 Jul 2020 10:14:10.970 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
client_1    | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
redis_1     | 1:M 09 Jul 2020 10:14:10.975 * Running mode=standalone, port=6379.
postgres_1  | The files belonging to this database system will be owned by user "postgres".
postgres_1  | This user must also own the server process.
postgres_1  |
client_1    | 10-listen-on-ipv6-by-default.sh: Getting the checksum of /etc/nginx/conf.d/default.conf
postgres_1  | The database cluster will be initialized with locale "en_US.utf8".
postgres_1  | The default database encoding has accordingly been set to "UTF8".
postgres_1  | The default text search configuration will be set to "english".
postgres_1  |
postgres_1  | Data page checksums are disabled.
postgres_1  |
postgres_1  | fixing permissions on existing directory /var/lib/postgresql/data ... ok
worker_1    |
worker_1    | > @ start /app
worker_1    | > node index.js
worker_1    |
nginx_1     | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
client_1    | 10-listen-on-ipv6-by-default.sh: /etc/nginx/conf.d/default.conf differs from the packaged version, exiting
redis_1     | 1:M 09 Jul 2020 10:14:10.976 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
redis_1     | 1:M 09 Jul 2020 10:14:10.976 # Server initialized
redis_1     | 1:M 09 Jul 2020 10:14:10.976 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
postgres_1  | creating subdirectories ... ok
redis_1     | 1:M 09 Jul 2020 10:14:10.979 * Ready to accept connections
postgres_1  | selecting dynamic shared memory implementation ... posix
client_1    | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
postgres_1  | selecting default max_connections ... 100
client_1    | /docker-entrypoint.sh: Configuration complete; ready for start up
postgres_1  | selecting default shared_buffers ... 128MB
postgres_1  | selecting default time zone ... Etc/UTC
postgres_1  | creating configuration files ... ok
postgres_1  | running bootstrap script ... ok
postgres_1  | performing post-bootstrap initialization ... ok
postgres_1  | syncing data to disk ... ok
postgres_1  |
postgres_1  |
postgres_1  | Success. You can now start the database server using:
postgres_1  |
postgres_1  |     pg_ctl -D /var/lib/postgresql/data -l logfile start
postgres_1  |
nginx_1     | 10-listen-on-ipv6-by-default.sh: Getting the checksum of /etc/nginx/conf.d/default.conf
postgres_1  | initdb: warning: enabling "trust" authentication for local connections
postgres_1  | You can change this by editing pg_hba.conf or using the option -A, or
postgres_1  | --auth-local and --auth-host, the next time you run initdb.
postgres_1  | waiting for server to start....2020-07-09 10:14:12.292 UTC [47] LOG:  starting PostgreSQL 12.3 (Debian 12.3-1.pgdg100+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 8.3.0-6) 8.3.0, 64-bit
postgres_1  | 2020-07-09 10:14:12.294 UTC [47] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres_1  | 2020-07-09 10:14:12.309 UTC [48] LOG:  database system was shut down at 2020-07-09 10:14:12 UTC
postgres_1  | 2020-07-09 10:14:12.314 UTC [47] LOG:  database system is ready to accept connections
postgres_1  |  done
postgres_1  | server started
postgres_1  |
postgres_1  | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
postgres_1  |
postgres_1  | waiting for server to shut down....2020-07-09 10:14:12.383 UTC [47] LOG:  received fast shutdown request
postgres_1  | 2020-07-09 10:14:12.384 UTC [47] LOG:  aborting any active transactions
postgres_1  | 2020-07-09 10:14:12.387 UTC [47] LOG:  background worker "logical replication launcher" (PID 54) exited with exit code 1
postgres_1  | 2020-07-09 10:14:12.387 UTC [49] LOG:  shutting down
postgres_1  | 2020-07-09 10:14:12.408 UTC [47] LOG:  database system is shut down
nginx_1     | 10-listen-on-ipv6-by-default.sh: /etc/nginx/conf.d/default.conf differs from the packaged version, exiting
nginx_1     | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
nginx_1     | /docker-entrypoint.sh: Configuration complete; ready for start up
postgres_1  |  done
postgres_1  | server stopped
postgres_1  |
postgres_1  | PostgreSQL init process complete; ready for start up.
postgres_1  |
postgres_1  | 2020-07-09 10:14:12.495 UTC [1] LOG:  starting PostgreSQL 12.3 (Debian 12.3-1.pgdg100+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 8.3.0-6) 8.3.0, 64-bit
postgres_1  | 2020-07-09 10:14:12.496 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
postgres_1  | 2020-07-09 10:14:12.496 UTC [1] LOG:  listening on IPv6 address "::", port 5432
postgres_1  | 2020-07-09 10:14:12.499 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres_1  | 2020-07-09 10:14:12.511 UTC [56] LOG:  database system was shut down at 2020-07-09 10:14:12 UTC
postgres_1  | 2020-07-09 10:14:12.517 UTC [1] LOG:  database system is ready to accept connections
api_1       | Listening
^CGracefully stopping... (press Ctrl+C again to force)
Stopping multi-container-application-production_nginx_1    ... done
Stopping multi-container-application-production_api_1      ... done
Stopping multi-container-application-production_postgres_1 ... done
Stopping multi-container-application-production_client_1   ... done
Stopping multi-container-application-production_redis_1    ... done
Stopping multi-container-application-production_worker_1   ... done
```