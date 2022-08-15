# Attribute Base Access Control Application in Nestjs

## Description

This application uses [Nest](https://github.com/nestjs/nest) to create an Attribute Base Access Control system for your applications. It's inspired by the [Policies system that AWS uses](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_controlling.html)

The policies and users are stored in database, in this case in a MongoDB database. You can assign policies to users to give ability to access to resources o create them

## Extending the Application

You can crete your own modules following [the principles described in Nestjs](https://docs.nestjs.com/modules). Then you need to implement the ABAC security in the controller

- Create a list of actions like the one you can find in [user.actions](src/auth/actions/user.actions.ts) that described the operations that your users can do
- Create the handler for that actions that te one you can find in [user.handler](src/auth/handlers/user.handler.ts)
- Update your controller with the `@CheckPolicies` decorator to check your policies. You can find an example in the [user.controller](src/auth/controllers/user.controller.ts)

### Auto generating new modules

First you have to compile the generator tool

```
npm run build:generator
```

Now you can use it to generate a new module with all the code neccesary (controller, service, tests, ...)

```
npm run generate
```

The schema will be generated without any properties so you have to do it for yourself. As well, you have to create the tests that check the schema and the conditions. You can find these tests searching for `TODO`

## Installation

```bash
$ npm install
```

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## CLI Utils

This project has a CLI to do some actions. If you want to use it you have to compile the CLI tool

```
npm run build:cli
```

Then you can use with the command `npm run cli` follow by the command of the CLI you want to use

### Users command

The CLI has a command called `users` that you can use to do things related with users

#### Create admin user

You can create an admin user using the CLI tool. Just use the sub command `create-admin` and pass the email and the password you want. Here is an example:

```
npm run cli users create-admin foo@example.com bar
```

This will generate an user with email `foo@example.com` with password `bar`. First, it will check if a policy called `Administrator` is in the database. If there is no policy it will create it with all the permissions. The policy `Administrator` will be assign to the user created

## TODOs and improvements
- [ ] Cache JWT lookups
