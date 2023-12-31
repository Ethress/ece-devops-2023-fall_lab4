
# Lab

Continuous Integration & Continuous Delivery (Deployment) (CI/CD)

## Objectives

1. Part 1. Continuous Integration with GitHub Actions
2. Part 2. Continuous Delivery (Deployment) with Heroku

## Before starting

Before starting configuring CI/CD to a software project, you need to have its repository on GitHub.

> Note. Skip the following steps if you already have a repository on GitHub containing the application from the previous [Continuous Testing lab](../04.continuous-testing/lab.md).

1. Create a Git repository for the User API project imported from [../03.continuous-testing/lab/](../03.continuous-testing/lab/), and commit all the files. 
2. Create a remote repository on GitHub, link it with the local one, and push the changes.

## Part 1. Continuous Integration with GitHub Actions

1. Read the [introduction to GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/introduction-to-github-actions).

2. Create a CI workflow for the Node.js using this [documentation](https://docs.github.com/en/actions/guides/building-and-testing-nodejs). 

> Note. Don't forget to commit and push your workflow configuration in the `.github/workflows` folder **under the root** of you Git repository.

Does your workflow work? Is there any problem with the connection to Redis?

3. Improve your Workflow to connect Node.js application to Redis using this documentation:
  - [About service containers](https://docs.github.com/en/actions/guides/about-service-containers)
  - [Creating Redis service containers](https://docs.github.com/en/actions/guides/creating-redis-service-containers)

4. Practice a regular workflow of the software development life cycle, for example for completing the [Lab 3 instructions](../03.continuous-testing/lab.md). 

Create a pull request to the `master` branch:

- create a new branch and publish it to your remote GitHub repository
- make any change in your source code, commit and push it
- make a **Pull Request** on GitHub
- wait for GitHub Actions to test it (observe the process on GitHub -> Actions page)
- review the commit and Merge this Pull Request into the `master` branch

5. Explore the GitHub Actions log on GitHub (under the "Actions" tab).

## Part 2. Continuous Delivery (Deployment) with Heroku

As of November 28th 2022, Heroku [stops the free tier](https://blog.heroku.com/next-chapter). You can use the alternative instructions provided [Here](./azure-webapp/webapp-tuto.md) to deploy a webb app with Microsoft Azure Cloud.

The following instructions for Heroku are now legacy.

1. Create an account on [Heroku](https://heroku.com)

2. Create an app on [Heroku](https://dashboard.heroku.com/new-app) and configure it.

Under the "Deploy tab" do:

  - sync the app with the GitHub repository

3. Add Redis service to Heroku deployment - https://elements.heroku.com/addons/heroku-redis

> Note. Redis service on Heroku is free, but it requires adding credit card information. Considering this limitation we will not run Redis on Heroku, and the application will be partially non-functional (it will print the "Hello world!" message on the home page, but the user API will not work). However, it will be enough to experience our CI/CD pipeline.

4. Configure the workflow to deploy to Heroku using [this guide](https://github.com/marketplace/actions/deploy-to-heroku).

5. Practice a regular workflow of the software development life cycle like in Part 2.

6. Test your public domain on Heroku.

## Bonus tasks

1. Integrate Swagger UI using this package - https://www.npmjs.com/package/express-swagger-generator






=====================================================================================================================================================================





# User API web application

It is a basic NodeJS web application exposing REST API that creates and stores user parameters in [Redis database](https://redis.io/).

## Functionality

1. Start a web server
2. Create a user
2. Get a user

## Installation

This application is written on NodeJS and it uses Redis database.

1. [Install NodeJS](https://nodejs.org/en/download/)

2. [Install Redis](https://redis.io/download)

3. Install application

Go to the root directory of the application (where `package.json` file located) and run:

```
npm install 
```

## Usage

1. Start a web server

From the root directory of the project run:

```
npm start
```

It will start a web server available in your browser at http://localhost:3000.

2. Create a user

Send a POST (REST protocol) request using terminal:

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"username":"sergkudinov","firstname":"sergei","lastname":"kudinov"}' \
  http://localhost:3000/user
```

It will output:

```
{"status":"success","msg":"OK"}
```

Another way to test your REST API is to use [Postman](https://www.postman.com/).

## Testing

From the root directory of the project, run:

```
npm test
```
