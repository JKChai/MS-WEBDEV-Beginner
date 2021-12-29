# Node.js

> An open-source, server-side JavaScript runtime environment.

> Node.js environment also offers an npm registry that you can use to share your own Node.js library

## Architecture

> Node.js is based on a single-threaded event loop. This architecture model efficiently handles concurrent operations. *Concurrency* means the ability of the event loop to perform JavaScript callback functions after completing other work.
> * *Single-threaded* means that JavaScript has only one call stack and can do only one thing at a time.
> * The *event* loop runs the code, collects and processes events, and runs the next subtasks in the event queue.
> * A *thread* in this context is a single sequence of programmed instructions that the operating system can manage independently.

> In Node.js, I/O operations such as reading or writing to a file on the disk, or making a network call to a remote server, are considered blocking operations. A *blocking operation* blocks all subsequent tasks until the operation is finished before the next operation can proceed. In a *non-blocking* model, the event loop can run multiple I/O operations at the same time.

The name *event loop* describes the use of the "busy-waiting" mechanism that waits synchronously for a message to arrive before processing it. The following shows an event loop implementation:

```JS
while (queue.wait()) {
  queue.process();
}
```

## Asynchronous programming

> To support the powerful event-based programming model, Node.js has a built-in set of non-blocking I/O APIs to handle common tasks such as file-system and database manipulation. These APIs are provided by the libuv library. 

## Node.js REPL

> Node.js has a built-in read-eval-print loop (REPL) mode that's useful for quick code evaluation and experimentation. REPL mode is an interactive console environment where you can enter JavaScript code and have Node.js interpret and run the code and then print the output.

> The Node.js REPL mode works as follows:
> * Read: Reads and parses the user's JavaScript code input (or shows an error if the code is invalid).
> * Eval: Evaluates the entered JavaScript code.
> * Print: Prints the computed results.
> * Loop: Loops and waits for the user to enter a new command (or exits if the user enters ctrl-c twice).

# Create a new Node.js project and work with dependencies

Lesson learned from https://docs.microsoft.com/en-us/learn/modules/create-nodejs-project-dependencies

## To Understand

* _manifest file_ - package.json file that contains metadata information for the project & more such as managing dependencies, etc.
* _dependency_ - application needs to depend on third-party library, called dependencies


## To note

`npm init` & `npm init -y` both generate package.json file but `-y` flag is faster because is not interactive by assgining default values.

## Initialize package.json

### package.json file 

* **Meta-information** - information about the project: name, description, author, and keywords.
* **Dependencies** - `dependencies` and `devDependencies` used to describe the libraries that are being used.
* **Scripts** - To do things like start, build, test, and lint a project.

### Script key

There are 4 basic elements for key `script` and is usually written as below as in JSON format.

```JSON
// Reference
"scripts" : {
  "<action>" : "<command>"
}

// Sample
"scripts" : {
  "start" : "node ./dist/index.js",
  "test": "jest",
  "build": "tsc",
  "lint": "eslint"
}
```

* `start` - starts the application that invokes `node` command with the entry file as an argument
* `build` - use to ship the project, e.g., use TypeScript compiler to compile typescript code
* `test` - use to run tests by using test framework such as `jest`
* `lint` - invoke selected linter program normally for readability

Note that actions can be invoked by running `npm run <action>` but some actions such as `start` & `test` are *special* actions in which can be ran by `npm <action>`

Set up configuration of node.js with command action `npm init -y` in which creates the package.json

Factors that determine if any packages are needed:
* Getting better code
* Saving time
* Maintenance

Factors for inspecting the dependencies:
* Size
* Licensing
* Active Maintenace

Some simple commands:
* `npm view <package name>` - View package dependencies 
* `npm install <package name>` - Install a package

`jest` is a more common test package for testing the input & output.

## Manage dependency updates

Considerations before updating:
* type of update
* whether the project is configured correctly
* security problems

