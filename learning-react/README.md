# Understand REACT

> Course lesson from https://docs.microsoft.com/en-us/learn/modules/react-get-started

The solutions and practice of the code is kept under the mslearn-react local directory and not uploaded to github.

## Concepts

- Model-View-Controllers: A software design principles  
- REACT uses special syntax known as JavaScript XML (JSX)

> Differences between XML & HTML
> * All elements must be placed inside one parent element
> * All elements must be closed

### Build Process

> Browsers don't support JSX. Tools such as `Webpack`, `Parcel`, `Snowpak` can solve this issue by making it a blunder.

### Components

> React development is based on components that are reusable, self-contained units, and make the core of any react application.

### Starter file descriptions

> learning packages use in `mslearn-react/code/0-starter` directory

* __package.json__ contains the list of packages and scripts:
    * Packages:
        * React for React
        * ReactDOM to mount our application inside the browser
    * Scripts:
        * __dev__ to run the development server from Snowpack:
            * It virtually builds all JavaScript and HTML files.    
            * It hosts and automatically restarts the server as files are changed.
        * __build__ to generate production files for deployment
* snowpack.config.json contains the core configuration for Snowpack.
    * __mount__ creates two virtual directories for our Snowpack server.
        * __public__ contains all static files (such as HTML, CSS, and images). It's hosted as /.
        * __src__ contains all JSX files and associated React files. It's hosted as dist.
* __public__ contains all static files.
* __src__ contains all React files.

## Properties (props)

> parts that make up component; `props` are read-only values available to a single instance of a component in which can be complex objects or arrays and is capable of storing objects and any other data type

Properties are powerful where it allows us to create dynamic data using JavaScript in html under `JSX` extension. Moreover, it can create complex data type of JavaScript object rating than prelimary data type or string type making it much more robust for development.

For example, `className` is used to assign the class tag in html and can apply dynamic data type by setting the `className` under ternary operator. Other than that, `map` method is utilize to create or modify an array.

# React State and Events

> `State` is data that can be updated and shared between components throughout your application. `Events` allow you to handle all the ways a user can interact with your application: the clicks, typing, and taps.

## Concept of State

* `Props` - `Props` are values passed to React components. These copies of the data are designed to allow the component to render itself. `Props` are `immutable` (read-only) values.
* `State` - `State` stores any data we expect to change during the application's life cycle. Changes might be values updated through a form, to-do items marked as completed, or updated server data that needs to be displayed on the page. Basically, if the value can change, it should be part of the application's state.
* `Immutability` - One of the tenets of React is the concept of `immutability`. Immutability means that values aren't updated but are rather set to new copies of data.

> By keeping state immutable, React can better determine what has changed, because the original values still exist. This continual use of new copies allows you to store history or apply other advanced functionality.

## Managing State

One of the method to manage `State` in react is *React Hooks*

> A *Hook* is a mechanism that allows you to access the inner workings of React. You can use Hooks to run code when something changes in React. Or use them to register something with React, such as state. When we create state by using the `useState` Hook, for example, we get the state object and an updater function to update the *Hook* value.

### Copy Object

This can be done with *spread syntax*, also known as *spread operator* `...`

```JS
let message = {
    text: 'Hello, world',
    color: 'red'
}

let messageCopy = {
    ...message,
    color: 'green'
};
```

Example above shows that the spread operator create a copy of the `message` variable & output as follow.

```JS
// new object
{
    text: 'Hello, world',
    color: 'green'
}
```

