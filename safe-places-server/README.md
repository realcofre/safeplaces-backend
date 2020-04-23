# Example NodeJS Postgres DB based backend for Safeplaces API

## Deployment

### Deploy in local machine

*Note*: The installation assumes you have already installed Postgres DB in your local environment listening for connections at port 5432.

Clone this repository

```
cd safeplaces-backend
```

#### Install Package Manager

Steps to install NVM are documented [in the nvm repository](https://github.com/nvm-sh/nvm#installing-and-updating).  
  
Install npm using nvm

```
nvm install 13.1.0
nvm use 13.1.0
npm install
```

#### Knex migrations and seed the database

Install Knex globally

```
npm install knex -g
```

Run migrations

```
knex migrate:latest --env test
knex migrate:latest --env development
```

Seed the database

```
knex seed:run --env test
knex seed:run --env development
```

#### Mocha unit tests

Install mocha globally.

```
npm install mocha -g
```

Run testing through mocha to see if unit tests pass

```
mocha
```

### Deploy using Docker

*Note*: The installation assumes you have already installed Postgres DB in your local environment listening for connections at port 5432. Your Postgres instance should listen to '*' instead of 'localhost', this setting can be found in your pgconfig file.

Clone this repository

```
cd safeplaces-backend
```

#### Build Dockerfile

```
docker build -t <docker_repo>/safeplaces-backend-expressjs .
```

#### Run Dockerfile

```
docker run -e NODE_ENV=development -e JWT_SECRET='testtokenforsecurity' -e PORT=3000 -e DATABASE_URL=postgres://<host_machine_ip>/safeplaces_test -p 3000:3000 <docker_repo>/safeplaces-backend-expressjs
```

*Note*: If you are using Mac or Windows your `host_machine_ip` is `host.docker.internal`.