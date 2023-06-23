# **Sockets**

# *Day 1*
* 'Socket Demo'
  + **First step** to get your sockets working, you'll need to set useSockets to true in your .env file on the front-end.

## Example:
```js
  export const dev = window.location.origin.includes('localhost')
  export const baseURL = dev ? 'http://localhost:3000' : ''
  export const useSockets = true
  export const domain = 'dev-pv3d0c0phnn17vle.us.auth0.com'
  export const audience = 'Http://sandbox.com'
  export const clientId = 'RrUWI4Z64ZfQvbPQ5PXr0Bz6iuUCgKZo'
```

  + If you click on the 'ws' filter on your network tab, you should see a new connection to your server. This is your socket connection. If you don't see it, make sure you have the 'ws' filter selected.

  + Web sockets are a fancy way to talk to a server that is not using HTTP or HTTPS. This is a two way connection that allows the server to send data to the client without the client asking for it. This is a great way to get real time updates from the server. Make sure once you turn your sockets to 'true' that you aren't receiving any errors here.

  + On the front-end you are dealing with socketsService.js, on the back-end you will be working with handlers.js. This is where you will be writing your socket logic.

  + In your **AuthHandler.js,** things like *.get, .post, etc.* are now referred to as *.on, .emit, etc.*. This is because you are now listening for events and emitting events. You will still be using the same methods, but they will be called different things.
  ##Example:
  ```js
  constructor(io, socket) {
    super(io, socket)
    this
      .on('authenticate', this.authenticate)

  }
  ```
  + Your **testHandler.js** is where you write your functions to test events.

  + In your network tab, the up arrow is what you are sending to the server, the down arrow is what you are receiving from the server.

  + **.io** is the global socket connection.

  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 