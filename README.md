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

## How do you configure Mongoose ?

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
    const express = require('express')                                       // import express.
    const mongoose = require('mongoose');                                    // import mongoose.
```
</dd>

### STEP 3: Configure Mongoose to use ES6 Promises:
------
<dd>

Although this is legacy code and isnt needed with Mongoose 5+, you should insert this statement to make Mongoose use built-in ES6 promises.
```JavaScript
    const express = require('express');
    const mongoose = require('mongoose');

    mongoose.Promise = global.Promise;                                      // Add ES6 Promise support.
```
</dd>

### STEP 4: Import values from config.js file:
------
<dd>

Because the config.js file is where you can control the constants for the entire app. In this way, you can also create development environment variables if
needed. So first, create a config.js file. 
```
    config.js
```
Then inside the config.js file, we have 3 constants: the database url, the test database url, and the port number we want the app to listen for (i.e. 8080). This helps us easily find the variables when needed.
```JavaScript
    exports.DATABASE_URL = process.env.DATABASE_URL || "mongodb://localhost/restaurants-app";
    exports.TEST_DATABASE_URL = process.env.TEST_DATABASE_URL || "mongodb://localhost/test-restaurants-app";
    exports.PORT = process.env.PORT || 8080;
```
```
    How do you set environment variables?

    Now if you want to set an environment variable, you can do so in TWO ways: Temporarily before you run the program OR set for the complete session.

    In the case of setting your environment variable temporarily:

        PORT=3000 node server.js

    In the case an environment variable for the complete session:

        export PORT=3000
        node server.js

```

Finally, we import the values from the config.js file to the server.js file.  We simply import from the config file and pull the variables we want (i.e. PORT and DATABASE_URL).
```Javascript
    const express = require('express');
    const mongoose = require('mongoose');

    mongoose.Promise = global.Promise;

    const { PORT, DATABASE_URL } = require("./config");      // import PORT and DATABASE_URL from config.js.
```

</dd>

### STEP 5: 
------
</dd>




```JavaScript

```
</dd>






</dl>








### STEP : :
------
</dd>


```JavaScript

```
</dd>


</dl>


<br>

## How

