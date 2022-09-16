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
