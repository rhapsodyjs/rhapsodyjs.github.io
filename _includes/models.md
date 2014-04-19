The RhapsodyJS models follow a generic template, so both server-side and client-side model (e.g. Backbone model) can be generated without code duplication.
All the models of an app must be in the `models` folder, inside the app folder.

## Accessing a model

When programming some action view, you can require a model using the method: Rhapsody.requireModel(modelName), and then use it as a Mongoose model.

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
        option: optionValue
    }
```

### Attribute types

As RhapsodyJS uses Mongoose currently, you can use any of the [Mongoose datatypes](http://mongoosejs.com/docs/schematypes.html):

* `String`
* `Number`
* `Date`
* `Buffer`
* `Boolean`
* `Mixed`
* `Objectid`
* `Array`

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

## Options

A model can have the following options:

* `allowRest` Allow the creation of a RESTful API for this model (see the RESTful API below)
* `middlewares` Middlewares names (see the [Middlewares session](/middlewares.html)) tha the request to the RESTful API will pass before have access to the data.

## RESTful API

RhapsodyJS creates automatically a RESTful API for each model (that can be disabled setting the allowRest option of the model as `false`).

Terminology: `documents` are each of the data stored in a model collection

The RESTful API of each model can be accessed by the path: /data/ModelName, so you can:

* **POST** `/data/ModelName` Insert a new document to the *ModelName* collection with the data sent via POST
* **GET** `/data/ModelName` Return all documents of the model *ModelName*
* **GET** `/data/ModelName/<id>` Return the document of the model *ModelName* with the given *id*
* **PUT** `/data/ModelName/<id>` Update the document of the model *ModelName* with the data sent via PUT
* **DELETE** `/data/ModelName/<id>` Delete the document with the given *id* from the *ModelName* collection

All theses request will first pass by the model middlewares (if any).