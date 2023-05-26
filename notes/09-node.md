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
  
  <br>

  <li>
    <b></b>
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
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
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
  
  <br>

  <li>
    <b>Queries</b> start with "word?=deeperword"
  </li>

  <li>
    Mongoose find method MUST be formatted as an object!
  </li>

  <li>
    Use .forbidden() when adding user business logic to your "editObject()" and "deleteObject()" function in your service later.  </li>

  <li>
    import, paste what is sent to you, use those and set those up like how Sammy did!!!
  </li>
  </ul>

## <U>DAY 3</U> ##

  <ul>
  <li>
    3 Types of data relationships
  </li>

  <li>
    1 to 1: exists independently of each other
  </li>

  <li>
    One to Many: one that points to many things
  </li>

  <li>
    Many to Many: Many things point to many things.
  </li>

  <li>
    Many to Many relationships need a "middle-man" to handle the synchronizing properties.
  </li>

  <li>
    <b><h2><u>STEPS</u></h2></b>
  </li>

  <br>
  <br>

  <li>
    <b>INITIALIZE REPOSITORY IN GITHUB</b>
  </li>
  


  <li>
    <b>RUN "BCW SERVE" IN YOUR CLIENT FOLDER</b>
  </li>
  
  <br>

  <li>
    <b>GRAB ASSIGNMENT VARIABLES AND PUT THEM IN .ENV FILE</b>
  </li>
  
  <br>

  <li>
    <b>START AT YOUR MOST PARENT COLLECTION</b>
  </li>
  
  <br>

  <li>
    <b>CREATE SCHEMA FOR SAID UTMOST PARENT COLLECTION WITH OBJECTS NAME (OBJECT.JS FILE)</b>
  </li>
  
  <br>

  <li>
    <b>BUILD OUT CREATE FUNCTION IN CONTROLLER AND SERVICE TO GET A SUCCESSFUL LOGGER</b>
  </li>
  
  <br>

  <li>
    <b>MAKE NEW COLLECTION FOR YOUR CODE IN POSTMAN</b>
  </li>
  
  <br>

  <li>
    <b>SET UP BASEURL IN YOUR VARIABLES</b>
  </li>
  
  <br>

  <li>
    <b>MAKE A FOLDER IN YOUR NEW COLLECTION FOR YOUR CREATE FUNCTIONALITY WITH "POST"</b>
  </li>
  
  <br>

  <li>
    <b>BRING IN YOUR BASEURL AND API INTO YOUR POST TO CREATE IN POSTMAN</b>
  </li>
  
  <br>

  <li>
    <b>POST SCHEMA FOR OBJECT FROM VSCODE TO POSTMAN</b>
  </li>
  
  <br>

  <li>
    <b>CREATE WHAT YOU WOULD LIKE IN YOUR POST USING YOUR SCHEMA AS A MODEL IN POSTMAN</b>
  </li>
  
  <br>

  <li>
    <b>CREATE MULTIPLE INSTANCES TO POST USING WORKSPACE IN POSTMAN</b>
  </li>
  
  <br>

  <li>
    <b>WRITE YOUR GET FUNCTION IN YOUR CONTROLLER</b>
  </li>
  
  <br>

  <li>
    <b>ALWAYS SET UP YOUR GET REQUESTS WITH A QUERY (CONST QUERY = REQ.QUERY) AT THE BEGINNING OF YOUR ASYNC FUNCTION IN YOUR CONTROLLER</b>
  </li>
  
  <br>

  <li>
    <b>RESPIN IN VS CODE, THEN IN POSTMAN GENERATE YOUR OUTCOME WITH A GET</b>
  </li>
  
  <br>

  <li>
    <b>IF YOU GET A 404 AFTER THIS, GO TO THIS.ROUTER IN YOUR CONTROLLER. (LOOK FOR SYNTAX '/:id')</b>
  </li>
  
  <br>

  <li>
    <b>ADD IN THE SERVICE LAYER, TO YOUR GETBYID() FUNCTION, IF(!OBJECT) THROW NEW BADREQUEST</b>
  </li>
  
  <br>

  <li>
    <b>AT THE END IF YOUR REQ.PARAMS."" - IT NEEDS TO MATCH WHAT YOU ARE BRINGING IN INSIDE OF YOUR THIS.ROUTER</b>
  </li>
  
  <br>

  <li>
    <b>CREATE INSIDE OF YOUR NEWLY DEFINED OBJECT, A FOLDER THAT GOES A LAYER DEEPER INTO YOUR INFO WITH A POST REQUEST ON THE NEW ITERATION</b>
  </li>
  
  <br>

  <li>
    <b>NO NEED TO WRITE YOUR ID IN YOUR SCHEMA - POSTMAN WILL TAKE CARE OF THAT FOR US</b>
  </li>
  
  <br>

  <li>
    <b>WHEN DEFINING THE RELATIONSHIP ID TYPE FOR THE NEXT SCHEMA - ITS THE NEXT OBJECTID TYPE SCHEMA.TYPES.OBJECTID, WITH A REF: 'PREVIOUS OBJECT'</b>
  </li>

  <br>

  <li>
    <b>INSERT TIMESTAMPS TRUE IN THE ABOUT TO BE MIDDLE-MAN SCHEMA</b>
  </li>
  
  <br>

  <li>
    <b>BUILD YOUR VIRTUAL LAYER IN THE BOTTOM OF YOUR SCHEMA</b>
  </li>

  <br>

  <li>
    <b>INSERT NEW SCHEMA INFO INTO YOUR DBCONTEXT.JS</b>
  </li>
  
  <br>

  <li>
    <b>AFTER MAKING THAT NEW CONTROLLER AND SERVICE LAYER, AGAIN COPY/PASTE YOUR SCHEMA MODEL INTO POSTMAN AS A "POST" FOR YOUR CREATE FUNCTION</b>
  </li>

  <br>

  <li>
    <b>BUILD OUT THAT SCHEMA'S ATTRIBUTES IN POSTMAN</b>
  </li>
  
  <br>

  <li>
    <b>TO ADD ANOTHER SCHEMA BASED FROM ANOTHER, GRAB THAT PARENT SCHEMAS ID FOR THE NEW SCHEMAS REFERENCE ID</b>
  </li>

  <br>

  <li>
    <b>TO GRAB YOUR NEW MODELS, WRITE A GET FUNCTION IN YOUR CONTROLLER.</b>
  </li>
  
  <br>

  <li>
    <b>VIRTUALS NOW COME INTO PLAY TO SHOW WHAT THE NEXT RELATED SCHEMA IS FOR</b>
  </li>

  <br>

  <li>
    <b>REFERENCE THAT WITH A .POPULATE() METHOD ON THE END OF YOUR QUERY GETTER INSIDE YOUR ASYNC FUNCTION WITHIN YOUR CONTROLLER LAYER</b>
  </li>
  
  <br>

  <li>
    <b>FOR GRABBING A PARENT'S CHILDREN SCHEMA, .GET('/:OBJECTID/CHILDOBJECT', THIS.GETOBJECTBYID)</b>
  </li>

  <br>

  <li>
    <b>THE MIDDLE-MAN SCHEMA WILL CONTAIN ONLY THE TWO LINKING ID'S, ALONG WITH A TIMESTAMP AND TWO VIRTUALS FOR EACH SCHEMA REF ID</b>
  </li>

   <li>
    <b>WRITE OUT THE SCHEMA IMPORTATION IN YOUR DBCONTEXT.JS</b>
  </li>

  <br>

  <li>
    <b>IN YOUR MIDDLE-MAN LAYER, ONCE YOUR CLIENT IS SPUN UP GRAB YOUR BEARER TOKEN AFTER BRINGING ALL OF YOUR ENVIRONMENT VARIABLES INTO POSTMAN FROM YOUR .ENV TO YOUR ENV.JS</b>
  </li>
  
  <br>

  <li>
    <b>INSERT BEARER TOKEN INTO YOUR AUTHORIZATION SECTION IN POSTMAN</b>
  </li>

  <br>

  <li>
    <b>TYPE MIDDLE-MAN OBJECT PATH INTO BASEURL "POST" SECTION</b>
  </li>
  
  <br>

   <li>
    <b>IN YOUR PERTAINING AREA TO DRAW YOUR OBJECT DEFINITION, COPY AND PASTE THE TWO OTHER CORRESPONDING ID'S INTO THEIR CORRESPONDING FIELDS. (FOR EXAMPLE; THE OBJECTID AND ACCOUNTID)</b>
  </li>

  <br>

  <li>
    <b>IF DESIGNATING THE ACCOUNT, YOU MUST GO INTO YOUR SCHEMA'S ASYNC CREATE FUNCTION, AND AS THE LAST PART OF YOUR CREATE FUNCTION, ADD "OBJECTDATA.ACCOUNTID = REQ.USERINFO.ID"!!!</b>
  </li>
  
  <br>

  <li>
    <b>ADD 2 AWAITS TO POPULATE THE OBJECTID AND THE ACCOUNT ID ENDED WITH THE METHOD ".POPULATE('OBJECTID')"</b>
  </li>

  <br>

  <li>
    <b>ONCE SUPPLYING ONE SIDE OF THE RELATIONSHIP, EXPECT TO HAVE TO RETURN THE OTHER SIDE WITH A .POPULATE()</b>
  </li>
  </ul>

  <br>