### Semantic Versioning

> An industry standard for expressing the type of change that you or some other developers is introducing to a library by ensuring a package has a version number:
* Major version - means to expect breaking changes in the code; part of the code may need to rewrite
* Minor version - means features have been added; generally safe to accept update
* Patch version - means a change has been applied that fixed something in the code that should have worked; generally safe to accept update

> For example, version 1.2.3 is divided as major.minor.patch version

To update package with `npm`: `npm update <package name>@<optional argument version number>`

Two things to considerate:
* whether the version argument is specified as part of the command
* the entry in the manifest file, e.g., `<dependency name>:<version number>`

> Configuration for update, under normal circumstances:
* `~` or `1.1.x` - update to the latest patch version
* `^` or `1.x.1` - update to only the minor version
* `*` or `x.0.0` - update to the highest major version

### package-lock.json file

A file uses to keep track of the exact version of every package that is installed so that a product is 100% reproducible in the same way even if packages are updated by their maintainers.

Note that package.json file newest version override package-lock.json file

### Find & Update Outdated packages

Use `npm outdated` command, output as:
* `Wanted` - version wanted matches the semantic version
* `Latest` - latest version of the package
* `Location` - location of dependency

### Manage Security issues

High vulnerbilities from installation of dependecy requires update. Hence, audit and fix is needed by using `npm audit` to list each vulnerability; `npm audit fix` try to fix the problem, `npm audit fix --force` update to major version

Use `npm install <package name>@latest` to install latest packages

# Interactively debug Node.js apps with the built-in and Visual Studio Code debuggers

> "If debugging is the process of removing bugs, then programming must be the process of putting them in." from Edsger Dijkstra

Two important debugger features:
* Control of your program execution
* Observation of your program's state

Debugging process (Multistep):
1. Identify a bug in your program
2. Find where the bug is located in your code
3. Analyze where the bug is located in your code
4. Fix the bug
5. Validate that your fix works

Using *breakpoint* to stop the process for step-by-step evaluation of the code, which can be done by using `debugger` statement

```JS
function addToBasket(product) {
  // pause at the beginning of this function
  debugger;

  const basket = getCurrentBasket();
  basket.add(product);
}
```

For security purpose, enable node.js inspect mode using `--inspect` flag, e.g., `--inspect=<host>:<port>` for custom host and port or by default listening on host `127.0.0.1` on port `9229`. Another flag `--inspect-brk` works the same but break code execution just before the start of code

## Built-in Debugger

```bash
# input
node inspect <YOUR_SCRIPT>.js

# output as below
node inspect myscript.js
< Debugger listening on ws://127.0.0.1:9229/ce3689fa-4433-41ee-9d5d-98b5bc5dfa27
< For help, see: https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in myscript.js:1
> 1 const express = require('express');
  2
  3 const app = express();
debug>
```

Common commands to use during the inspection process:
* `cont` or `c` - continue until the next breakpoint or the end of the program
* `next` or `n` - execute next line of code
* `step` or `s` - same as `n` but will move to the function line of code if the next code is a function call
* `out` or `o` - jump out a function call and move to the next line of code
* `restart` or `r` - restarts the program and pauses the execution before the start of your code

Get information about current execution point:
* `list(<N>)` - list source code with *N* lines before and after the current execution point
* `exec <EXPR>` - evaluate an expression within the current execution context, e.g., evaluate variable `i` using `exec i`; mutiple variables is viewable using array such as `exec [i, sum]` for both i & sum variables

Commands for setting and clearing breakpoints of a code:
* `setBreakpoint`or `sb()` - add breakpoint on the current line
* `setBreakpoint(<N>)`or `sb(<N>)` - add breakpoint on line number *N*
* `clearBreakpoint('myscript.js', <N>)` or `cb('myscript.js', <N>)` - clear the breakpoint in the file `myscript.js` on line number *N*

