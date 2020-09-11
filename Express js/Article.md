## Why you should use Express.js in your Node.js Application

If you're wondering what the fuss is about Express.js and why most popular javascript stacks are MERN, MEAN, MEVN etc., using Express.js as part of their stack instead of alternate web frameworks, you are in the right place!

I will start this tutorial by:
#### 1. Giving a brief introduction about Node js
#### 2. Briefly introducing Express js
#### 3. Discussing Reasons why Express js is the right middleware for your Node js app
**4. Discussing changes in Express 4, and why Express 4 is super cool**

### 1: Brief Introduction about Node js
Node.js is an open-source, cross-platform runtime environment that allows developers to create all kinds of server-side tools and applications in JavaScript. Node.js has NPM (Node Package Manager) which provides access to hundreds of thousands of reusable packages, it also has best-in-class dependency resolution and can also be used to automate most of the build toolchain.

To understand how a server-side application can be created with Node js, We will create a simple "hello world" application with Node.js. 

- if you don't already have Node.js installed on your system, download [nodejs](https://nodejs.org/en/download) for your operating system.
- Read [node_setup](https://nodejs.org/en/download) to install and set up your node js environment,
- if you're not sure if Node js is already installed on your system, open your command prompt or other terminal and type the following:

```
node --version
v5.0.0
npm --version
3.5.2

```
> You should get the version of node and npm installed on your system, else Node .js has not been installed.

- After setting up your Node js environment, create a new folder for our "hello world" application and navigate to the folder by running this code on your terminal.

```
cd hello_world
```

create a new project in the folder with Npm by executing this code in your terminal

```
npm init
```
Npm would ask the following questions as shown below, to create a package.json file

```
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Press ^C at any time to quit.
name: (myproject)
version: (1.0.0)
description: A sample Node js project
entry point: (app.js)
test command:
git repository: hello_world/myproject
keywords:
author: JaneDoe
license: (ISC)
About to write to /Users/JaneDoe/hello_world/myproject/package.json:

{
  "name": "myproject",
  "version": "1.0.0",
  "description": "A sample Node js project",
  "main": "app.js",
  "dependencies": {},
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/JaneDoe/myproject.git"
  },
  "author": "JaneDoe",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/JaneDoe/hello_world/myproject/issues"
  },
  "homepage": "https://github.com/JaneDoe/hello_world/myproject#readme"
}


Is this ok? (yes)
```

The name of my file is app.js, in hello_world/myproject replace with the name of the file you created.
> With any text editor of your choice, open the file you created (app.js) and input the following codes:

```
// Import HTTP module for your app
const http = require("http");

// Create HTTP server 
const server = http.createServer((req, res) => {

   // Set the response HTTP header with HTTP status and Content type
   res.writeHead(200, {'Content-Type': 'text/plain'});
   
   // Send the response body "Hello World"
   res.send('Hello World');
});

// Prints a log once the server starts listening
server.listen(3000 () => {
   console.log(`Server running at http://localhost:3000`);
})
```
To start your server, run the following code on your terminal
```
node app.js
```
Navigate to http://localhost:3000 in your web browser; you should see the text "Hello World" in the web page.

![hello world page.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1599740228396/DUbnzTkHg.png)

### 2. Briefly introducing Express js
You are probably wondering why you need Express.js since you can create a simple server-side web application with Node js;

Imagine you want to structure a web application to handle multiple different HTTP requests at a specific URL, for instance an ideal web application may have a blog page (specific URL) and users should be able to delete their blog post, edit their blog post, read more about a single web page and so on (handle multiple different HTTP requests).

This is where Express js comes in, Express helps you respond to requests with route support so that you may write responses to specific URLs and handle multiple different HTTP requests at specific URLs.

To understand this better, we will create a simple "hello world" application to display hello world message and the route name as we navigate.

- Create a folder for our Express App
```
cd hello_world_Express
```
- Create a new file in the folder with the same steps like when we created our first Node .js app.

- To add Express Js to your application write in your terminal ```npm i express``` or ```npm install express``` for full to install Express via Npm.
```
npm i express
```


> With any text editor of your choice, open the file you created (app.js) and input the following codes:

```
const express = require('express');
var app = express();
app.get('/', (req, res) => {
    res.send('Hello Express this is home page')
});
app.get('/blog', (req, res) => {
    res.send('Hello Express this is blog page')
});
app.get('/about', (req, res) => {
    res.send('Hello Express this is about page')
});
app.listen(3000)
```
run your server by inputing the following code on your terminal
```
node app.js
```
Navigate to http://localhost:3000 in your web browser; you should see the text "Hello Express this is home page" in the web page. 

![home page.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1599740242581/XOflZ-i7P.png)

Navigate to http://localhost:3000/blog in your web browser; you should see the text "Hello Express this is blog page" in the web page.

![blog page.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1599740254318/OnSFpJqNG.png)

Navigate to http://localhost:3000/about in your web browser; you should see the text "Hello Express this is about page" in the web page.

![about page.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1599740276083/p_CPY-1Kb.png)

>With Express js, we have successfully created three routes for port 3000 and have created delete method and get method for ```('/')``` route (handle multiple different http requests at a specific URL)

### 3. Discussing Reasons why Express js is the right web framework for your Node js app
**1. Express js Writes handlers for requests with different HTTP verbs at different URL paths (routes).
**

An example is this expression for Express 4
```
app.route('/name')
  .get(function (req, res) {
    res.send('Bring a list of visitors names')
  })
  .post(function (req, res) {
    res.send('Add a new visitor')
  })
  .put(function (req, res) {
    res.send('Update visitor list')
  })
