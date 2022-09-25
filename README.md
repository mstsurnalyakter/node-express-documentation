# My Node.js & Express.js Documentation

## Total Chapters are following

1. Node.js
   1. Introduction to the playlist
   2. Introduction to node.js
   3. Local Module
   4. Built-in module - fs module
   5. Built-in module - os and path module
   6. Built-in module - http module
   7. request, response, status code
   8. npm crash course
   9. http routing
   10. create node server and deploy on heroku
2. Express.js
   1. introduction to express.js
   2. express server
   3. http methods and postman
   4. Express Router
   5. HTTP Response
   6. HTTP Request part-1
   7. HTTP Request part-2
   8. HTTP Request part-3
   9. send and receive from data
   10. Area Calculator
   11. How to set .env variables
   12. Middlewares
   13. express static Middlewares
   14. MVC pattern

## Chapter 1: Node.js

### [1.1 Introduction to Node.js & setup](https://youtu.be/36R0VXmX8i8)

#### What is Node.js & Why Node.js?

- fullstack = front-end + back-end
- window is a global object for browser. before node.js we could use javascript for the browser only but now with the help of node.js we can run javascript for accessing our local machine. try console.log(), window.alert() at the browser and in the terminal.
- Node.js is server side environment; not a programming language.
- It utilize Google's V8 engine (developed with C++) which compiles javascript code into machine code
- a js runtime which allows us to run js in the server
- node.js does not run on browser but only vanila js
- helps us to create real time applications
- It helps to manage files (create, open, read, write, delete and close) on the server.
- it supports asynchronous programming.
- it helps to collect form data.
- It helps to manage (add, modify, delete data) database.

#### Environment setup

- check node is already installed or not using the command: node --version or node -v
- [Node.js](https://nodejs.org/en/) download & install
- Editor: anything; I prefer [Visual Studio Code](https://code.visualstudio.com/)
- type node and enter for using Node REPL and try writing some javascript code here like console.log(), mathematical calculations
- window is a global object in the fornt end; global is the global object in the backend

### [1.3 Local module](https://youtu.be/n3F1kaOfyzw)

#### What is module? Types of module?

- we can use es6 import, export by adding "type":"module" in package.json
- when you have too much code in a single file you would like to separate them in multiple files so that they are reusable and modular.
- Module is a set of functions or variables.
- console.log(process) and find the module.exports = {}
- 3 types of module.
  - local module (own created module)
  - built-in-modules (node.js own module)
  - External modules (3rd party module mainly managed by npm)
- example 1

  ```js
  // message.js
  const SUBJECT = "Node.js";

  const displayInfo = (name) => {
    console.log(`Welcome ${name}`);
  };

  module.exports = { SUBJECT, displayInfo };

  // index.js
  const message = require("./message");
  console.log(message.SUBJECT);
  message.displayInfo("Anisul Islam");
  ```

- example 2

  ```js
  // message.js

  const SUBJECT = "Node.js";
  // exports.SUBJECT = "Node.js";

  const displayInfo = (name) => {
    console.log(`Welcome ${name}`);
  };

  exports.SUBJECT = SUBJECT;
  exports.displayInfo = displayInfo;

  // index.js

  // following line will get everything from message module
  const message = require("./message");

  // following line will get separate items from message module
  const { SUBJECT, displayInfo } = require("./message");
  console.log(SUBJECT);
  displayInfo("anisul");

  // another example
  exports.add = (num1, num2) => {
    return num1 + num2;
  };
  exports.sub = (num1, num2) => {
    return num1 - num2;
  };
  exports.mul = (num1, num2) => {
    return num1 * num2;
  };
  ```

### [1.4 Built-in module - fs module](https://youtu.be/808jcN3c8MM)

- some of the common built-in module - http, url, fs, path
- example of fs module

  ```js
  const fs = require("fs");
  console.log(fs);

  // creating a file
  fs.writeFile("test.txt", "this is some demo text", (err) => {
    // if there is 1 if else then use ternary operator
    if (err) {
      console.log(err);
    } else {
      console.log("File is created successfully");
    }
  });

  // appending data to a file
  fs.appendFile("test.txt", "some extra text is added", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("data is added successfully");
    }
  });

  // reading data from a file
  fs.readFile("test.txt", "utf-8", (err, data) => {
    if (err) {
      console.log(err);
    } else {
      console.log(data);
    }
  });

  // renaming an existing file
  fs.rename("test.txt", "test2.txt", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("successfully renamed");
    }
  });

  // checking a file exsits or not
  fs.exists("test2.txt", (result) => {
    if (result) {
      console.log("file exists");
    } else {
      console.log("file does not exist");
    }
  });

  // deleting a file
  fs.unlink("test2.txt", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("file is deleted successfully");
    }
  });
  ```

### [1.5 Built-in module - os and path module](https://youtu.be/EHo7KNPawhw)

- Example of os and path module

  ```js
  // os, path
  const { totalmem, freemem } = require("os");
  console.log(os.userInfo());
  console.log(os.homedir());
  console.log(os.hostname());
  console.log(totalmem());
  console.log(freemem());

  console.log(__dirname);
  console.log(__filename);

  const path = require("path");

  const extensionName = path.extname("index.html");
  console.log(extensionName);

  const joinName = path.join(__dirname + "/../views");
  console.log(joinName);
  ```

### [1.6 Built-in module - http module](https://youtu.be/PmLJO403hvc)

- Example of a node.js http server

  ```js
  // Method 1
  const http = require("http");

  const PORT = 3000;
  const hostName = "127.0.0.1";

  const server = http.createServer((req, res) => {
    // res.end("welcome to the server");
    res.end("<h1>welcome to the server</h1>");
  });

  server.listen(PORT, () => {
    console.log(`server is running at http://${hostName}:${PORT}`);
  });

  // Method 2
  const http = require("http");
  http
    .createServer((req, res) => {
      res.end("<h1> Welcome to your first node server</h1>");
    })
    .listen(3000, () => {
      console.log("server is running");
    });
  ```

### [1.7 request, response and status code](https://youtu.be/lHfnjUP-N4E)

- [status code cheatsheet](https://devhints.io/http-status)
- Example

  ```js
  // index.js file
  const http = require("http");

  const PORT = 3000;

  const server = http.createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.write("welcome to the server");

    // if we want to return html as status
    // res.writeHead(200, { "Content-Type": "text/html" });
    // res.write("<h1>welcome to the server</h1>");

    res.end();
  });

  server.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### [1.8 External modules | npm crash course](https://youtu.be/A8W1p8suw5I)

