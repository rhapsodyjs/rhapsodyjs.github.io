In the `app/config/db-adapters.js` file you will register all the JugglingDB adapters you'll be using in your app

This file has the following spec:

```js
{
    adapterOneName: {
        lib: require('adapterOne'),
        adapterOption1: '',
        adapterOption2: '',
        adapterOption3: '',
        adapterOptionN: ''
    },
    adapterTwoName: {
        lib: require('adapterTwo'),
        adapterOption1: '',
        adapterOption2: '',
        adapterOption3: '',
        adapterOptionN: ''
    }
}
```

The options depends of the adapter you'll use, here you can see [all adapters JugglingDB has](https://github.com/1602/jugglingdb#jugglingdb-adapters).

**Don't forget to install the adapter you want to use in your project and add it to the package.json file !**

To use the built-in adapters of JugglingDB, just pass their names in the `lib` option.