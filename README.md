# Mongoose Study

<br>

Here's some questions covered in the study:

* [What is Mongoose](#)
* [How do you connect with MongoDB using Mongoose?](#How-do-you-connect-with-MongoDB-using-Mongoose)

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

Install mongoose from node package manager.
```
    npm install mongoose
```
</dd>

### STEP 2: Import mongoose into your server.js file:
------
<dd>

This is pretty much a standard importation of the mongoose package you previously installed to your dependencies.
```JavaScript
    const mongoose = require('mongoose');                                               // require mongoose.
```
</dd>

### STEP 3: Add ES6 Promise support:
------
<dd>

Although this is legacy code and isnt needed with Mongoose 5+, you should insert this statement to make Mongoose use built-in ES6 promises.
```JavaScript
    mongoose.Promise = global.Promise;
```
</dd>

### STEP : :
------
</dd>


```JavaScript

```
</dd>




</dl>


<br>

## How