- first initialize npm with the command `npm init` then follow the instructions
- we can also use `npm init -y` command for ignoring the installation instructions
- npm packages : https://www.npmjs.com/
- Install https://www.npmjs.com/package/random-fruits-name package
  and follow the instructions

### [1.9 http routing](https://youtu.be/Vlk4UPzi6tc)

- initialize the npm `npm init -y`
- example is given below:

  ```html
  // index.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>home</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to home page</h1>
      </main>
    </body>
  </html>
  ```

  ```html
  // about.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>about</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to about page</h1>
      </main>
    </body>
  </html>
  ```

  ```html
  // contact.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>contact</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to contact page</h1>
      </main>
    </body>
  </html>
  ```

  ```html
  // error.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>error</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>page not found 404</h1>
      </main>
    </body>
  </html>
  ```

  ```js
  // index.js
  const http = require("http");
  const fs = require("fs");

  const PORT = 3000;

  const server = http.createServer((req, res) => {
    const handleReadFile = (fileName, statusCode) => {
      fs.readFile(fileName, (err, data) => {
        res.writeHead(statusCode, { "Content-Type": "text/html" });
        res.write(data);
        res.end();
      });
    };

    if (req.url === "/") {
      handleReadFile("index.html", 200);
    } else if (req.url === "/about") {
      handleReadFile("about.html", 200);
    } else if (req.url === "/contact") {
      handleReadFile("contact.html", 200);
    } else {
      handleReadFile("error.html", 404);
    }
  });

  server.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

- run the server `node index.js`

### [1.10 create node server and deploy on heroku](https://youtu.be/2IFDMvfJJHc)

- [node-server-demo](https://node-server-2022.herokuapp.com/)

- Create 3 html pages inside views folder: index.html, about.html, contact.html

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>

      <style>
        body {
          background-color: bisque;
        }
      </style>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <h1>This is Home page</h1>
    </body>
  </html>
  ```

