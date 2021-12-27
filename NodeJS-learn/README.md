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


