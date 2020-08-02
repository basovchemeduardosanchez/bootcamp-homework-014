# bootcamp-homework-014

This is a sample Node.js application that demonstrates the use of Sequelize and 
the Passport (See http://www.passportjs.org/docs/) authentication library using a local strategy (See http://www.passportjs.org/packages/passport-local/)

## Requirements

1. MySQL Server must be installed on the machine

## Running

1. Download the repository to your computer
2. Open the downloaded folder in a file explorer
3. Modify the `config/config.json` file with the details of your database
4. Open the terminal
5. Navigate to the repository root
6. Import the database schema
    ```sh
    mysql -u root -p -vvv < db/schema.sql
    ```
7. Install the dependencies by executing
    ```sh
    npm install
    ```
8. Run the server by executing
    ```sh
    node server.js
    ```
9. Open your browser at http://localhost:8080/
10. Register an account and login with it afterwards

## Application Walkthrough

### About Passport

**Passport** is an **authentication library** for Node.js. It can work with
Express.js to authenticate users in a web application. Passport splits the core
authentication logic from the actual **login method** which they call
**_Strategy_**. A _Strategy_ encompasses the means of authentication, which
could be via Facebook, Twitter, Google, Local (Self-managed users and passwords)
or others

#### Passport Local Strategy

The Passport local _Strategy_ allows developers to fully control the user
registration allowing to save the user and password in a local database.

### File Structure

#### /

The main project folder

##### /.gitignore

Includes file patterns to ignore when commiting files into the repository

##### /activity_instructions.md

The instructions given for this activity

##### /package.json

This file contains project information including the dependencies for the
project, which in this case are:

- `express`: A simple HTTP Server library for Node.js
- `mysql2`: MySQL dependency for `sequelize`
- `sequelize`: An ORM (Object-Relation Map) to handle relational databases
- `passport-local`: The local strategy dependency for the `passport` library
- `passport`: An authentication library for Node.js
- `bcryptjs`: A library to help hash passwords for them to be safe to save into
    a database
- `express-session`: This is a library to manage data in a session, which is
    useful to keep things like a shopping cart or other details

##### /package-lock.json

This file gets created after the execution of `npm install`. It contains the
fixed versions of the dependencies that are downloaded. When this file is
committed to the repository, the next time the application is installed, `npm` will make sure that the exact same versions of the dependencies are installed

##### /README.md

This file

##### /server.js

The main file of the application. This file initializes Express.js with all of
the dependencies needed and imports the routes of the application from other
files in the project

##### /config

This folder contains configuration files for Passport and Sequelize

###### /config/config.json

This JSON file contains the configuration for Sequelize to connect to the MySQL database. 

**IMPORTANT**: The details here should be changed to match those of your local database to start developing the application

###### /config/passport.js

This is the configuration file for Passport. In it, passport is told to use the
"Local" strategy to allow us to manage the users ourselves. This file also
defines how authentication should behave.

In this case, when we receive an authentication call we check if the e-mail we
were passed is already registered in the database by using our `User` Sequelize
model to query for a user registered with that e-mail.

The following describes our authentication flow:

- If a user with the provided email is not found in the database, then we call
    the Passport's `done` function (Which in the documentation is called _verify
    callback_) and set the second parameter to `false`, which means
    authentication failed
- If the user was found in our database we attempt to check if the password is
    correct by using our `User` model `validPassword` which in turn will call
    the `bcrypt`'s `compareSync` function which compares the passport passed to
    the function with the encrypted version saved in the database.
    - If the password doesn't match we call the Passport's `done` function with
        its second parameter set to `false`, which means authentication failed
    - If the password matches then Passport's `done` function is called with the
        second parameter set to the record in the database corresponding to the
        email that was passed, which means authentication succeeded

###### /config/middleware

Stores files that will be used as Express.js middleware functions. According to
the Express.js documentation at https://expressjs.com/en/guide/using-middleware.html

> Middleware functions are functions that have access to the request object
> (`req`), the response object (`res`), and the next middleware function in the
> application’s request-response cycle. The next middleware function is commonly
> denoted by a variable named `next`.
>
> Middleware functions can perform the following tasks:
>
> - Execute any code.
> - Make changes to the request and the response objects.
> - End the request-response cycle.
> - Call the next middleware function in the stack.

This means that a middleware function is a function that can make further
processing of the request and response objects. Popular middlewares in Express
are:

- The `json` middleware, which processes JSON objects sent in the request body
    to a route
- The `urlencoded` middleware which can process form data sent by an HTML form

The middleware functions stores in this directory are custom.

###### /config/middleware/isAuthenticated.js