- create the server (server) and load the html files based on request url

  ```js
  const http = require("http");
  const fs = require("fs");
  const PORT = 3000;

  const handleReadFile = (fileName, statusCode, req, res) => {
    fs.readFile(fileName, "utf-8", (err, data) => {
      if (err) {
        console.log(err);
      } else {
        res.writeHead(statusCode, { "Contant-Type": "text/plian" });
        res.write(data);
        res.end();
      }
    });
  };
  const server = http.createServer((req, res) => {
    if (req.url === "/") {
      handleReadFile("./views/index.html", 200, req, res);
    } else if (req.url === "/about") {
      handleReadFile("./views/about.html", 200, req, res);
    } else if (req.url === "/contact") {
      handleReadFile("./views/contact.html", 200, req, res);
    } else {
      handleReadFile("./views/error.html", 404, req, res);
    }
  });

  server.listen(PORT, () => {
    console.log(`Server is running at http://localhost:${PORT}`);
  });
  ```

- How to deploy on heroku
  - step1 : const PORT = process.env.PORT || 3000;
  - step2 : add Procfile -> `web: node index.js`
  - step3 : npm init -y && npm install nodemon
  - step4 : follow the steps in heroku

### [1.11 Node js event loop]

- Node.js is single threaded but non-blocking beacuse of event loop.
- it is efficient because of its non blocking feature
- all the events are placed in a stack (first in first out FIFO)
- Node.js keep running like FIFO, one after one event is handles by node process
- if any task required time instead of stop and wait it will be passed to callback function and then move to the next task
- once all the tasks are handled then from the event loop task will be executed
- synchronous vs asynchronous programming
- example

  ```js
  console.log("hello 1");
  console.log("hello 2");
  setTimeout(() => {
    console.log("hello 3");
  }, 1000);
  setTimeout(() => {
    console.log("hello 4");
  }, 1000);
  console.log("hello 5");
  console.log("hello 6");
  ```

## Chapter 2: Express.js

### [2.1 Introduction to express.js](https://youtu.be/1Max9huISzA)

- always check the documentation of [express.js](https://www.npmjs.com/package/express)
- Express.js is a node.js framework which makes life easier
- easy to learn and time saving facilitites available because we have ready made stuff in express.js
- MERN Stack, NERD stack, PERN stack

### [2.2 creating express server](https://youtu.be/t9GVn5j1Hsw)

- first initialize npm : `npm init -y`
- install express: `npm install express`
- example

  ```js
  const express = require("express");

  const PORT = 3000;

  const app = express();

  app.get("/", (req, res) => {
    res.send("<h1> Welcome to express server </h1>");
  });

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### [2.3 http methods and postman](https://youtu.be/AnCkn--EAas)

- HTTP methods - get, post, put, patch, delete ...
- get methods helps to get a resource or data
- post method helps to create new resource
- put method helps to update a resource
- patch method helps to update single item of a resource
- delete method helps to delete a resource
- example

  ```js
  // index.js

  const express = require("express");

  const PORT = 3000;

  const app = express();

  // http://localhost:3000/user

  // this will work for all http methods: get, post so use app.get() or anything specific
  app.use("/user", (req, res) => {
    res.send("<h1> Welcome to get request of express server </h1>");
  });

  app.get("/user", (req, res) => {
    res.send("<h1> Welcome to get request of express server </h1>");
  });

  app.post("/user", (req, res) => {
    res.send("<h1> Welcome to post request of express server </h1>");
  });

  // put is for updating multiple property
  // patch is for updating one property

  app.put("/user", (req, res) => {
    res.send("<h1> Welcome to put request of express server </h1>");
  });

  app.patch("/user", (req, res) => {
    res.send("<h1> Welcome to patch request of express server </h1>");
  });

  app.delete("/user", (req, res) => {
    res.send("<h1> Welcome to delete request of express server </h1>");
  });

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });

  // error handling
  app.use((req, res) => {
    res.send("<h2>Page not found 404</h2>");
  });

  app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send("Something broke!");
  });
  ```

### [2.4 Express Router](https://youtu.be/S7oFcdUiF1k)

- use morgan package for getting more info about routing on console

  ```js
     step1 : npm install morgan
     step2 : const morgan = require("morgan");
     step3 : app.use(morgan("dev"));
  ```

- example

  ```js
  // step1: creates a routes folder
  // setp2: create a file name as user.routes.js
  // step3: write the following code inside user.routes.js
  const express = require("express");

  const router = express.Router();

  // /users
  router.get("/", (req, res) => {
    res.send("I am get method of user route");
  });

  router.post("/", (req, res) => {
    res.send("I am post method of user route");
  });

  router.put("/", (req, res) => {
    res.send("I am put method of user route");
  });

  router.patch("/", (req, res) => {
    res.send("I am patch method of user route");
  });

  router.delete("/", (req, res) => {
    res.send("I am delete method of user route");
  });

  module.exports = router;

  //step4: write following code inside index.js
  const express = require("express");

  const userRoutes = require("./routes/user.routes");

  const PORT = 3000;

  const app = express();

  app.use("/users", userRoutes);

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

- example 2

  ```js
  const express = require("express");
  const router = express.Router();

  // how to get the path
  const path = require("path");

  const getFileLocation = (fileName) => {
    return path.join(__dirname, `../views/${fileName}`);
  };

  router.get("/", (req, res) => {
    res.sendFile(getFileLocation("index.html"));
  });
  router.get("/register", (req, res) => {
    res.sendFile(getFileLocation("register.html"));
  });
  router.get("/login", (req, res) => {
    res.sendFile(getFileLocation("login.html"));
  });
  module.exports = router;
  ```

### [2.5 HTTP Response](https://youtu.be/S7oFcdUiF1k)

- response can be text, html, json
- res.send("some text here");
- res.status(statuscode).json({...});
- res.sendFile(fileName);
- res.cookie(key, value);
- res.clrarCookie(key);
- res.writeHead()
- res.write()
- res.end()
- res.append(key, value); this will set as response header

### [2.6 HTTP Request part-1](https://youtu.be/141Q7XhGGS8)

- request with query parameter - req.query.parameterName
- request with route parameters - req.params.parameterName
- request with headers - req.header(key)
- request with json data / form data inside body - req.body.parameterName
- query parameter has question mark; search something on google.

  - example of query parameter - http://localhost:3000?id=101&name=anisul islam

    - we can get the value using req.query.id and req.query.name

    ```js
    router.post("/", (req, res) => {
      console.log(req.query);
      console.log(req.query.id);
      console.log(req.query.name);
      res.send("I am get method of user route");
    });
    ```

### [2.7 HTTP Request part-2](https://youtu.be/141Q7XhGGS8)

- example of routes parameter

  - http://localhost:3000/101
  - we can get the value using req.params.id

    ```js
    router.post("/:id", (req, res) => {
      console.log(req.params.id);
      res.send("I am get method of user route");
    });
    ```

- example of how to get data header requests

  ```js
  router.post("/", (req, res) => {
    console.log(req.header("id"));
    res.send("I am get method of user route");
  });
  ```

### [2.8 HTTP Request part-3](https://youtu.be/141Q7XhGGS8)

- example of request with json data

  - first add `app.use(express.json())`; for form data use `app.use(express.urlencoded({extended: true}))`
  - then access the data using `req.body.parameterName`

  ```js
  // sending json or from data when making request
  {
    "name" : "anisul"
  }

  router.post("/", (req, res) => {
    res.status(201).json({
      message: "user is created",
      name: req.body.name,
    });
  });
  ```

### [2.9 send and receive from data](https://youtu.be/GXkth_xoG64)

- create a index.html file inside views folder

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <title>home</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to home page</h1>
        <form action="/users" method="post">
          <label for="name">Name</label>
          <input type="text" id="name" name="name" />
          <button type="submit">Register</button>
        </form>
      </main>
    </body>
  </html>
  ```

