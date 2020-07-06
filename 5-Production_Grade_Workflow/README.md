# Run the Node App using docker-compose with port forwarding and volume
## Run the test case at run time

## Install the node version v8.4.0
S😎MESH~[5-Production_Grade_Workflow (master)]-$ **nvm install v8.4.0**

## Check the node version
S😎MESH~[5-Production_Grade_Workflow (master)]-$ **node -v**
v8.4.0

## List out all the version installed
S😎MESH~[5-Production_Grade_Workflow (master)]-$ **nvm ls**
```
->       v8.4.0
        v8.11.3
        v9.11.2
        v10.4.1
       v12.12.0
default -> 10 (-> v10.4.1)
ws -> 10.4.1 (-> v10.4.1)
node -> stable (-> v12.12.0) (default)
stable -> 12.12 (-> v12.12.0) (default)
iojs -> N/A (default)
unstable -> N/A (default)
lts/* -> lts/erbium (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.21.0 (-> N/A)
lts/erbium -> v12.18.2 (-> N/A)
```

## Install the basic react-app
S😎MESH~[5-Production_Grade_Workflow (master)]-$ **npm install -g create-react-app**
```
/Users/someshprajapati/.nvm/versions/node/v8.4.0/bin/create-react-app -> /Users/someshprajapati/.nvm/versions/node/v8.4.0/lib/node_modules/create-react-app/index.js
+ create-react-app@3.4.1
updated 1 package in 5.012s
```

## Create frontend using create-react-app
S😎MESH~[5-Production_Grade_Workflow (master)]-$ **create-react-app frontend**

## Run the test
S😎MESH~[frontend (master)]-$ **npm run test**
```
 PASS  src/App.test.js
  ✓ renders without crashing (19ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.253s
Ran all test suites related to changed files.

Watch Usage
 › Press a to run all tests.
 › Press o to only run tests related to changed files.
 › Press p to filter by a filename regex pattern.
 › Press q to quit watch mode.
 › Press Enter to trigger a test run.
```

## Build the app
S😎MESH~[frontend (master)]-$ **npm run build**
```
> frontend@0.1.0 build /Users/someshprajapati/Documents/MyLearning/WorkSpan/Docker and Kubernetes-The Complete Guide/Exercise/Docker/5-Production_Grade_Workflow/frontend
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  44.68 KB  build/static/js/main.801fd914.js
  264 B     build/static/css/main.40b4a62f.css

The project was built assuming it is hosted at the server root.
To override this, specify the homepage in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage": "http://myname.github.io/myapp",

The build folder is ready to be deployed.
You may serve it with a static server:

  yarn global add serve
  serve -s build
```

## multiple directory got created after build
S😎MESH~[frontend (master)]-$ **ls -l**
```
total 720
-rw-r--r--    1 someshprajapati  staff   80668 Jul  6 13:08 README.md
drwxr-xr-x    6 someshprajapati  staff     192 Jul  6 13:13 build
drwxr-xr-x  828 someshprajapati  staff   26496 Jul  6 13:08 node_modules
-rw-r--r--    1 someshprajapati  staff     371 Jul  6 13:08 package.json
drwxr-xr-x    4 someshprajapati  staff     128 Jul  6 13:08 public
drwxr-xr-x    8 someshprajapati  staff     256 Jul  6 13:08 src
-rw-r--r--    1 someshprajapati  staff  282453 Jul  6 13:08 yarn.lock

S😎MESH~[frontend (master)]-$ ls build/static/js/main.801fd914.js
build/static/js/main.801fd914.js
```

## Run the development server
S😎MESH~[frontend (master)]-$ **npm run start**
```
Compiled successfully!

The app is running at:

  http://localhost:3000/

Note that the development build is not optimized.
To create a production build, use yarn run build.
```

## Create the Dockerfile
S😎MESH~[frontend (master)]-$ **cat Dockerfile.dev**
```
───────┬───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: Dockerfile.dev
───────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ # Specify a base image
   2   │ FROM node:alpine
   3   │
   4   │ # Specify a working directory
   5   │ WORKDIR '/app'
   6   │
   7   │ # Install some depenendencies
   8   │ COPY package.json .
   9   │ RUN npm install
  10   │ COPY ./ ./
  11   │
  12   │ # Default command
  13   │ CMD ["npm", "run", "start"]
───────┴───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

## Build using Docker file, OOPS-not able to find the Dockerfile because our Dockerfile name is different
S😎MESH~[frontend (master)]-$ **docker build .**
```
unable to prepare context: unable to evaluate symlinks in Dockerfile path: lstat /Users/someshprajapati/Documents/MyLearning/WorkSpan/Docker and Kubernetes-The Complete Guide/Exercise/Docker/5-Production_Grade_Workflow/frontend/Dockerfile: no such file or directory
```

## Build image using custom name Docker file
S😎MESH~[frontend (master)]-$ **docker build -f Dockerfile.dev .**
```
Sending build context to Docker daemon  112.3MB
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> ef49b8be9f94
Step 3/6 : COPY package.json .
 ---> 7d9d5a594d89
Step 4/6 : RUN npm install
 ---> Running in 7560ed1cac39
added 979 packages from 671 contributors and audited 1100 packages in 43.476s
6 packages are looking for funding
  run `npm fund` for details

found 426 vulnerabilities (362 low, 35 moderate, 28 high, 1 critical)
  run `npm audit fix` to fix them, or `npm audit` for details
Removing intermediate container 7560ed1cac39
 ---> 2dcc664a1daa
Step 5/6 : COPY ./ ./
 ---> 4ded18c0aa98
Step 6/6 : CMD ["npm", "run", "start"]
 ---> Running in 149859b756be
