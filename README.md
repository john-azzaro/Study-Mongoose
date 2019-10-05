# Mongoose Study

<br>

Here's some questions covered in the study:

* [What is Mongoose](#)

<br>

## What is Mongoose?
Mongoose is a Object Data Mapper (ODM) library (or Object Modeling Modeler) for MongoDB and Node.js, and allows your Node.js app to (which speaks the JavaScript language) to talk to the MongoDB database.  The primary objective of the Mongoose framework is to simply the writing of validation code, business logic boiler plate, and make the code shorter and easier to work with. 

In more technical terms, Mongoose provides a modeling enviroment for your data, enforcing structure while maintaing flexibility. Mongoose manages realtionships between data, providing schema validation, and is used between objects in code and the representation of those object in MongoDB.


<br>

## How do you connect with MongoDB using Mongoose?

<dl>

### STEP 1: Install the Node package "mongoose":
-----
<dd>

```
    npm install mongoose
```
</dd>

### STEP 2: Require the mongoose package in your server.js file:
------
This is pretty much a standard require of the mongoose package you previusoly installed to your dependencies.
<dd>

```JavaScript
    const mongoose = require('mongoose');                   // require mongoose.
```
</dd>

### STEP 3: Connect to your database
-----
When you connect to a database, you call mongoose with the .connect method (i.e. ``` mongoose.connect()```). Then, you want to pass a connection string that references the mongoDB database.  In the example below, you have the localhost to conenct to your local machine for.  However, note that when the application is deployed to a production enviroment, you will be using a different connection string.

```JavaScript
    mongoose.connect('mongodb://localhost/sandbox')      // connect to local mongodb database.
```

In addition to this connection, we need a way to check whether or not we are connected to our database.  To do this, you need to chain a ```.then()```, which will be a promise that, when fulfilled, will log "connected to MongoDB...".  And if there is an error connecting to the database, use a ``` .catch()``` to log an error message and the error.

```JavaScript
    mongoose.connect('mongodb://localhost/playground')
        .then( () => console.log('Connected to MongoDB...'))
        .catch( (err) => console.log('Could not connect to MongoDB...', err));
```


</dl>


<br>

