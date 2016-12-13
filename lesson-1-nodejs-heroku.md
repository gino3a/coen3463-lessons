### Prerequisites
* Node.js and npm installed.
* Github Account + Git installed
* a free Heroku account.
* the Heroku CLI.

### Create New Github Project
Take note of SSH URL of the github project git@github.com:<username>/<project-name>.git
eg: git@github.com:juandelacruz/myapp.git

### Create New Heroku Project
* Go to https://dashboard.heroku.com/new?org=personal-apps
* Set an app name or let Heroku chose one for you
* Leave Runtime Selection set to United states
* Click Create App button
* Go to the Settings page of the created app and take note of this app's Git URL found in the Info Section
eg: https://git.heroku.com/myapp-1234.git


### Create Node Project in your Local Environment

* To create a new empty repository, run on a terminal:

    $ mkdir myapp
    $ cd myapp
    $ git init

* Set Github URL
    $ git remote add origin git@github.com:juandelacruz/myapp.git

* Set Heroku Git URL
    $ git remote add origin https://git.heroku.com/myapp-1234.git


* Setup Node package
In a terminal in the `myapp` folder, run:


    $ npm init


It will ask you for multiple questions, you can leave most of the defaults except for `entry point`, key in app.js.
name: (myapp)
version: (1.0.0)
description:
entry point: (index.js) app.js
test command:
git repository:
keywords:
author:
license: (ISC)

This file will be generated for you containing the list of your dependencies (the librairies our program will depend on) and some others descriptives informations.

* Install Express in your project folder
Still in the `myapp` folder, run:

     $ npm install --save express

* Add start command in package.json

    "scripts" : {
        "start": "node app.js"
    }

Your package.json should look something like this now

    {
      "name": "myapp",
      "version": "1.0.0",
      "description": "",
      "main": "app.js",
      "scripts": {
        "start": "app.js"
      },
      "author": "",
      "license": "ISC",
      "dependencies": {
        "express": "^4.14.0"
      }
    }
~

* Write in a file named **app.js**:


    var express = require("express");
    var app = express();

    app.get('/', function(req, res) {
      res.send('Hello World!');
    });

    var port = Number(process.env.PORT || 5000);
    app.listen(port, function() {
      console.log("Listening on " + port);
    });

* Write in a file named *.gitignore**:


    /node_modules
    npm-debug.log
    .DS_Store
    /*.env


### Deployment

* While in your app's folder, login to heroku


    $ heroku login

* Commit your changes


    $ git add .
    $ git commit -am "initial commit"

* Push to Github

    $ git push origin master

* Push to Heroku

    $ git push heroku master

### All done, you can now double check if your app's is runing in heroku
https://myapp-1234.herokuapp.com

