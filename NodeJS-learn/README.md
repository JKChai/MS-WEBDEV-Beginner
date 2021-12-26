# Create a new Node.js project and work with dependencies

Lesson learned from https://docs.microsoft.com/en-us/learn/modules/create-nodejs-project-dependencies

## To Understand

* _manifest file_ - package.json file that contains metadata information for the project & more such as managing dependencies, etc.
* _dependency_ - application needs to depend on third-party library, called dependencies


## To note

`npm init` & `npm init -y` both generate package.json file but `-y` flag is faster because is not interactive by assgining default values.

# Initialize package.json

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