```
Or this expression for express 3

```
  app.get ('/name')
  (function (req, res) {
    res.send('Bring a list of visitors names')
  })
  app.post(function (req, res) {
    res.send('Add a new visitor')
  })
  app.put(function (req, res) {
    res.send('Update visitor list')
  })
```

**2. Express js sets common web application settings like the port to use for connecting, and the location of templates that are used for rendering the response, and also adds additional request processing "middleware" at any point within the request handling pipeline.**

**3. Express js supports MVC (Model-View-Controller), a very common architecture to design web applications.**

MVC is an architectural pattern that separates an application into three main logical components: the model, the view, and the controller. Each of these components are built to handle specific development aspects of an application. MVC is one of the most frequently used industry-standard web development framework to create scalable and extensible projects.

The Model component corresponds to all the data-related logic that the user works with. This can represent either the data that is being transferred between the View and Controller components or any other business logic-related data. For example, a Customer object will retrieve the customer information from the database, manipulate it and update it data back to the database or use it to render data.

The View component is used for all the UI logic of the application. For example, the Customer view will include all the UI components such as text boxes, dropdowns, etc. that the final user interacts with.

Controllers act as an interface between Model and View components to process all the business logic and incoming requests, manipulate data using the Model component and interact with the Views to render the final output. For example, the Customer controller will handle all the interactions and inputs from the Customer View and update the database using the Customer Model. The same controller will be used to view the Customer data.

**4. Express js leverages upon Node.js single threaded and asynchronous model.**

A thread is the smallest sequence of programmed instructions that can be managed independently by a scheduler, which is typically a part of the operating system. A Node.js application runs on single thread and the event loop also runs on the same thread. Hence, we can say Node.js is single-threaded.

**5. Express js is cross-platform and is not limited to any particular operating system**

**6. Express js comes with a default template engine, Jade which helps to facilitate the flow of data into a website structure and also integrate with other "view" rendering engines in order to generate responses by inserting data into templates.**

A template engine enables you to use static template files in your application. At runtime, the template engine replaces variables in a template file with actual values, and transforms the template into an HTML file sent to the client. This approach makes it easier to design an HTML page.

Some popular template engines that work with Express are Pug, Mustache, and EJS. The Express application generator uses Jade as its default, but it also supports several others.

### 4. Discussing changes in Express 4, and why Express 4 is super cool

> Express 4 is a breaking change from Express 3. That means an existing Express 3 app may not work if you update the Express version in its dependencies.

The two major change in Express 4 are :-

- Express Core and middleware Changes
- Routing system Changes

#### 1.  Express Core and middleware Changes
Express 4 no longer depends on Connect, and removes all built-in middleware from its core, except for the express.static function. This means that Express is now an independent routing and middleware web framework, and Express versioning and releases are not affected by middleware updates.

Without built-in middleware, you must explicitly add all the middleware that is required to run your app. Simply follow these steps:

Install the module: npm install --save <module-name>
In your app, require the module: require('module-name')
Use the module according to its documentation: app.use( ... )
Express 3 middleware and their counter-parts in Express 4 becomes:

```
/**for Express 4**/ 
const bodyParser = require('body-parser'); 
// instead of this for Express 3
express.bodyParser 

