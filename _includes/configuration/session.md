In the `app/config/session.js` file you will have all the options for the use of sessions in your app.

This file can have the following options:

```js
{
    enabled: true,

    //The id of the session on the browser of the client
    sessionIDKey: 'sessionID',

    //The secret to use signed cookies. If "undefined", the cookies will be unsigned
    cookieSecret: 'rhapsodyCookieSecret', 

    //The secret used to protect the cookie key of the session in the browser of the client
    sessionSecret: 'rhapsodySessionSecret', 

    //The max age of the cookies. If "undefined", the cookies will never expire
    maxAge: 60000, 

    //If undefined, uses MemoryStore
    //otherwise you must pass a store capable of store cookies/sessions
    sessionStore: undefined
}
```