## <b><u>DAY 4</b></u> ##

  <br>

  <ul>
  <li>
    To add a collaborator to a repo: Go to Settings, collaborators and teams, button that says "add people", type github users name, click name, select member.
  </li>
  
  <br>

  <li>
    Create your object in your model
  </li>

  <br>

  <li>
    (enum: property lets you define multiple dimension sizes)
  </li>
  
  <br>

   <li>
    Timestamp the bottom of each model with a toJSON: {virtuals: true}
  </li>

  <br>

  <li>
    If a model is going to exist in mongo it needs a creatorId {type: Schema.Types.ObjectId, required: true, ref: account}
  </li>
  
  <br>

  <li>
    Remember the value of auth is your BEARER TOKEN in your key params in mongoDB
  </li>

  <br>

  <li>
    After "getting" your empty array, pass your .env file information from your server side folder to your env.js file on your client side folder
  </li>
  
  <br>

  <li>
    Remember to add your userInfo.id method to the top of your createObject function in your server controller!
  </li>
  
  <br>

   <li>
    After that, populate your createObject in service with await.newObject.populate('id', 'name picture')
  </li>

  <br>

  <li>
    Be sure to remember to add your own .env file info to your server folder once you have cloned down a project that you are collaborating on. You do not need to touch your env.js file.
  </li>
  
  <br>

  <li>
    Also, remember in your terminal in vscode to run npm i in your server folder to update everything you need to spin your server and get all your dependencies directed the way you need them to be
  </li>

  <br>

  <li>
    Once on the front-end, remember to <b>START YOUR CLIENT</b> in your debug section of vs code by switching it from spinning your server
  </li>
  
  <br>

  <li>
    Check ALL CONNECTIONS before you start writing any front-end code
  </li>
  
  <br>

   <li>
    <h3><b><u>STEPS (breaching back-end to front-end)</u></b></h3>
  </li>

  <br>

  <li>
    Start at router.js - examine the already posted values of current controllers that are drawn to the page
  </li>
  
  <br>

  <li>
    the ""router-view" in your index.html is the primary viewport. You can draw to the page from your router.js by using a method similar to grabbing a document by it's ID name. (e.g. view: routerView)
  </li>

  <br>

  <li>
    Comment out auth section
  </li>
  
  <br>

  <li>
    (Use unsplash website for a large library of HD quality images)
  </li>
  
  <br>

   <li>
    Make a new view:
    <br>
    Create a new "view" and copy/paste your html template into it's pertaining "view" folder, then mount and register your new view into your router.js folder
  </li>

  <br>

  <li>
    .unshift() method will insert an object to the BEGINNING of an array of objects
  </li>
  
  <br>

  <li>
    Remember that the middle-man schema is primarily only used for storing the ID's that are trying to cross-communicate to give us the ability to place properties from one ID type to the Other
  </li>

  <br>

  <li>
    <b>To grab an accurate count, after building out your virtual for counting in your schema, be sure to go to the proper service layer and .populate('targetId targetCount') then .sort('watcherCount')</b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

   <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

   <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

   <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

   <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

   <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

   <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>
  
  <br>

   <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

  <li>
    <b></b>
  </li>

  <br>

  <li>
    <b></b>
  </li>
  
  <br>

</ul>