- load a html file

  ```js
  // Inside user.routes.js file
  const express = require("express");
  const path = require("path");

  const router = express.Router();

  router.get("/", (req, res) => {
    res.sendFile(path.join(__dirname, "../views/index.html"));
  });

  router.post("/", (req, res) => {
    res.status(201).json({
      message: "user is created",
      name: req.body.name,
    });
  });

  module.exports = router;

  // inside index.js
  const express = require("express");

  const userRoutes = require("./routes/user.routes");

  const PORT = 3000;

  const app = express();

  app.use(express.json());
  app.use(express.urlencoded({ extended: true }));
  app.use("/users", userRoutes);

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### [2.10 Area Calculator](https://youtu.be/u1BgJg6YzYM)

### [2.11 How to set .env variables](https://youtu.be/dxwUjw2Jyfc)

- Step 1: create an .env file in the root directory

- Step 2: define environment variable(S) using uppercase letters and underscore if more than one word. Example -
  PORT
  DATABASE_URL

- Step 3: Assign the values without double quotation and space
  PORT=3000
  DATABASE_URL=mongodb+srv://medo:demo1234@cluster0.0tl3q.mongodb.net/test?retryWrites=true&w=majority

- Step 4: you can make a comment using #

  ```js
  # server port
  PORT=3000
  ```

- Step 5: install dotenv package - npm install dotenv

- Step 6: require dotenv - require('dotenv').config();

- Step 7: Access the env variables from anywhere using process.env.VARIABLE_NAME. Example – process.env.PORT;

- Optional: DotENV Extension - nice syntax highlighting in your .env files.

### [2.12 Middlewares](https://youtu.be/byiRZfg2JaE)

- what is middleware?
  - middleware is a function; it contains request obejct, response object and next function
- why middleware?
  - execute any code inside middleware
  - we can make changes to the request and response object
  - we can end the request and response cycle.
  - we can call the next middleware in the stack.
- Types of middleware

  - Application Level middleware: app.use(), app.METHOD(); here METHOD can be get, put, post, delete, patch
  - router Level middleware: router.use(),router.METHOD()
  - built-in Level middleware: express.json(), express.urlencoded(), express.static()
  - third-party Level middleware: body-parser
  - error handling middleware

    ```js
    // routes not found error
    app.use((req, res, next) => {
      res.status(404).json({
        message: "resource not found",
      });
    });

    // server error
    app.use((err, req, res, next) => {
      console.log(err);
      res.status(500).json({
        message: "something broke",
      });
    });
    ```

### [2.13 express static Middlewares](https://youtu.be/lqRIy6d6D48)

- `app.use(express.static());` helps us to use static resources such as css and image inside our server

### [2.14 MVC Architecture](https://youtu.be/BDeBB9b2L9I)

- MVC Architecture means Model View Controller Architecture
- Model holds all the database related codes
- View is what users see
- Controller is the connection point between Model and View. basically It deals with all the logic.
- example of mvc file structure: setup a project and install necessary packages ( npm init -y && npm install nodemon express body-parser cors)

  <img width="203" alt="Screenshot 2022-04-26 at 05 13 08" src="https://user-images.githubusercontent.com/28184926/165205917-0b83ecc1-9145-40ac-b92f-b8e8cb7511b4.png">

- controllers - user.controller.js

  ```js
  const path = require("path");
  const users = require("../models/user.model");

  const getUser = (req, res) => {
    res.status(200).json({
      users,
    });
  };

  const createUser = (req, res) => {
    const user = {
      username: req.body.username,
      email: req.body.email,
    };
    users.push(user);
    res.status(201).json(users);
  };

  module.exports = { getUser, createUser };
  ```

- models

  - user.model.js

    ```js
    const users = [
      {
        username: "anisul islam",
        email: "lalalal@yahoo.com",
      },
      {
        username: "rakibul islam",
        email: "lalalal@yahoo.com",
      },
    ];
    module.exports = users;
    ```

- routes

  - user.route.js

    ```js
    const express = require("express");
    const { getUser, createUser } = require("../controllers/user.controller");
    const router = express.Router();

    router.get("/", getUser);
    router.post("/", createUser);

    module.exports = router;
    ```

- views

  - index.html

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/api/users">Register</a></li>
          </ul>
        </nav>
        <h1>Home Page</h1>
      </body>
    </html>
    ```

    - user.html

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=], initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/api/users">Register</a></li>
          </ul>
        </nav>
        <h1>User Registration</h1>
        <form action="/api/user" method="post">
          <input type="text" name="username" placeholder="username" />
          <input type="email" name="email" placeholder="email" />
          <button type="submit">register</button>
        </form>
      </body>
    </html>
    ```

- .env
  - `PORT=4000`
- app.js

  ```js
  const express = require("express");
  const cors = require("cors");
  const app = express();
  const bodyParser = require("body-parser");
  const userRouter = require("./routes/user.route");
  // CORS
  app.use(bodyParser.urlencoded({ extended: true }));
  app.use(bodyParser.json());
  app.use(cors());

  app.use("/api/users", userRouter);

  app.get("/", (req, res) => {
    res.sendFile(__dirname + "/views/index.html");
  });

  // routes not found error
  app.use((req, res, next) => {
    res.status(404).json({
      message: "resource not found",
    });
  });

  // server error
  app.use((err, req, res, next) => {
    console.log(err);
    res.status(500).json({
      message: "something broke",
    });
  });

  module.exports = app;
  ```

- index.js

  ```js
  require("dotenv").config();
  const app = require("./app");
  const PORT = process.env.PORT || 5000;
  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### [2.15] Validation with express-validator

