# Notes

**source**: https://medium.com/@gausmann.simon/nestjs-typeorm-and-postgresql-full-example-development-and-project-setup-working-with-database-c1a2b1b11b8f

- We'll work on a simple NodeJS API that is powered by a PostgreSQL database
  for data storage and setup some tooling around it to make dev's life better.

- The setup -> NestJS and TypeORM connected to a PostgreSQL DB in a docker
  container

- To build the API in NodeJS we will use NestJS. It's a pretty flexible
  framework and is built on ExpressJS principles and lets you craft out
  NodeJS services in no time as it comes with a lot of goodies: - like full typescipt support, - dependency injection, - module management and a lot more

- We'll use the TypeORM to manage our database schema. What is nice about
  TypeORM is, that it allows you to model your data entities in type save
  code (TypeScript) and then is able to apply/sync these models into the
  table structure in your database. (By the way, this not only works with
  PostgreSQL databases, but also other databases)

### Setting up a local PostgreSQL database instance - with docker automation!

- To work locally with data persistence, we now would need a database server
  and a database to connect to.

- We use pre-build PostgreSQL docker image and run the database server as a
  docker process. Like this we can script a whole setup with a couple lines of
  shell code to get out server instance running and prepare an empty database
  ready to connect to.

- This is great because it's reproducible and the setup code can be managed
  in source control together with the rest of the project code, what makes
  the "getting started" for other dev's in your team super straightforward.

- Here is how this script would look like:

```
#!/bin/bash

SERVER="my_database_server"
PW="mysecretpassword"
DB="my_database"

echo "echo stop & remove old docker [$SERVER] and starting new fresh
instance of [$SERVER]"

(docker kill $SERVER || :) && \
    (docker rm $SERVER || :) && \
    docker run --name $SERVER -e POSTGRESQL_PASSWORD=$PW \
    -e PGPASSWWORD=$PW \
    -p 5432:5432 \
    - postgres

# wait for pg to start
echo "sleep wait for pg-server [$SERVER] to start";
SLEEP 3;

# create the db
echo "CREATE DATABASE $DB ENCODING 'UTF-8'; | docker exec -i $SERVER psql -U postgres
echo "\l" | docker exec -i $SERVER psql -U postgres
```

- Lets add that command to out `package.json` run-scripts so we can easy execute
  it.

```
start:dev:db: "./src/scripts/start-db.sh"
```

- We have a command we can run and it would setup the database server and a
  plain database to start with.

- To make the process more robust, we will always use the same name for the
  docker container ($SERVER var in the script) - like this we can add an
  additional check - if the container is running already kill and remove it to
  ensure a clean state.

### Connecting NestJS to your database:

- Let's add TypeORM support to our project by using the pre-build
  NestJS-to-TypeORM module:

```
npm install --save @nestjs/typeorm typeorm pg
```

### Configuration Management:

- The way we can tell TypeORM in NestJS to which database server to connect to,
  is by using the TypeOrmModule.

- It has a forRoot method we can pass the config in.

> But here is the challenge. We know that the config will be different on
> local development and on the production environment. So, this process somehow
> has to be generic so it can provide different config for these cases.

- To make this work nicely we can write the following config service.

-
