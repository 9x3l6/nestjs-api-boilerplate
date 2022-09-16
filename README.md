# NestJS API Boilerplate

This is a good starting point for an api application that uses nodejs.

The commands below were used to create or generate this boilerplate which you can use as a great starting point for your apps.

- [https://docs.nestjs.com/](https://docs.nestjs.com/)

Make sure you have nodejs installed. I like to have [nvs (Node Version Switcher)](https://github.com/jasongin/nvs) installed so to change the nodejs version on my machine anytime I need.

After installing it just type `nvs` to set what nodejs version you want to use.

```shell
nvs
```

Then install `nestjs-cli` so you can create the project and get the party started.

```shell
npm i -g @nestjs/cli
```

Run the command below to create our app. This will create a directory named `webapi` in the current directory with all the project files for our nestjs app.

```shell
$ nest new webapi
$ cd webapi
# remove the .git directory which has all the nestjs history, we have our own git history as it is
$ rm -rf .git
$ npm run start
```

Alternatively, to install the TypeScript Project use git clone to download the code into the `webapi` directory inside the current directory.

```shell
git clone https://github.com/nestjs/typescript-starter.git webapi
$ cd webapi
# remove the .git directory which has all the nestjs history, we have our own git history as it is
$ rm -rf .git
$ npm install
$ npm run start
```

Next you need to create a database container for the webapi to use for storing all the data your app will have.

Firstly we need a file to securely hold our database credentials and other things like secret keys. Make sure to add this file to `.gitignore` so that it doesn't get added to the files uploaded to git and so no one can see your secret that are stored in this file. When the application is deployed we will be able to provide these details so that things will work.

```ini
POSTGRES_PASSWORD=password
```

Create a `docker-compose.yml` file inside the `webapi/` directory having the contents below:

- Notice: we are loading the `.env` file having our secrets with the `env_file:` docker-compose configuration option.
- Notice: we are using docker-compose to create a network for this project having the project name. If you have multiple project using the same network name or volume name and try to start the apps it may not work as expected.

```yaml
version: "3"

services:
  db:
    image: postgres
    restart: always
    ports:
      - "5432:5432"
    env_file:
      - .env
  redis:
    image: 'redis:alpine'
    ports:
      - '${FORWARD_REDIS_PORT:-6379}:6379'
    volumes:
      - 'nestjs-api-boilerplate-redis:/data'
    networks:
      - nestjs-api-boilerplate
    healthcheck:
        test: ["CMD", "redis-cli", "ping"]
        retries: 3
        timeout: 5s
networks:
  nestjs-api-boilerplate:
    driver: bridge
volumes:
  nestjs-api-boilerplate-pgsql:
    driver: local
  nestjs-api-boilerplate-redis:
      driver: local
```

To start the database service and the redis service run this command below:

```shell
docker-compose up -d
```

To start only the database service you can just add the name of the service to the command above.

```shell
docker-compose up -d <name>
docker-compose up -d db
```

When you're done you can run `docker-compose stop` or ` docker-compose kill` to stop all of the services. Or just like with the `up` command you can specify the service name to stop.

Later you will most likely want to add more services that your application will be using in order to operate effeciently. For now having a databse server and a redis cache server is a good start and you can do a lot just with this setup.

Next we will be adding `Authentication and Authorization` functionality to the webapi so that users can create an account with username, email and password and then login and logout.

You'll want to install [Insomnia](https://insomnia.rest/) to make requests to the api until we build a frontend to handle that for us. It's better than running curl commands from the terminal, more feature rich. Insomnia can export the requests you make, to be ran as curl commands from the terminal instead of the app interface.

Are you looking for a Technical Writer? Are you looking for a Full-Stack Web Developer? Are you looking for a Tech Lead to support a team of junior developers? Maybe you found this page useful and want to [buy me a coffee](https://buymeacoffee.com/alexgoretoy). As of Sept. 2022 I'm looking for a new job, let's talk. email alex@goretoy.com to connect with me.

If you'd like to learn the ins and outs of nestjs you can sign up for the course from the guys who wrote the framework. The [fundamentals course - $39.99](https://learn.nestjs.com/p/fundamentals) and as of Sept 2022 they are making [Authorization and Authorization course - $49.99](https://learn.nestjs.com/p/authentication-and-authorization) you can pre-order it to save %25. You don't have to take these courses to learn nestjs, however it is the best way to learn it along with reading the documentation. It's 2022 and there are youtube videos and blog posts you can find that will show you how things work and how people are using it to solve real world problems.