- install express-validator

<hr />
<hr />

## Version-2 Express server with a project

## Express tutorial

## 1. Create an express server

- initialize npm and install packages

```js
npm init -y && npm install express
npm install -D nodemon
```

```js
// index.js
const express = require("express");

const app = express();

const port = 3001;

app.listen(port, () => {
  console.log(`server is running at http://localhost:${port}`);
});
```

```json
//package.json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/index.js",
    "start-dev": "nodemon src/index.js"
  },
```

## 2. setting environment variables

## 3. Handle GET Request -> GET all products

- routing plan using HTTP methods for RESTful Services
- HTTP Verbs -> GET, POST, PUT, PATCH, DELETE helps us to CRUD operations

```js
GET /products - get all the products -> 200 (ok) / 404 (not found)
GET /products/:id - get a single product -> 200 / 404
POST /products/ - create a single product -> 201 (Created) / 404 (Not Found) / 409 (Conflict -> Already Exist)
PUT /products/:id - update/replace every resource in a single product -> 200 (Ok) / 404 (Not Found) / 405 (Method Not Allowed)
PATCH /products/:id - update/Modify product itself -> 200 (Ok) / 404 (Not Found)  / 405 (Method Not Allowed)
DELETE /products/:id - delete a single product -> 200 (Ok) / 404 (Not Found) / 405 (Method Not Allowed)

```

```js
// app.use()
app.use("/", (req, res) => {
  res.send("home page");
});

// now use ThunderClient extension for testing the API; you will see app.use() accept all http methods

// app.get() - will only accept get method
app.get("/", (req, res) => {
  res.send("home page");
});
```

```js
let products = [
  {
    id: 1,
    title: "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
    price: 109.95,
  },
  {
    id: 2,
    title: "Mens Casual Premium Slim Fit T-Shirts ",
    price: 22.3,
  },
];

app.get("/products", (req, res) => {
  res.send(products);
});
```

## 4. Middleware

## 5. Handling error

```js
// client error
app.use((req, res) => {
  res.send("<h2>Page not found 404</h2>");
});

// server error
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.send("Something broke!");
});
```

## 6. Response Object

- text, HTML, JSON

```js
res.send("hello");
res.send({
  success: true,
  user: { id: 1, name: "anisul" },
});
res.sendFile("hello.html");
```

## 7. [Status codes](https://devhints.io/http-status)

```js
app.get("/", (req, res) => {
  res.status(200).send("home page");
});

app.get("/products", (req, res) => {
  res.status(200).send(products);
});

