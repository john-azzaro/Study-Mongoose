# Mongoose Study

<br>

Here's some questions covered in the study:

* [What is Mongoose](#)
* [How do you setup and configure a Mongoose server?](#How-do-you-setup-and-configure-a-Mongoose-server)
* [What is a Schema?](#What-is-a-Schema)

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
    exports.DATABASE_URL = process.env.DATABASE_URL || "mongodb://localhost/books";
    exports.TEST_DATABASE_URL = process.env.TEST_DATABASE_URL || "mongodb://localhost/test-books";
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
3. If successful, call a callback function if that connection worked. If unsuccessful, return error.

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

<br>

## What is a Mongoose Schema?

<dl>
<dd>

A **schema** is used to define the shape (i.e. layers of properties) of documents within a collection in MongoDB. 

In other words, a schema is a template that you can plug data into and save in a collection inside your database. For instance, in MongoDB Compass 
for each database you will see "collections". A "document" in a MongoDB "collection" is an individual instance of each 
schema with unique values in the standard properties.

To create a schema, you first need to create a "blueprint" of your document. This define the shape of the document you wish to create.  

> In the following example, we'll create schema for a book with associated properties (i.e. name, author, etc.).

</dd>
</dl>

### First, we set the "bookSchema" to a new schema class:

<dl>
<dd>

This basically creates a new schema when the "bookSchema" is called. And because this creates a new instance of the class, you pass an object with the key/value pairs
in the books documents. So again, this book "schema" will define the shape (i.e. layout) of the book documents (i.e. individual instances) in the Mongo Database.
```JavaScript
    const bookSchema = new mongoose.Schema({
        // properties of book go here.
    })
```

</dd>
</dl>

### Second, specify the properties your document has:

<dl>
<dd>

When you create your schema, you are going to need to have specific attributes that document has.  Thus, for each an every book schema that is created you need to have properties such as a name, author, isPublished, etc. 

Now take for example the "author" property. This property has a schema type of "String" which maps to an internal validator that will be triggered when the model is saved to MongoDB. If the data type is anything other than a String, it will fail because it is not a string type. 

 ```JavaScript
    const bookSchema = new mongoose.Schema({             // Schema that will represent a book:
        name: {                                          // object with type property and required value.
            type: String, 
            required: true
        },            
        authors: String,                                 // string.
        tags: [ String ],                                // array of string values.                 
        isPublished: Boolean                             // boolean
        date: { type: Date, default: Date.now },         // date (set to the date created).
        reviews: [{                                      // array of objects
            reviewer: String,
            publication: String,
            grade: Number,
            date: Date
        }]
    })
```

Also note that when creating schemas, you can use only the following data types: 

| **Data Type:**                            | **Example:**                             |
| ---------------------------------------- | ----------------------------------------------|
|    *String*                                      |          Joe Smith                                     |
|     *Number*                                     |           12345                                    |
|    *Date*                                      |         2019-06-29T22:34:02.188Z                                      |
|    *Boolean*                                      |       true                                        |
|    *Array*                                       |         [red, yellow, green]                                      |
|    *Object*                                       |         {name: String, age: Number}                                      |


</dd>
</dl>



<br>

## What is a Mongoose Model?

<dl>
<dd>

A **Mongoose model** is a wrapper on the Mongoose schema.

While the *schema* defines the structure of the document, like the default values, validators, etc., the Mongoose *model* provides the interface to the database for creating, querying, updating, deleting, etc.

</dd>
</dl>

<br>

## How do you create a Mongoose Model?
To create a model, we need to follow a three step process: 
1. Reference Mongoose
2. Define the Schema
3. Export the model

### STEP 0: Create a models file.
<dl>
<dd>

```
    models.js
```

</dd>
</dl>

### STEP 1: Reference Mongoose.
<dl>
<dd>

```JavaScript
    const mongoose = require('mongoose');              //load mongoose
```

</dd>
</dl>

### STEP 2: Define the Schema.
<dl>
<dd>

As we covered in the previous "What is a Mongoose Schema" section, you are simply creating a template for any instance of books you will create. 
```JavaScript
    const mongoose = require("mongoose");

    const bookSchema = new mongoose.Schema({          // schema of book
        name: {                      
            type: String, 
            required: true
        },            
        authors: String,         
        tags: [ String ],                   
        isPublished: Boolean,      
        date: { type: Date, default: Date.now },  
        reviews: [{               
            reviewer: String,
            publication: String,
            grade: Number,
            date: Date
        }]
    })
```

</dd>
</dl>

### STEP 3: Export the model.
<dl>
<dd>

Now that you have your schema, you need to package it a model to be exported elsewhere in your code. To do this, you need to do the following:

1. Tell mongoose top create a new model:
    ```JavaScript
        mongoose.model();
    ```
2. Pass in TWO arguments: The corresponding collection in your database and the schema:
When you tell mongoose to create a model, the first argument you pass in will be the collection in the database that corresponds to this model. The second argument will be the schema we just defined. Also note that by default, Mongo will convert convert the name of the first argument (i.e. Book => books), where it will be working with ``` db.books```.

    ```JavaScript
        mongoose.model('Book', bookSchema);    
    ```
3. Store as a constant:

    ```JavaScript
        const Book = mongoose.model('Book', bookSchema);
    ```
4. Export the model:
Then just export the model you just created

     ```JavaScript
       const Book = mongoose.model('Book', bookSchema);
       module.exports = { Book }
     ```   

And as a finished model, see how everything fits together:
        
```JavaScript
        const mongoose = require("mongoose");

        const bookSchema = new mongoose.Schema({  
            name: {                      
                type: String, 
                required: true
            },            
            authorName: {
                firstName: String,
                lastName: String,
            }        
            tags: [ String ],                   
            isPublished: Boolean,      
            date: { type: Date, default: Date.now },  
            reviews: [{               
                reviewer: String,
                publication: String,
                grade: Number,
                date: Date
            }]
        });

        const Book = mongoose.model("Book", bookSchema);     // Create a new mongoose model of book...

        module.exports = { Book };                           // and export Book (for use in server.js).
```

</dd>
</dl>

<br>

## What are Virtuals?
<dl>
<dd>

A **virtual** allows you to manipulate properties in the schema object (which are stored in the database). In other words, it will let you take existing properties in your database to create a new property.

For example, look at the ```authorName``` property in our bookSchema, which is an object with two properties: ```firstName``` and ```lastName```.
```JavaScript
    const bookSchema = new mongoose.Schema({
        authorName: {                                        // author object with...
            firstName: String,                               // ... first name and...
            lastName: String,                                // ... last name properties.
        }
        ...
        ...
    });
```
Now suppose you want to reference the full name of the author of your books. How would you do this?

You *could* just have a property like ```fullName``` with a combination of the first and last names, most of the time your database will not have this spcific combination. This is where *virtuals* come in. Conversely, you *could* concatenate the properties of the first and last name throughout the entire application. However, this is messy and with the power of virtuals, you only need to do this *once*!

What a virtual will do is create a new property (that does not exist nor persist in the database) and *manipulate* those properties so that a new property is created for use in your application. In the following question, you'll see just how easy creating a new virtual property can be.

</dd>
</dl>

<br>

## How do you define a virtual property?
<dl>
<dd>

### STEP 1: 


To create a virtual property, you need simply need to call the Schema and chain the ```.virtual``` method

</dd>
</dl>




