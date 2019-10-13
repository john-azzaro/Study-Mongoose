# Mongoose Study

<br>

Here's some questions covered in the study:

* [What is Mongoose](#)
* [How do you setup and configure a Mongoose server?](#How-do-you-setup-and-configure-a-Mongoose-server)

<br>

## What is Mongoose?
Mongoose is a Object Data Mapper (ODM) library (or Object Modeling Modeler) for MongoDB and Node.js.

Mongoose allows your Node.js app to talk to the MongoDB database.  The primary objective of the Mongoose framework is to simply the writing of validation code, business logic boiler plate, and make the code shorter and easier to work with. 

In more technical terms, Mongoose provides a modeling enviroment for your data, enforcing structure while maintaing flexibility. Mongoose manages realtionships between data, providing schema validation, and is used between objects in code and the representation of those object in MongoDB.


<br>

## How do you setup and configure a Mongoose server?
To setup Mongoose, you need to install the Mongoose depency, configure Mongoose to use ES6 promises (for pre-version 5 Mongoose). Then, you can add your database url's and environment variables either in the server.js file or (as in this study), in a seperate config.js file.  Lastly, add a runServer and a closeServer function to connect with MongoDB and listen for connections and close the server when disconnected.

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
    const express = require('express')                                               // import express.
    const mongoose = require('mongoose');                                            // import mongoose.
```
</dd>

### STEP 3: Configure Mongoose to use ES6 Promises:
------
<dd>

Although this is legacy code and isnt needed with Mongoose 5+, you should insert this statement to make Mongoose use built-in ES6 promises.
```JavaScript
    const express = require('express');
    const mongoose = require('mongoose');

    mongoose.Promise = global.Promise;                                         // Add ES6 Promise support.
```
</dd>

### STEP 4: Import values from config.js file:
------
<dd>

1. Because the config.js file is where you can control the constants for the entire app. In this way, you can also create development environment variables if
needed. So first, create a config.js file. 
```
    config.js
```

<br>

2. Then inside the config.js file, we have 3 constants: the database url, the test database url, and the port number we want the app to listen for (i.e. 8080). This helps us easily find the variables when needed.

> NOTE: If you want to set an environment variable, you can do so in TWO ways: Temporarily before you run the program OR set for the complete session. In the case of setting your environment variable temporarily: ```PORT=3000 node server.js```. In the case an environment variable for the complete session: ```export PORT=3000 node server.js```.
```JavaScript
    exports.DATABASE_URL = process.env.DATABASE_URL || "mongodb://localhost/restaurants-app";
    exports.TEST_DATABASE_URL = process.env.TEST_DATABASE_URL || "mongodb://localhost/test-restaurants-app";
    exports.PORT = process.env.PORT || 8080;
```

<br>

3. Finally, we import the values from the config.js file to the server.js file.  We simply import from the config file and pull the variables we want (i.e. PORT and DATABASE_URL).
```Javascript
    const express = require('express');
    const mongoose = require('mongoose');

    mongoose.Promise = global.Promise;

    const { PORT, DATABASE_URL } = require("./config");       // import PORT and DATABASE_URL from config.js.
```

</dd>

### STEP 5: Create a "runServer" function to connect to database and run HTTP server!
------
</dd>

So essentially the runServer function will connect to the MongoDB database and run the HTTP server in unison.  It does this in a specific order:
1. Mongoose connects to our database using the URL's we provided in the config.js file.
2. Listen for connections on the ports we specified (i.e. 8080 OR other specified env variable port).
3. If successful, call a callback function that connection worked. If unsuccessful, return error.

```JavaScript
    let server;                                                    // server declared OUTSIDE Run and Close.
 
    function runServer(databaseUrl, port=PORT) {                   // To Run server: 
        return new Promise((resolve, reject) => {                  // return Promise in which...
            mongoose.connect(databaseUrl, err => {                 // Mongoose connects to database:
                if (err) {                                         // If there is an error... 
                    return reject(err);                            // ... return reject.
                }       

                server = app.listen(port, () => {                  // Listen for connection to configured port.  
                    console.log(`Listening on port ${port}`);      // ... and log connection in terminal.
                    resolve();                                     // and then the promise is resolved!
                })
                .on('error', err => {                              // But if there is an error...
                    mongoose.disconnect();                         // ... disconnect from mongoose...
                    reject(err);                                   // and reject (passing in an error object).
                });
            });
        });
    }
```

</dd>

### STEP 6: Create a "closeServer" to disconnect from database and close app:
------
</dd>

This closes the app as well as disconnects from the database. This also returns a promise, which is doen for testing, and accesses the server object which was created in runServer.

```JavaScript
    function closeServer() {                                     // To close server:
        return mongoose.disconnect().then(() => {                // disconnect and then...
            return new Promise((resolve, reject) => {            // return a promise which...
                console.log("Closing server");                   // ... will log "closing server"...
                server.close(err => {                            // and close the server...
            if (err) {                                           // and if there is an error, reject...
               return reject(err);                                  
            }
            resolve();                                           // else resolve.
        });
        });
    });
    }
```
</dd>

</dl>

## What is a Schema?
A schema is used to define the shape (i.e. layers of properties) of documents within a collection in MongoDB. In other words, a schema is 
a template that you can plug data into and save in a collection inside your database.  

In MongoDB Compass for each database you will see "collections". A "document" in a MongoDB "collection" is an individual instance of each 
schema with unique values in the standard properties. Think of schemas like the difference between Classes and objects. A Class would be a human.
An object would be a person named "Joe".








<br>

## How do you create Mongoose models?
First, what is a 


<dl>







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