app.use((req, res) => {
  res.status(404).send("<h2>Page not found 404</h2>");
});

app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send("Something broke!");
});
```

## 8. Request Object

- request with query parameter - req.query.parameterName

- request with route parameters - req.params.parameterName

- request with headers - req.header(key)

- request with json data / form data inside body - req.body.parameterName

- query parameter has question mark; search something on google.

- example of query parameter - http://localhost:3000?id=101&name=anisul islam

- we can get the value using req.query.id and req.query.name

```js
router.post("/", (req, res) => {
  console.log(req.query);
  console.log(req.query.id);
  console.log(req.query.name);
  res.send("I am get method of user route");
});
```

## 9. Handle GET Request -> get a single product

```js
// route parameter
app.get("/products/:id", (req, res) => {
  const singleProduct = products.find(
    (product) => product.id === Number(req.params.id)
  );
  res.status(200).send(singleProduct);
});

// query parameter
const sortItems = (sortBy, items) => {
  if (sortBy === "ASC") {
    return items.sort((a, b) => a.price - b.price);
  } else if (sortBy === "DESC") {
    return items.sort((a, b) => b.price - a.price);
  }
};

const sortItems = (sortBy, items) => {
  if (sortBy === "ASC") {
    return items.sort((a, b) => a.price - b.price);
  } else if (sortBy === "DESC") {
    return items.sort((a, b) => b.price - a.price);
  }
};

app.get("/products", (req, res) => {
  const maxPrice = Number(req.query.maxPrice);
  const sortBy = req.query.sortBy;
  let result;
  if (maxPrice) {
    result = products.filter((product) => product.price <= maxPrice);
    result = sortBy ? sortItems(sortBy, result) : result;
    res.status(200).send(result);
  } else {
    res.status(200).send(products);
  }
});
```

## 10. Handle POST Request -> create a single product

```js
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

app.post("/products", (req, res) => {
  const newProduct = {
    id: Number(req.body.id),
    title: req.body.title,
    price: req.body.price,
  };
  products.push(newProduct);
  res.status(200).send(newProduct);
});
```

## 11. Handle DELETE Request -> delete a single product

```js
app.delete("/products/:id", (req, res) => {
  products = products.filter((product) => product.id !== Number(req.params.id));
  res.status(200).send(products);
});
```

## 12. Handle PUT Request -> update a single product

```js
app.put("/products/:id", (req, res) => {
  products
    .filter((product) => product.id === Number(req.params.id))
    .map((product) => {
      product.title = req.body.title;
      product.price = req.body.price;
    });
  res.status(200).send(products);
});
```

## 13. MVC Structure - Routing with express Router

- create a router folder and then create a product file where we will move all our routes

```js
//routes -> product.js
const express = require("express");
const router = express.Router();

let products = [
  {
    id: 1,
    title: "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
    price: 109.95,
  },
  {
    id: 2,
    title: "Mens Casual Premium Slim Fit T-Shirts ",
    price: 22.3,
  },
  {
    id: 3,
    title: "Mens Cotton Jacket",
    price: 55.99,
  },
  { id: 4, title: "Mens Casual Slim Fit", price: 15.99 },
];

const sortItems = (sortBy, items) => {
  if (sortBy === "ASC") {
    return items.sort((a, b) => a.price - b.price);
  } else if (sortBy === "DESC") {
    return items.sort((a, b) => b.price - a.price);
  }
};

router.get("/products", (req, res) => {
  const maxPrice = Number(req.query.maxPrice);
  const sortBy = req.query.sortBy;
  let result;
  if (maxPrice) {
    result = products.filter((product) => product.price <= maxPrice);
    result = sortBy ? sortItems(sortBy, result) : result;
    res.status(200).send(result);
  } else {
    res.status(200).send(products);
  }
});

router.get("/products/:id", (req, res) => {
  const singleProduct = products.find(
    (product) => product.id === Number(req.params.id)
  );
  res.status(200).send(singleProduct);
});

router.post("/products", (req, res) => {
  const newProduct = {
    id: Number(req.body.id),
    title: req.body.title,
    price: req.body.price,
  };
  products.push(newProduct);
  res.status(200).send(newProduct);
});

router.put("/products/:id", (req, res) => {
  products
    .filter((product) => product.id === Number(req.params.id))
    .map((product) => {
      product.title = req.body.title;
      product.price = req.body.price;
    });
  res.status(200).send(products);
});

router.delete("/products/:id", (req, res) => {
  products = products.filter((product) => product.id !== Number(req.params.id));
  res.status(200).send(products);
});

module.exports = router;

// inside index.js
const productRouters = require("./router/products");
app.use(productRouters);
```

- remove all the products and in index.js use `app.use("/products", productRouters);`

## 14. MVC Structure - Controller part

```js
// routes -> products.js
const express = require("express");
const {
  getAllProducts,
  getSingleProduct,
  createProduct,
  updateProduct,
  deleteProduct,
} = require("../controller/products");
const router = express.Router();

