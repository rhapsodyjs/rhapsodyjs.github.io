If you want to bootstrap some configuration (like create new log levels), run Grunt or Gulp tasks and so on, it's the place.

the boostrap file is a function that receives the `done` callback as parameter, so this function can be used asynchronously.
Don't **ever** forget to call it, so your app will never run.