/**for Express 4**/ 
const compression = require('compression');
// instead of this for Express 3
express.compression

/**for Express 4**/ 
const cookieSession = require('cookie-session');
// instead of this for Express 3
express.cookieSession

/**for Express 4**/ 
const cookieParser = require('cookie-parser');
// instead of this for Express 3
express.cookieParser

/**for Express 4**/ 
const logger = require('morgan');
// instead of this for Express 3
express.logger

/**for Express 4**/ 
const session = require('express-session');
// instead of this for Express 3
express.session

/**for Express 4**/ 
const favicon = require('serve-favicon');
// instead of this for Express 3
express.favicon

/**for Express 4**/ 
const responseTime = require('response-time');
// instead of this for Express 3
express.responseTime

/**for Express 4**/ 
const errorHandler = require('error-handler');
// instead of this for Express 3
express.errorHandler

/**for Express 4**/ 
const methodOverride = require('method-override');
// instead of this for Express 3
express.methodOverride

/**for Express 4**/ 
const timeout = require('connect-timeout');
// instead of this for Express 3
express.timeout
```
Here is the complete list of [Express4](https://expressjs.com/en/resources/middleware.html) middlewares.

#### 2. Routing system Changes
Apps now implicitly load routing middleware, so you no longer have to worry about the order in which middleware is loaded with respect to the router middleware.
The way you define routes is unchanged, but the routing system has two new features to help organize your routes:

-  A new method, app.route(), to create chainable route handlers for a route path.
- A new class, express.Router, to create modular mountable route handlers.

**2(a). app.route() method**

The new app.route() method enables you to create chainable route handlers for a route path. Because the path is specified in a single location, creating modular routes is helpful, as is reducing redundancy and typos.

Here is an example of chained route handlers that are defined by using the app.route() function.

```
app.route('/name')
  .get(function (req, res) {
    res.send('Bring a list of visitors names')
  })
  .post(function (req, res) {
    res.send('Add a new visitor')
  })
  .put(function (req, res) {
    res.send('Update visitor list')
  })
```

Instead of this in Express 3

```
  app.get ('/name')
  (function (req, res) {
    res.send('Bring a list of visitors names')
  })
  app.post(function (req, res) {
    res.send('Add a new visitor')
  })
  app.put(function (req, res) {
    res.send('Update visitor list')
  })
```
**2(b). express.Router class**

The other feature that helps to organize routes is a new class, express.Router, that you can use to create modular mountable route handlers. A Router instance is a complete middleware and routing system; for this reason it is often referred to as a “mini-app”.

The following example creates a router as a module, loads middleware in it, defines some routes, and mounts it on a path on the main app.

For example, create a router file named birds.js in the app directory, with the following content:

```
var express = require('express')
var router = express.Router()

// middleware specific to this router
router.use(function timeLog (req, res, next) {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page')
})
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds')
})

module.exports = router
```
Then, load the router module in the app:
```
var birds = require('./birds')

// ...

app.use('/birds', birds)
```

### Conclusion 

In this article, we have talked briefly about Node Js. Detailed explanation of what Express Js is and why you need it in your Node Js application was discussed with some code examples. Also, changes made in Express 4 when compared to Express 3 was discussed and why Express 4 is super cool.

Thank you so much for reading this article till the end! you can contact me on [twitter](http://www.twitter.com/hannydevelop) or send a [mail](mailto:ukpaiugochi0@gmail.com) if you have any questions or suggestions regarding this article. 