router.get("/", getAllProducts).get("/:id", getSingleProduct);

router.post("/", createProduct);

router.put("/:id", updateProduct);

router.delete("/:id", deleteProduct);

module.exports = router;

// controller -> products.js
let products = [
  {
    id: 1,
    title: "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
    price: 109.95,
  },
  {
    id: 2,
    title: "Mens Casual Premium Slim Fit T-Shirts ",
    price: 22.3,
  },
  {
    id: 3,
    title: "Mens Cotton Jacket",
    price: 55.99,
  },
  { id: 4, title: "Mens Casual Slim Fit", price: 15.99 },
];

const sortItems = (sortBy, items) => {
  if (sortBy === "ASC") {
    return items.sort((a, b) => a.price - b.price);
  } else if (sortBy === "DESC") {
    return items.sort((a, b) => b.price - a.price);
  }
};

const getAllProducts = (req, res) => {
  const maxPrice = Number(req.query.maxPrice);
  const sortBy = req.query.sortBy;
  let result;
  if (maxPrice) {
    result = products.filter((product) => product.price <= maxPrice);
    result = sortBy ? sortItems(sortBy, result) : result;
    res.status(200).send(result);
  } else {
    res.status(200).send(products);
  }
};

const getSingleProduct = (req, res) => {
  const singleProduct = products.find(
    (product) => product.id === Number(req.params.id)
  );
  res.status(200).send(singleProduct);
};

const createProduct = (req, res) => {
  const newProduct = {
    id: Number(req.body.id),
    title: req.body.title,
    price: req.body.price,
  };
  products.push(newProduct);
  res.status(200).send(newProduct);
};

const updateProduct = (req, res) => {
  products
    .filter((product) => product.id === Number(req.params.id))
    .map((product) => {
      product.title = req.body.title;
      product.price = req.body.price;
    });
  res.status(200).send(products);
};

const deleteProduct = (req, res) => {
  products = products.filter((product) => product.id !== Number(req.params.id));
  res.status(200).send(products);
};

module.exports = {
  getAllProducts,
  getSingleProduct,
  createProduct,
  updateProduct,
  deleteProduct,
};
```

## 15. MVC Structure - Model part

```js
// model -> products.js
let products = [
  {
    id: 1,
    title: "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
    price: 109.95,
  },
  {
    id: 2,
    title: "Mens Casual Premium Slim Fit T-Shirts ",
    price: 22.3,
  },
  {
    id: 3,
    title: "Mens Cotton Jacket",
    price: 55.99,
  },
  { id: 4, title: "Mens Casual Slim Fit", price: 15.99 },
];

module.exports = products;
```

## 16. Deploy on Heroku

- `const port = process.env.PORT || 3001;`
- Procfile -> `web: node index.js`
- add .gitignore file -> `node_modules_`

## 17. Database

- save(), find(), findOne(), deleteOne(), updateOne()

```js
const mongoose = require("mongoose");
mongoose
  .connect("mongodb://localhost:27017/testProduct")
  .then(() => console.log("DB is connected"))
  .catch((error) => {
    console.log(error.message);
    process.exit(1);
  });

// schema & model
const { model } = require("mongoose");
const mongoose = require("mongoose");

const productsSchema = new mongoose.Schema({
  id: Number,
  title: String,
  price: Number,
});

module.exports = model("Product", productsSchema);

// controller
const Products = require("../model/products");

// Create
const createProduct = async (req, res) => {
  try {
    const newProduct = new Products({
      id: Number(req.body.id),
      title: req.body.title,
      price: req.body.price,
    });
    await newProduct.save();
    res.status(200).send(newProduct);
  } catch (error) {
    res.status(500).send(error.message);
  }
};

// Read
const getAllProducts = async (req, res) => {
  try {
    const products = await Products.find();
    res.status(200).send(products);
  } catch (error) {
    res.status(500).send(error.message);
  }
};

// read all the products
const getAllProducts = async (req, res) => {
  try {
    const products = await Products.find();
    const maxPrice = Number(req.query.maxPrice);
    const sortBy = req.query.sortBy;
    let result;
    if (maxPrice) {
      result = await Products.find({ price: { $lt: maxPrice } });
      result = sortBy ? sortItems(sortBy, result) : result;
      res.status(200).send(result);
    } else {
      res.status(200).send(products);
    }
  } catch (error) {
    res.status(500).send(error.message);
  }
};

// read single product by id
const getSingleProduct = async (req, res) => {
  try {
    // const id = parseInt(req.params.id);
    const singleProduct = await Products.findOne({ req.params.id });
    res.status(200).send(singleProduct);
  } catch (error) {
    res.status(500).send(error.message);
  }
};

// delete one product by id
const deleteProduct = async (req, res) => {
  try {
    const id = parseInt(req.params.id);
    const singleProduct = await Products.deleteOne({ id });
    res.status(200).send({ success: true });
  } catch (error) {
    res.status(500).send(error.message);
  }
};

