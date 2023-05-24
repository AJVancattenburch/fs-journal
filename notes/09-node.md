# Node

## DAY 1

<ul>

  <li>
    In your vs code command directory, with your package.JSON, run npm i and press enter. It will read the JSON file and install all needed files to the particular project you're working on. It will generate a "node_modules" folder.
  </li>

  <li>
    Start at index.js
  </li>

  <li>
    Go into vs code terminal and type node index.js
  </li>

  <li>
    Type npm init to create package.JSON file
  </li>

  <li>
    Paste domain, audience, and client ID into env file. no spaces or quotes.
  </li>

  <li>
    Go into URL box and type localhost.3000/apis/values
  </li>

  <li>
    .get() in your valuescontroller constructor is treated like .on() calling to your AppState
  </li>

  <li>
    Any time you make a change re-spin your server.
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    Make a controller.
  </li>

  <li>
    Export a class in that controller to extend your basecontroller.
  </li>

  <li>
    Build a constructor
  </li>

  <li>
    Add a super directly under constructor with your ('api/thing')
  </li>

  <li>
    Under that add this.router(). Under that put your .get('', this.getThing)
  </li>

  <li>
    Under constuctor, write your try/catch async.
  </li>

  <li>
    as your param always put (req, res, next) in your try/catch async controller function.
  </li>

  <li>
    Under your "try", add a logger.log for req and res. Then re-spin your server.
  </li>

  <li>
    Check postman after changing from a "post" to a "get".
  </li>

  <li>
    Under logger.logs request a res.send('thing')
  </li>

  <li>
    Use req to take data in, res to push it out.
  </li>

  <li>
    Build a fake database to pull fake api information that you create within that database.
  </li>

  <li>
    Under your ObjectController, under your first .get(), write another .get('/:placeholder', this.getThing)
  </li>

  <li>
    post and puts work with body else they do not.
  </li>

  <li>
    "~~()" is short for "Math.Floor()"
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>
<p>```js
  async deleteTiger(req, res, next)
    try {
      let tiger = await tigersService.deleteTiger(req, params, burgerId)
      res.send(tiger) 
    } catch (error) {
      next(error)
    }
</p>```


<br>
<br>


  <li>
    Make model, then controller/service
  </li>

  <li>
    Be sure to select the "start server" option on the top left of vs code.
  </li>

  <li>
    post comes in with a bearer token in your network tab and .use will call as the "middleware" grabs the bearer token and userinfo from auth0 to authenticate the user who made the request.
  </li>

  <li>
    Variables you need in postman are baseurl (localhost:3000), auth (as a bearer token that you paste into your authorization submenu in postman),   
  </li>

  <li>
    Be sure to set files under their parent folders as "inherit"
  </li>

  <li>
    <i>***best reference for data on node.js is from gregslist node project***</i>
  </li>

  <li>
    <b>Queries</b> start with "word?=deeperword" <i></i>
  </li>

  <li>
    Mongoose find method MUST be formatted as an object!
  </li>

  <li>
    Use .forbidden() when adding user business logic to your "editObject()" and "deleteObject()" function in your service later.  </li>

  <li>
    import, paste what is sent to you, use those and set those up like how Sammy did!!!
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

</ul>