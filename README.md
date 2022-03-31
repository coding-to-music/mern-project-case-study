## Project Case study MERN app to document apps calling GitHub API

The note taking functionality does not work.

Search for text and the GitHub API returns data that are displayed using cards.

## mern-project-case-study

https://github.com/coding-to-music/mern-project-case-study

https://mern-project-case-study.herokuapp.com/

By pramitmarattha pramit-marattha https://github.com/pramit-marattha

https://github.com/pramit-marattha/mern-project-case-study-app

## Installation:

## Procfile for however to start the Client

Procfile

```java
web: npm run start:client
```

## Modify server/index.js

```java
app.use(express.static(path.resolve(__dirname, "../react-ui/build")));

// Priority serve any static files.
app.use(express.static(path.resolve(__dirname, "../react-ui/build")));
```

### Project Directory Structure

```java
tree -d -L 2
.
├── client
│   ├── build
│   ├── node_modules
│   ├── public
│   └── src
├── node_modules
└── server
    ├── controllers
    ├── database
    ├── models
    └── routes
```

### Package.json

key items in package.json

- cacheDirectories for Heroku to save time on builds

- engine set the node version to use

main scripts

`npm run` and any of the scripts below:

- install
- build
- start
- deploy

```java
{
  "name": "project-case-study-mern-server",
  "version": "1.0.0",
  "description": "take notes while exploring projects",
  "main": "index.js",
  "engines": {
    "node": "16.x"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server",
    "build": "cd client/ && npm install && npm run build",
    "watch": "nodemon server",
    "deploy": "git add . && git commit -m Heroku && git push && git push heroku",
    "install:client": "cd client && npm install --production=false",
    "build:client": "cd client && npm run build",
    "install:server": "npm install --production=false",
    "install:server:client": "concurrently \"npm install --production=false\" \"npm install:client\"  \"npm install:server\"",
    "start:client": "cd client && npm run start",
    "start:server": "npm run start",
    "start:all": "concurrently \"npm run start:client\" \"npm run start:server\""
  },
  "keywords": [
    "mern"
  ],
  },
  "cacheDirectories": [
    "node_modules",
    "client/node_modules"
  ]
}
```

### GitHub

```java
nvm use v16
npx browserslist@latest --update-db
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/mern-project-case-study.git
git push -u origin main
```

### Heroku

```java
heroku create mern-project-case-study

heroku run npx browserslist@latest --update-db
```

### .env MongoDB Environment Variables

```java
MONGODB_URI="mongodb+srv://<userid>:<password>@cluster0.zadqe.mongodb.net/mern-project-case-study?retryWrites=true&w=majority"
```

### Heroku MongoDB Environment Variables

```java
heroku config:set MONGODB_URI="mongodb+srv://<userid>:<password>@cluster0.zadqe.mongodb.net/mern-project-case-study?retryWrites=true&w=majority"
git push heroku
```

### Heroku Buildpack

See this repo for more info about setting up a node/react app on heroku:

https://github.com/mars/heroku-cra-node

```java
heroku buildpacks

heroku buildpacks --help

heroku buildpacks:clear

```

### Notice we are doing a SET and then and ADD

```java
heroku buildpacks:set heroku/nodejs

heroku buildpacks:add mars/create-react-app

```

Output:

```java
Buildpack added. Next release on mern-project-case-study will use:
  1. heroku/nodejs
  2. mars/create-react-app
Run git push heroku main to create a new release using these buildpacks.
```

### Lets try reversing the order

```java
heroku buildpacks:set mars/create-react-app

heroku buildpacks:add heroku/nodejs
```

```java
heroku buildpacks
```

Output:

```java
=== mern-project-case-study Buildpack URLs
1. mars/create-react-app
2. heroku/nodejs
```

### Push to Heroku

```
git push heroku
```

## Error:

```java
2022-03-29T08:06:58.791397+00:00 heroku[web.1]: Starting process with command `npm start`
2022-03-29T08:06:59.934025+00:00 app[web.1]: ls: cannot access '/client/build/static/js/*.js': No such file or directory
2022-03-29T08:06:59.938326+00:00 app[web.1]: Error injecting runtime env: bundle not found '/client/build/static/js/*.js'. See: https://github.com/mars/create-react-app-buildpack/blob/master/README.md#user-content-custom-bundle-location
```

Attempted this:

```java
heroku config:set JS_RUNTIME_TARGET_BUNDLE=./client/build/static/js/*.js

heroku run npx browserslist@latest --update-db

heroku run npm i tree && tree -d -L 2

```

## Local Development

Because this app is made of two npm projects, there are two places to run `npm` commands:

1. **Node API server** at the root `./`
1. **React UI** in `react-ui/` directory.

### Run the API server

In a terminal:

```bash
# Initial setup
npm install

# Start the server
npm start
```

#### Install new npm packages for Node

```bash
npm install package-name --save
```

### Run the React UI

The React app is configured to proxy backend requests to the local Node server. (See [`"proxy"` config](react-ui/package.json))

In a separate terminal from the API server, start the UI:

```bash
# Always change directory, first
cd react-ui/

# Initial setup
npm install

# Start the server
npm start
```

#### Install new npm packages for React UI

```bash
# Always change directory, first
cd react-ui/

npm install package-name --save
```
