As RhapsodyJS is a HMVC framework, you can define controllers inside Controllers.
For it to work, some name patterns must be followed.

All the controllers must be in the `controllers` folder, inside the app folder.

Each controller must have its own folder, where it will contain:

* `index.js` (file) The file where the actions/views will be programmed, and the controller options will be defined
* `controllers` (folder) The subcontrollers of this controller
* `views` (folder) The folder with the templates of the views of this controller, so you can use `res.view` method to reference the templates without use an absolute path

For example, an app with a `band` controller with a `music` and a `member` controllers inside it, and a `genre` controller, would have the `controllers` folder like this:

```
/controllers/
    |
    `- band/
    |   |
    |   `- index.js
    |   `- views/
    |   |     |
    |   |     `- bio.ejs
    |   |     `- index.ejs
    |   |     `- photos.hbs
    |   |
    |   `- controllers/
    |           |
    |           `- music/
    |           |   |
    |           |   `- index.js
    |           |   `- views/...
    |           |
    |           `- member/
    |               |
    |               |`- index.js
    |               `- views/...
    |
    `- genre/
        |
        `- index.js
        `- views/

```

## The index.js file

The index.js file is where all the controller behavior will be programmed, with each of its views, configurations and so on.

The spec of a controller file is:

```js
var ControllerName = {
    mainView: mainViewName,
    middlewares: [/* Middlewares that apply to the whole controller */]

    views: {
        //Any of the views
    }
}
```

### Main view

Should be a string, with the name (or verb:name) of the main view of the controller.

Using our example above, the mainView option of our `band` controller would be the name of the view when the user access /band, without the view name.

### Middlewares

The middlewares defined here are applied to all the views of the controller (see the [Middlewares session](/middlewares.html)).
Should be an array of strings (so it will be the middleware with the same name in the `middlwares` folder) or functions (so the function itsel will be the middleware).

### Views

Any of the views of this controller

A view can be described by two ways:

```js

    staticViewName: 'viewFile',

    dynamicViewName: {
        option: optionValue
    }

```

The view name can be just its name (so the view verb will be set to the default `get` value) or in the form: `verb:name`. For example:

* `post:login`
* `put:updateUser`

#### Static views

The static views will not have middlewares, nor data will be processed to render it, RhapsodyJS will just send the file `controllerName/views/viewFile` to the client.

#### Dynamic views

The dynamic views must have a `action` option. This options can be described by two ways:

```js
    
    dynamicViewWithFileName: {
        action: 'viewFile',
        middlewares: [middlewaresNames],
        params: [paramsNames]
    },

    dynamicViewWithoutFileName: {
        action: function(req, res) {
            //View computing here
        },
        middlewares: [middlewaresNames],
        params: [paramsNames],
        customRoutes: [customRoutes]
    }

```

##### Dynamic view with file

They are similar to the static views, but now you can put middlewares to this view

##### Dynamic view without file

This is the more flexible type of view. You will have access to the `req` (from "request") object, and send the view to the client-side with the `res` (from "responde") object.
RhapsodyJS uses [Express](http://expressjs.com/api.html) internally, so if you know Express, you know how to use it

The unique difference between Express in this part is that the response argument will have as a plus the method `res.view` (but you still can use the `res.render` from Express).
The method `res.view` has an only object argument, with the following attributes:

* `name` The name of the view file. It's a relative path to `controller/views/fileName`
* `locals` The locals to use inside the file that will be interpreted by some template engine (see Template Engine in the [Configuration session](/configuration))

##### Middlewares

The middlewares arrays inside of a view defines the middlewares a request to a view will pass before reach the view.
This middlewares can be used to create administrator areas, areas of a site that can only be accessed by logged users and so on.

##### Params

It follows the Express params pattern, so if, in our example above, you want to see all the bands with the genre "punk-rock" from the 80's, you can create the following view in the genre controller:

```js
search: {
    action: function(req, res) {
        var Band = Rhapsody.requireModel('Band');

        Band.find({style: req.params.genre, age: req.params.age}, function(err, bands) {
            if(err) {
                Rhapsody.log.error(err);
                res.send(404);
            }
            else {
                res.view({
                    name: 'search.hbs',
                    locals: {
                        bands: bands
                    }
                });
            }
        });
    },

    params: [':genre', ':age']
}
```

So if the user can now access: `/genre/search/punk-rock/80` and all the bands with this style will be shown.

##### Custom routes

You can also specify custom routes for your views.

Using our example above, if you want that the user just use `/genre-x-age/punk-rock/80` to look for punk rock bands of the 80's, you can add the following attribute to the view object:

```js
customRoutes: ['/genre-x-age']
```

**Don't forget the '/' in the begining of the custom route's path, or the custom routes won't work!**