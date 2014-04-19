All the Socket behavior are defined here.

The `app/config/socket.js` is a function that receives the `io` object (an instance of [Socket.io](http://socket.io/)) and the `sessionSockets` (only if you has sessions enabled, it's an instance of [session.socket.io](https://github.com/wcamarao/session.socket.io)) as arguments, so you can create the rooms, messagens, listeners and so on.

All the socket [advanced options](https://github.com/LearnBoost/Socket.IO/wiki/Configuring-Socket.IO) must also be done here using the method `io.set(property, value)`.