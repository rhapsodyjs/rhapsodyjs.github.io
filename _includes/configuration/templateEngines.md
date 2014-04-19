RhapsodyJS allows you to use any template engine you want! (Well, [almost it](https://github.com/visionmedia/consolidate.js/)).

In this file you will define the template engines you'll be using in your app, and the default engine if you don't specify a file extension when rendering a view.

A example file of an app that used EJS and Handlebars as templates engines is:

```js
{
  defaultEngine: 'ejs',

  engines: {
    ejs: {
      extension: 'ejs',
      lib: require('ejs')
    },
    
    handlebars: {
      extension: 'hbs',
      lib: require('handlebars')
    },

    /**
     * engineName: {
     *  extension: 'engineExtension',
     *  lib: require('engine')
     * }
     */
  }
}
```