# Run the Node App with Nginx using Multistep Dockerfile
1. Build Step
2. Run Step

## Multistep Dockerfile (Build + Run Steps)
S😎MESH~[frontend (master)]-$ **cat Dockerfile**
```
───────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: Dockerfile
───────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ # Build Phase
   2   │ FROM node:alpine as builder
   3   │ WORKDIR '/app'
   4   │ COPY package.json .
   5   │ RUN npm install
   6   │ COPY ./ ./
   7   │ RUN npm run build
   8   │
   9   │ # Run Phase
  10   │ FROM nginx
  11   │ COPY --from=builder /app/build /usr/share/nginx/html
───────┴───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

## Build the image
S😎MESH~[frontend (master)]-$ **docker build .**
```
Sending build context to Docker daemon  112.3MB
Step 1/8 : FROM node:alpine as builder
 ---> 5d97b3d11dc1
Step 2/8 : WORKDIR '/app'
 ---> Using cache
 ---> ef49b8be9f94
Step 3/8 : COPY package.json .
 ---> Using cache
 ---> 827a2a284817
Step 4/8 : RUN npm install
 ---> Using cache
 ---> 2ed14ea8b946
Step 5/8 : COPY ./ ./
 ---> 676c6f854fcb
Step 6/8 : RUN npm run build
 ---> Running in d83178ced448

> frontend@0.1.0 build /app
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  44.65 KB (-31 B)  build/static/js/main.98b1c6d3.js
  264 B             build/static/css/main.40b4a62f.css

The project was built assuming it is hosted at the server root.
To override this, specify the homepage in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage": "http://myname.github.io/myapp",

The build folder is ready to be deployed.
You may serve it with a static server:

  yarn global add serve
  serve -s build

Removing intermediate container d83178ced448
 ---> e82bc0095034
Step 7/8 : FROM nginx
latest: Pulling from library/nginx
8559a31e96f4: Already exists
8d69e59170f7: Pull complete
3f9f1ec1d262: Pull complete
d1f5ff4f210d: Pull complete
1e22bfa8652e: Pull complete
Digest: sha256:21f32f6c08406306d822a0e6e8b7dc81f53f336570e852e25fbe1e3e3d0d0133
Status: Downloaded newer image for nginx:latest
 ---> 2622e6cca7eb
Step 8/8 : COPY --from=builder /app/build /usr/share/nginx/html
 ---> a5d974c5df47
Successfully built a5d974c5df47
```

## Run the container with port forwarding
S😎MESH~[frontend (master)]-$ **docker run -p 8080:80 a5d974c5df47**
```
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up

172.17.0.1 - - [06/Jul/2020:11:13:01 +0000] "GET / HTTP/1.1" 200 378 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:77.0) Gecko/20100101 Firefox/77.0" "-"
172.17.0.1 - - [06/Jul/2020:11:13:01 +0000] "GET /static/css/main.40b4a62f.css HTTP/1.1" 200 358 "http://localhost:8080/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:77.0) Gecko/20100101 Firefox/77.0" "-"
172.17.0.1 - - [06/Jul/2020:11:13:01 +0000] "GET /static/js/main.98b1c6d3.js HTTP/1.1" 200 144349 "http://localhost:8080/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:77.0) Gecko/20100101 Firefox/77.0" "-"
172.17.0.1 - - [06/Jul/2020:11:13:01 +0000] "GET /static/media/logo.5d5d9eef.svg HTTP/1.1" 200 2671 "http://localhost:8080/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:77.0) Gecko/20100101 Firefox/77.0" "-"
172.17.0.1 - - [06/Jul/2020:11:13:01 +0000] "GET /favicon.ico HTTP/1.1" 200 24838 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:77.0) Gecko/20100101 Firefox/77.0" "-"
```