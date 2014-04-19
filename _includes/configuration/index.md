The configuration file `app/config/config.js` is where the environment is set.

## Environment

Should be a string, the name of the current environment of your app.
Initially RhapsodyJS creates two environment files for you (dev.js and prod.js, plus a all.js file with configurations common for all environments), but you can create infinite environment files inside the `env` folder and use its name (without the ".js") as a value to this option.