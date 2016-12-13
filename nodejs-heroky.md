### Prerequisites
* Node.js and npm installed.
* Github Account + Git installed
* a free Heroku account.
* the Heroku CLI.

### Creation of a Git Repository

Our source code is going to be stored in a Git repository. Heroku uses Git for deployment, and it's also a better habit to use git.

To create a new empty repository, run on a terminal:


    $ mkdir myapp
    $ cd myapp
    $ git init


We are now going to work on this `myapp` folder.

You can also host this repository on [GitHub][1], this is optional but advised:

1. Create a repository on GitHub
2. On a terminal in the `myapp` folder run: `git remote set-url upstream `

The url for the repository on GitHub is in the format: `https://github.com//.git`.

### Creation of a base for a Node.js application

Now that our git repository is ready, we can start working on writting our node.js application.

In a terminal in the `myapp` folder, run:


    $ npm init


It will ask you for multiple questions and generate a `package.json` file. This file will contain the list of your dependencies (the librairies our program will depend on) and some others descriptives informations.

### Commit our base

It's time to commit our first commit for this application:


    $ git add package.json
    $ git commit -m "Base package.json"


And push it to GitHub:


    $ git push


[1]: https://github.com


## Coding the application | Heroku + Node.JS

Now that the git repository and the node module structure are setup, we are ready to start coding the application.

This application will be a simple hello world.

### Instaling our dependencies

In node.js, the dependencies are listed in the **package.json** file. All dependencies from this file can be installed using the command `npm install .`.

An other dependency can be installed and added to the package.json using: `npm install name@version --save`.

Our application will depend on: `express@4.3.1`.

So install it using:


    $ npm install express@4.3.1 --save


### Hello World

[Express][1] is web application framework for node, it makes it really easy to write web application using node.

Write in a file named **main.js**:


    var express = require("express");
    var app = express();

    app.get('/', function(req, res) {
      res.send('Hello World!');
    });

    var port = Number(process.env.PORT || 5000);
    app.listen(port, function() {
      console.log("Listening on " + port);
    });


This code will simply create an application using Express. Define an handling method for a get request on the root path. And start the web server on the port defined by the environment variable `PORT` or `5000`.

### Run Script

Heroku convention needs a `Procfile` file that defines how to start the application. You can learn more about **Procfile** in the [Heroku documentation][2].

Write in a file named **Procfile**:


    web: node main.js


This file simply tell Heroku that for starting this application, it needs to start a web dyno by running the command `node main.js`.

[1]: http://expressjs.com/
[2]: https://devcenter.heroku.com/articles/procfile



## Deployment | Heroku + Node.JS

We just test our application, and it's working fine. Now it's time to deploy it on Heroku to make it available for everybody.

### Create an application on Heroku

If you haven't already, sign up on [Heroku][1]. It's free and easy!

Click on the button "Create a new app" and enter a name for your application. You can select the region that you want, it doesn't change anything for the deployment.

### Install the Heroku Command Line Tool

First, install the Heroku Toolbelt on your local workstation. You can find it at [toolbelt.heroku.com][2].

### Commit your changes

The first is to commit your changes (main.js and Procfile):

List all the changes that needs using:


    $ git status


You can see that the folder `node_modules` is contained in the list. This folder contains all the dependencies, we installed using **NPM**. We need to add this folder to a `.gitignore` file:

Copy and paste the content of [GitHub Node .gitignore][3] to a file named `.gitignore`.

If you run `git status` again, you can see that `node_modules/` is no longer present in the list.

You can now commit the other changes using:


    $ git add .
    $ git commit -m "Base code"


### Pushing to Heroku

It is now time to push to Heroku. In the configuration or homepage of your Heroku application, you can see a GIT url with the following format:


    git@heroku.com:{{ application name }}.git


To deploy a new release of your application, simply run:


    $ git push heroku master


Heroku will log the installation of the node dependencies and the launch of your application.

Once it's done you can open your application using:


    $ heroku open


[1]: https://heroku.com
[2]: https://toolbelt.heroku.com/
[3]: https://github.com/github/gitignore/blob/master/Node.gitignore