To exit, press "Ctrl + D" or select command `.exit`

Debugging can be done with:
* node.js CLI
* Visual Studio Code

Using VSC for debugging required `launch.json` for configuration by checking the entry point of the file for debugging: `Run` >> `Configuration` >> `Node.js`

# Work with files & directories

## Work with file system

*fs* is a default package named *file system* in which use to read files and folders

```JS
const fs = require("fs");
```

## Work with file paths

*path* is a default package to work with path because this module works properly in different operating systems in regard to searching directories, e.g., `/` for linux & `\` for windows

```JS
const path = require("path");
```

To join path:
```JS
console.log(path.join("stores", "201")); // stores/201
```

Get most of the information with `parse` method
```JS
console.log(path.parse("stores/201/sales.json"));
// { root: '', dir: 'stores/201', base: 'sales.json', ext: '.json', name: 'sales' }
```

## Create files & directories

* `fs.mkdir` method creates directories
* `fs.writeFile` method creates files

## Read & Write files

* `fs.readfile` method to read files which output `buffer` values
* `fs.writeFile` method creates files and can append values to file

```JS
const data = JSON.parse(await fs.readFile("stores/201/sales.json"));

// write the total to the "totals.json" file
await fs.writeFile(path.join("salesTotals/totals.txt"), `${data.total}\r\n`, {
  flag: "a"
});
// \r\n is carriage return line feed

// totals.json
// 22385.32
// 22385.32
```

> A few things to keep in mind from this module
> * Always use the `promises` namespace on the built-in modules. You can then use the `async` and `await` operators to make code synchronous without blocking program execution.
> * Whenever you are creating a directory, make sure that you wrap it in a `try/catch`. The default behavior in Node.js is to throw an error when you try to create a directory that already exists. If you just want to check if a directory exists or not, you can use the `stat` method. Note that this method does not exist on the `promises` namespace, but on the main `fs` object.
> * If you need to parse other file types, check out the packages on npmjs.org. For example, you can use the [papaparse](https://www.npmjs.com/package/papaparse) package for .csv files. You can use the [fixy](https://www.npmjs.com/package/fixy) package for fixed-width files.

# Build WEB API with Node.js & Express

> Important concepts to consider when you build web applications and APIs:
> * **Routing**: Your application is divided into different sections based on parts of the URL address.
> * **Support for different content types**: The data to serve up might exist in different file formats, Such as plain text, JSON, HTML, CSV, and more.
> * **Authentication/Authorization**: Some data might be sensitive. A user might need to sign in or have a specific role or permission level to access the data.
> * **Read/Write data**: Users usually need to both view and add data to the system. To add data, users might enter data in a form or upload files.
> * **Time to market**: To create web applications and APIs efficiently, choose tools and libraries that provide solutions to common problems. These choices help the developer spend as much time as possible on the business requirements of the job.

## HTTP module

> The following classes help manage a request from start to finish:
> * **http.Server**: Represents an instance of an HTTP Server. This object needs to be instructed to listen to different events on a specific port and address.
> * **http.IncomingMessage**: This object is a readable stream created either by **http.Server** or **http.ClientRequest**. Use it to access status, headers, and data.
> * **http.ServerResponse**: This object is a stream created internally by the HTTP Server. This class defines what the response should look like, for example, the type of headers and the response content.

**Streams** makes server capable of handling many concurrent requests; define how data is transported; an operating concept not Node.js concept; a fundamental data strucutre of Node.js that read and write data, and send and receive messages or *events* 

> The **req** and **res** parameters from the example are streams. Use the method **on()** to listen to incoming data from a client request like this:

```JS
req.on('data', (chunk) => {
  console.log('You received a chunk of data', chunk)
})
```

Use the method **end()** for data sent back to the client in the response stream **res**:

```JS
res.end('some data')
```

### Express framework

Help make app scalable
> * **Good features**: Express has a set of features that makes you fast and productive.
> * **Abstracts away complexity**: Express abstracts away complicated concepts like streams, for example, and makes the whole development experience a lot easier.
> * **Solves common Web problems**: Express helps you with common problems such as route management, caching, and redirection.
> * **Trusted by millions of developers**: According to GitHub, 6.8 million developers currently use Express for their web applications.

Some conceputal knowledge:
* `http://localhost:3000/products` end part of the URL is a *route*: `/products`
* `HTTP verbs` - action for data such as: post, put, get

