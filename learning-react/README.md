# Understand REACT

> Course lesson from https://docs.microsoft.com/en-us/learn/modules/react-get-started

## Concepts

- Model-View-Controllers: A software design principles  
- REACT uses special syntax known as JavaScript XML (JSX)

> Differences between XML & HTML
> * All elements must be placed inside one parent element
> * All elements must be closed

### Build Process

> Browsers don't support JSX. Tools such as `Webpack`, `Parcel`, `Snowpak` can solve this issue.

### Components

> React development is based on components 

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