In the `app/config/envs` are defined all the configurations for any of the environments of your app.
The `all.js` file contains configurations common for all the environments.

An environment file with all the options has the following form:

```js
var config = {
    host: 'localhost',

    http: {
        port: 4242,
        socket: true
    },

    https: {
        enabled: true,
        port: 4243,
        socket: true
    },

    methodOverride: {
        enabled: true,
        attributeName: 'newMethod',
    },

    database: {
        enabled: true,
        defaultAdapter: ''
    },

    log: {
        //For log levels, see WolverineJS documentation: https://github.com/talyssonoc/wolverinejs
        level: 'debug',

        //if undefined, will print to the terminal
        output: '/home/rhapsody/log.log',

        //If true, will print the error stack if an Error object is passed as argument in some log method
        printStack: false,

        //If true, show the debug level before the message
        printLevel: true,

        //If true, shows the time the log was logged before the level name
        time: true,

        //If true, show and file and the line number of where the log was called
        printFileInfo: true
    },

    routes: {
        //Controller used when access the app's root
        mainController: 'main',

        //View used when the user doen't specify it
        mainView: 'index',

        //If must be created REST routes for models
        allowREST: true
    },

    //If true, uploaded files via form will be at req.file
    upload: {
        enabled: true,
    },

    compression: {
        enabled: true
    },

    //See CSFR session to see how it works
    csrf: {
        enabled: false
    },

    generateClientModels: true
}
```