Removing intermediate container 149859b756be
 ---> 537b2d90aeab
Successfully built 537b2d90aeab
```

## Check the running container
S😎MESH~[frontend (master)]-$ **docker ps**
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

## Run the container
S😎MESH~[frontend (master)]-$ **docker run 537b2d90aeab**
```
> frontend@0.1.0 start /app
> react-scripts start
Starting the development server...
Compiled successfully!

The app is running at:
  http://localhost:3000/

Note that the development build is not optimized.
To create a production build, use yarn run build.
```

## Run the container with port mapping
S😎MESH~[frontend (master)]-$ **docker run -p 3000:3000 537b2d90aeab**
```
> frontend@0.1.0 start /app
> react-scripts start

Starting the development server...
Compiled successfully!

The app is running at:
  http://localhost:3000/

Note that the development build is not optimized.
To create a production build, use yarn run build.
```

## Run the container with volumes
S😎MESH~[frontend (master)]-$ **docker run -p 3000:3000 -v /app/node_modules -v /Users/someshprajapati/Documents/MyLearning/WorkSpan/Docker\ and\ Kubernetes-The\ Complete\ Guide/Exercise/Docker/5-Production_Grade_Workflow/frontend:/app 537b2d90aeab**
```
> frontend@0.1.0 start /app
> react-scripts start

Starting the development server...
Compiled successfully!

The app is running at:
  http://localhost:3000/

Note that the development build is not optimized.
To create a production build, use yarn run build.

Compiling...
Compiled successfully!
Compiling...
Compiled successfully!
```

## Run the app using docker-compose
S😎MESH~[frontend (master)]-$ **docker-compose up**
```
Building web
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> ef49b8be9f94
Step 3/6 : COPY package.json .
 ---> 751c6e30f0b2
Step 4/6 : RUN npm install
 ---> Running in 54a34aa4285f
added 979 packages from 671 contributors and audited 1100 packages in 44.293s
6 packages are looking for funding
  run `npm fund` for details

found 426 vulnerabilities (362 low, 35 moderate, 28 high, 1 critical)
  run `npm audit fix` to fix them, or `npm audit` for details
Removing intermediate container 54a34aa4285f
 ---> 1552b695cbfd
Step 5/6 : COPY ./ ./
 ---> 804068199811
Step 6/6 : CMD ["npm", "run", "start"]
 ---> Running in 42bbd392dfbe
Removing intermediate container 42bbd392dfbe
 ---> b0d79210c2ae
Successfully built b0d79210c2ae
Successfully tagged frontend_web:latest
web_1  | Compiled successfully!
web_1  |
web_1  | The app is running at:
web_1  |
web_1  |   http://localhost:3000/
web_1  |
web_1  | Note that the development build is not optimized.
web_1  | To create a production build, use yarn run build.
web_1  |
web_1  | Compiling...
web_1  | Compiled successfully!
```

## Build the image using Dockerfile
S😎MESH~[frontend (master)]-$ **docker build -f Dockerfile.dev .**
```
Sending build context to Docker daemon  112.3MB
Step 1/6 : FROM node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Using cache
 ---> ef49b8be9f94
Step 3/6 : COPY package.json .
 ---> Using cache
 ---> 827a2a284817
Step 4/6 : RUN npm install
 ---> Using cache
 ---> 2ed14ea8b946
Step 5/6 : COPY ./ ./
 ---> Using cache
 ---> 0fdb03632a20
Step 6/6 : CMD ["npm", "run", "start"]
 ---> Using cache
 ---> b3f0d9884387
Successfully built b3f0d9884387
```

## Run the test case using override default command
S😎MESH~[frontend (master)]-$ **docker run b3f0d9884387 npm run test**
```
 PASS  src/App.test.js
  ✓ renders without crashing (43ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.968s
Ran all test suites.

Watch Usage
 › Press p to filter by a filename regex pattern.
 › Press q to quit watch mode.
 › Press Enter to trigger a test run.
  console.error node_modules/react-dom/cjs/react-dom.development.js:88
    Warning: validateDOMNesting(...): <h2> cannot appear as a descendant of <p>.
        in h2 (at App.js:14)
        in p (at App.js:13)
        in div (at App.js:8)
        in App (at App.test.js:7)
```

## Update the docker-compose file to run test at runtime (service: test)
S😎MESH~[frontend (master)]-$ **cat docker-compose.yml**
```
───────┬───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: docker-compose.yml
───────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ version: '3'
   2   │ services:
   3   │     web:
   4   │         build:
   5   │             context: .
   6   │             dockerfile: Dockerfile.dev
   7   │         ports:
   8   │             - "3000:3000"
   9   │         volumes:
  10   │             - /app/node_modules
  11   │             - .:/app
  12   │     tests:
  13   │         build:
  14   │             context: .
  15   │             dockerfile: Dockerfile.dev
  16   │         volumes:
  17   │             - /app/node_modules
  18   │             - .:/app
  19   │         command: ["npm", "run", "test"]
───────┴───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

## Build and run the container using docker-compose
S😎MESH~[frontend (master)]-$ **docker-compose up --build**
```
 PASS  src/App.test.js
tests_1  |   ✓ renders without crashing (6ms)
tests_1  |   ✓ renders without crashing (3ms)
tests_1  |
tests_1  | Test Suites: 1 passed, 1 total
tests_1  | Tests:       2 passed, 2 total
tests_1  | Snapshots:   0 total
tests_1  | Time:        0.151s, estimated 1s
tests_1  | Ran all test suites.
tests_1  |
tests_1  | Watch Usage
tests_1  |  › Press p to filter by a filename regex pattern.
tests_1  |  › Press q to quit watch mode.
tests_1  |  › Press Enter to trigger a test run.
tests_1  |
```