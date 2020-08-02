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

This JSON file contains the configuration