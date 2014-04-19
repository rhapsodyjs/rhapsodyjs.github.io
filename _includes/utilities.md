Here will be listed some utilities created to be used inside your RhapsodyJS app.

## Logging

For use the logging system (configured in the file of your current environment in `app/config/environment_name.js`), you just use:

```js
	Rhapsody.log.LOG_LEVEL(TITLE, MESSAGE);
```

For the API of `Rhapsody.log`, see the [WolverineJS API](https://www.npmjs.org/package/wolverine).

## Libs

All libs used internally by RhapsodyJS that you possibly would use in your app are accessible trough the `Rhapsody` global variable, they are:

* `Rhapsody.libs.express` https://www.npmjs.org/package/express
* `Rhapsody.libs.jsmin` https://www.npmjs.org/package/jsmin
* `Rhapsody.libs.lodash` https://www.npmjs.org/package/lodash
* `Rhapsody.libs.wolverine` https://www.npmjs.org/package/wolverine

## Middlewares

When you're configuring the middlewares of a controller or a view, you can set any of then as the name of a file inside the `app/middlewares` folder (without the `.js`) or the function itself.

The NodeJS community has already created some standard middlewares, and some of them can be accessed by the `Rhapsody` global variable, they are:

* `Rhapsody.middlewares.compression` https://www.npmjs.org/package/compression
* `Rhapsody.middlewares.methodOverride` https://www.npmjs.org/package/method-override
* `Rhapsody.middlewares.bodyParser` https://www.npmjs.org/package/body-parser
* `Rhapsody.middlewares.multiparty` https://www.npmjs.org/package/connect-multiparty
* `Rhapsody.middlewares.cookieParser` https://www.npmjs.org/package/cookie-parser
* `Rhapsody.middlewares.session` https://www.npmjs.org/package/express-session
* `Rhapsody.middlewares.csurf` https://www.npmjs.org/package/csurf
* `Rhapsody.middlewares.cors` https://www.npmjs.org/package/cors

## App root folder

The app root folder (that contains the `app`, `node_modules`, `app.js` and `package.json`) can be accessed by the variable `Rhapsody.root`.