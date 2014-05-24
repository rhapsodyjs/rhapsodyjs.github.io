The RhapsodyJS models follow a generic template, so both server-side and client-side model (e.g. Backbone model) can be generated without code duplication.
All the models of an app must be in the `models` folder, inside the app folder.

## Accessing a model

When programming some action view, you can require a model using the method: Rhapsody.requireModel(modelName), and then use it as a [JugglingDB](https://github.com/1602/jugglingdb) model normally.
To see how to use the models, check the [JugglingDB documentation](https://github.com/1602/jugglingdb).

## Spec

```js
var ModelName = {
    attributes: {
        //Write the attributes here
    },

    sharedMethods: {
        //Methods that will be both in server-side and client-side model
    },

    clientMethods: {
        //Methods that will be only in the client-side model
    },

    serverMethods: {
        //Methods that will be only in the server-side model
    },

    options: {
        //Model options
    }
}
```

## Attributes

A model attribute can be writen by two ways:

```js
    attributeWithoutOptions: attributeType,

    attributeWithOptions: {
        option: optionValue (see the options below)
    }
```

### Attribute types

As RhapsodyJS uses [JugglingDB](https://github.com/1602/jugglingdb) for database access, the attribute types dependes on the adapter you're using.
But most of adapters accept the following attribute types:

* `String`
* `Number`
* `Date`
* `Boolean`
* `Object` (You must pass the object, not write `Object` in the type)

### Attribute options

A model attribute can have the following options:

* `type` The type of the attribute. For available types, see above. (**required**)
* `serverValidations` Array of method *names* (that must be in the serverMethods) that validates the attribute
* `default` Default value of the attribute
* `required` If the attribute is required
* `restricted` If the attribute is omited when the model is sent with the RESTful API (see `RESTful API` below)

## Methods

### Shared methods

These methods will be both in the server-side models (returned from a database query) and the client-side models (e.g. Backbone models), so shouldn't contain specific server-side or client-side code.

### Client and Server Methods

Each on them, as the name says, will be attached to theirs respective sides (client-side and server-side) models.

## Model options

A model can have the following options:

* `allowRest` Allow the creation of a RESTful API for this model (see the RESTful API below)
* `middlewares` Middlewares names (see the [Middlewares session](/middlewares.html)) tha the request to the RESTful API will pass before have access to the data.
* `adapter` Name of the adapter this model uses (see the [Database adapters session](/configuration/database-adapters.html)). If not specified, will use the defaultAdapter (see [defaultAdapater](/configuration/environments.html))

## RESTful API

RhapsodyJS creates automatically a RESTful API for each model (that can be disabled setting the allowRest option of the model as `false`).

Terminology: `documents` are each of the data stored in a model collection

The RESTful API of each model can be accessed by the path: /data/ModelName, so you can:

* **POST** `/data/ModelName` Insert a new document to the *ModelName* collection with the data sent via POST and returns it
* **GET** `/data/ModelName` Return all documents of the model *ModelName*
* **GET** `/data/ModelName/<id>` Return the document of the model *ModelName* with the given *id*
* **PUT** `/data/ModelName/<id>` Update the document of the model *ModelName* with the data sent via PUT
* **PATCH** `/data/ModelName/<id>` Update partially the document of the model *ModelName* with the data sent via PATCH
* **DELETE** `/data/ModelName/<id>` Delete the document with the given *id* from the *ModelName* collection

All theses request will first pass by the model middlewares (if any).

If you want just some attributes, you can pass it with the option "attrs" separating them with commas (no spaces), for example:

`/data/ModelName/?attrs=name,registry`

or

`/data/ModelName/someID/?attrs=name,registry`