// update a product by id
const updateProduct = async (req, res) => {
  try {
    await Products.updateOne(
      { id: req.params.id },
      {
        $set: {
          title: req.body.title,
          price: req.body.price,
        },
      }
    );
    res.status(200).send({ success: true });
  } catch (error) {
    res.status(500).send(error.message);
  }
};
```

## 18. cors setup

- cors setup

```js
npm install cors
app.use(cors())
```

## 19. connection from front end

```js
import "./App.css";
import React, { useEffect, useState } from "react";
import NewProduct from "./components/NewProduct";

const URL = "http://localhost:4000/products";
function App() {
  const [products, setProducts] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  // update
  const [selectedProduct, setSelectedProduct] = useState({
    title: "",
    price: "",
  });
  const [updateFlag, setUpdateFlag] = useState(false);
  const [selectedProductId, setSelectedProductId] = useState("");

  const getAllProducts = () => {
    fetch(URL)
      .then((res) => {
        if (!res.ok) {
          throw Error("could not fetch");
        }
        return res.json();
      })
      .then((result) => {
        setProducts(result);
      })
      .catch((err) => {
        setError(err.message);
      })
      .finally(() => {
        setIsLoading(false);
      });
  };
  useEffect(() => {
    getAllProducts();
  }, []);

  const handleDelete = (id) => {
    fetch(URL + `${id}`, {
      method: "DELETE",
    })
      .then((res) => {
        if (!res.ok) {
          throw Error("could not delete");
        }
        getAllProducts();
      })
      .catch((err) => {
        setError(err.message);
      });
  };

  const addProduct = (product) => {
    fetch(URL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(product),
    })
      .then((res) => {
        if (res.status === 201) {
          getAllProducts();
        } else {
          throw new Error("could not create new product");
        }
      })
      .catch((err) => {
        setError(err.message);
      });
  };

  const handleEdit = (id) => {
    setSelectedProductId(id);
    setUpdateFlag(true);
    const filteredData = products.filter((product) => product.id === id);
    setSelectedProduct({
      title: filteredData[0].title,
      price: filteredData[0].price,
    });
  };

  const handleUpdate = (product) => {
    console.log(selectedProductId);
    fetch(URL + `/${selectedProductId}`, {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(product),
    })
      .then((res) => {
        if (!res.ok) {
          throw new Error("failed to update");
        }
        getAllProducts();
        setUpdateFlag(false);
      })
      .catch((err) => {
        setError(err.message);
      });
  };

  return (
    <div className="App">
      <h1>Products</h1>
      {isLoading && <h2>Loading...</h2>}
      {error && <h2>{error}</h2>}

      {updateFlag ? (
        <NewProduct
          btnText="Update Product"
          selectedProduct={selectedProduct}
          handleSubmitData={handleUpdate}
        />
      ) : (
        <NewProduct btnText="Add Product" handleSubmitData={addProduct} />
      )}

      {products.length > 0 &&
        products.map((product) => (
          <article key={product.id}>
            <h3>{product.title}</h3>
            <p>{product.price}</p>
            <button
              onClick={() => {
                handleEdit(product.id);
              }}
            >
              Edit
            </button>
            <button
              onClick={() => {
                handleDelete(product.id);
              }}
            >
              Delete
            </button>
          </article>
        ))}
    </div>
  );
}

export default App;


// NewProduct.js
import React, { useState, useEffect } from "react";
import { v4 as uuidv4 } from "uuid";

const NewProduct = ({ handleSubmitData, selectedProduct, btnText }) => {
  const [product, setProduct] = useState({
    title: "",
    price: "",
  });

  const { title, price } = product;

  useEffect(() => {
    setProduct({
      title: selectedProduct.title,
      price: selectedProduct.price,
    });
  }, [selectedProduct]);

  const handleChange = (e) => {
    const selectedField = e.target.name;
    const selectedValue = e.target.value;
    setProduct((prevState) => {
      return { ...prevState, [selectedField]: selectedValue };
    });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const newProduct = {
      id: Number(uuidv4()),
      title: product.title,
      price: product.price,
    };
    handleSubmitData(newProduct);
    setProduct({
      title: "",
      price: "",
    });
  };

  return (
    <form onSubmit={handleSubmit}>
      <div className="field-group">
        <label htmlFor="title">Title: </label>
        <input
          type="text"
          id="title"
          name="title"
          value={title}
          onChange={handleChange}
          required
        />
      </div>
      <div className="field-group">
        <label htmlFor="price">Price: </label>
        <input
          type="text"
          id="price"
          name="price"
          value={price}
          onChange={handleChange}
          required
        />
      </div>
      <button type="submit" className="btn">
        {btnText}
      </button>
    </form>
  );
};

NewProduct.defaultProps = {
  selectedProduct: {
    title: "",
    price: "",
  },
};

export default NewProduct;

```