> Follow these steps to create a web application using the Express framework:
> 1. **Instantiate the app**: Create a web application instance. At this point, the instance can't be run, but you have something you can extend.
> 2. **Define routes and route handlers**: Define what routes the application should listen to. A route is part of the URL. For example, in the URL http://localhost:8000/products, the route part is /products. Express uses different routes to execute different pieces of code. Other examples of routes are /, also known as the default route, and /orders. Routes will be explored in more detail later in this module.
> 3. **Configure middleware**: Middleware is a piece of code that can run before or after a request. You can also use middleware to handle authentication/authorization, or to add a capability to your app.
> 4. **Start the app**: Define a port, and then instruct the app to listen to that port. Now the app is ready to receive requests.

## Manage a request lifecycle with middleware

> Request steps:
> 1. **Pre request**: Investigate whether the user sent the proper credentials through a request header. If the credentials are verified, send the request to the next step.
> 2. **Construct the response**: Talk to some kind of data source, like a database or an endpoint. This step returns the resource, as long as the request asks for the resource correctly.
> 3. **Post request**: This is an optional step to run a piece of code after the request is handled. You might run this step for logging purposes.

> A pre or post request in Express is known as a *middleware*, and has the following shape:
```JS
// use the use method
app.use((req, res, next) => {})
```

> Request Pipelines:
> * Middleware that needs to run before the request (pre request) is defined before the actual request.
> * Middleware that needs to run after the request (post request) is defined after the actual request.
```JS
app.use((req, res, next) => {
  // pre request
})
app.get('/protected-resource', () => {
  // handling the actual request
})
app.use((req, res, next) => {
  // post request
})

app.get('/login', () => {})
```

# Route management in Node.js with JavaScript

## Understand URLs and routes

**URL** - An address to locate specific server and resources:
```bash
http://localhost:8000/products/1?page=1&pageSize=20

##########
scheme:[//authority]path[?query][#fragment]
``` 

* scheme - indicates protocol such as `https`, `ftp`, `irc`, `file`
* authority - consists of optional user info (*username@password*) and a host; can be describe in host, ip address, or domain name
* path - consists of segments seperated by `/`
* query - (optional) defined after `?` with `key=value` pairs seperated by `&` or `;`
* fragment - (optional) for more specific call/search such as filtering

**Route** - a subsection of a URL that usually points to a specific resource

* route parameter - signals that you want to access a specific resource from a collection
> E.g., route `/orders/1/items/2`, the route parameters are `1` and `2`. The `1` signals that you want a specific order with the unique key `1`. The `2` asks for a specific order item with the unique key `2`. These route parameters return a specific resource rather than all resources of a specific type.
* query parameter - a set of key/value pairs that exist after the `?` character

| Route                        |	Express route pattern |
|------------------------------|------------------------| 
| /products                    |	products/             |
| /products/1 and products/114 |           products/:id |
| /orders/1/items/2    |	orders/:orderId/items/:itemId |
|xyz	                 | **                             |

** - indicate *catch-all*; use it to handle typos, etc. in a graceful manner

**HTTP verb** - express the *what*. E.g., `get` expresses reading data from the resource and `post` expresses writing data to the resource

### **CRUD** api:
* Create
* Read
* Update
* Delete

There are differences under the implementation of `route` method used in express framework especially when it comes to *delete* verb. See the `read-write` files for specific details.


