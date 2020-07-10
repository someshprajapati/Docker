# Basic React App with Travis-CI Integration

## Build the image 
S😎MESH~[docker-travis-integration]-$ **docker build -f Dockerfile.dev .**
```
Sending build context to Docker daemon  887.8kB
Step 1/6 : FROM node:alpine
alpine: Pulling from library/node
cbdbe7a5bc2a: Pull complete
bdfc8e0b7a31: Pull complete
b0f8983c8893: Pull complete
057ed1351239: Pull complete
Digest: sha256:ae13d1ab371853dc03590ddee6b0901f0c66c3e107e78dc26e4bd673a7334b41
Status: Downloaded newer image for node:alpine
 ---> 5d97b3d11dc1
Step 2/6 : WORKDIR '/app'
 ---> Running in 863688c432f4
Removing intermediate container 863688c432f4
 ---> 8f6dd7567a83
Step 3/6 : COPY package.json .
 ---> 09d8ded5990f
Step 4/6 : RUN npm install
 ---> Running in 39df69638176
> core-js@2.6.11 postinstall /app/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon:
> https://opencollective.com/core-js
> https://www.patreon.com/zloirock

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)

added 979 packages from 671 contributors and audited 1100 packages in 31.504s

6 packages are looking for funding
  run `npm fund` for details

found 101 vulnerabilities (37 low, 35 moderate, 28 high, 1 critical)
  run `npm audit fix` to fix them, or `npm audit` for details
Removing intermediate container 39df69638176
 ---> 2ae5160c767c
Step 5/6 : COPY . .
 ---> acf23de7af2e
Step 6/6 : CMD ["npm", "run", "start"]
 ---> Running in 059c60fc8f4b
Removing intermediate container 059c60fc8f4b
 ---> 7c49df2d9b6b
Successfully built 7c49df2d9b6b
```

## Run the test case
S😎MESH~[docker-travis-integration]-$ **docker run -it 7c49df2d9b6b npm run test -- --coverage**
```
> frontend@0.1.0 test /app
> react-scripts test --env=jsdom "--coverage"

 PASS  src/App.test.js
  ✓ renders without crashing (41ms)
  ✓ renders without crashing (3ms)

----------|----------|----------|----------|----------|-------------------|
File      |  % Stmts | % Branch |  % Funcs |  % Lines | Uncovered Line #s |
----------|----------|----------|----------|----------|-------------------|
All files |       50 |      100 |      100 |       50 |                   |
 App.js   |      100 |      100 |      100 |      100 |                   |
 index.js |        0 |      100 |      100 |        0 |                 1 |
----------|----------|----------|----------|----------|-------------------|
Handlebars: Access has been denied to resolve the property "statements" because it is not an "own property" of its parent.
You can add a runtime option to disable the check or this warning:
See https://handlebarsjs.com/api-reference/runtime-options.html#options-to-control-prototype-access for details
Handlebars: Access has been denied to resolve the property "branches" because it is not an "own property" of its parent.
You can add a runtime option to disable the check or this warning:
See https://handlebarsjs.com/api-reference/runtime-options.html#options-to-control-prototype-access for details
Handlebars: Access has been denied to resolve the property "functions" because it is not an "own property" of its parent.
You can add a runtime option to disable the check or this warning:
See https://handlebarsjs.com/api-reference/runtime-options.html#options-to-control-prototype-access for details
Handlebars: Access has been denied to resolve the property "lines" because it is not an "own property" of its parent.
You can add a runtime option to disable the check or this warning:
See https://handlebarsjs.com/api-reference/runtime-options.html#options-to-control-prototype-access for details
Test Suites: 1 passed, 1 total
Tests:       2 passed, 2 total
Snapshots:   0 total
Time:        0.941s
Ran all test suites.
  console.error node_modules/react-dom/cjs/react-dom.development.js:88
    Warning: validateDOMNesting(...): <h2> cannot appear as a descendant of <p>.
        in h2 (at App.js:14)
        in p (at App.js:13)
        in div (at App.js:8)
        in App (at App.test.js:7)

  console.error node_modules/react-dom/cjs/react-dom.development.js:88
    Warning: validateDOMNesting(...): <h2> cannot appear as a descendant of <p>.
        in h2 (at App.js:14)
        in p (at App.js:13)
        in div (at App.js:8)
        in App (at App.test.js:12)
```