# Async

### <u>PUT REQUESTS</u>

<ul>

  <li>
    <b>To import a second api,</b> go into your AxiosService and copy an instance of your current api, rename it as '_'api, and the interceptors api link to match the name of your new apis. <i></i>
  </li>

  <li>
    You <b>can dump or ignore the about link</b> if you do not need it. <i></i>
  </li>

  <li>
    The <b>first thing you want to do is build your controller.</b> That way you get  <i></i>
  </li>
  <ul>
    <li>
      If you <b>dump the about page and the home page in your router.js,</b> you can immediately start a <i>console.log() in your devTools console from your controller.</i> At that point you won't have to worry about route.js in this point of the cohort.
    </li>
    <li>
      <b>Build your async function</b> in your controller. <i></i>
    </li>
    <li>
      <b>Get your data to log from your service layer.</b> <i></i>
    </li>
    <li>
      <b>Once you have the results of your data,</b> send it to your AppState with "AppState.object" <i></i>
    </li>
  </ul>
  <li>
    <b>In your controller,</b> call AppState.On to the id of your object, and  _drawObject<i></i>
  </li>

  <li>
    <b>Build out your object layout in your HTML.</b> <i></i>
  </li>

  <li>
    <b>Once building out your model in the model layer,</b> you can use the .join() method to change the properties how you want them to be <i></i>
  </li>

  <li>
    <b>Clear out your imported properties as you assign them in your model. Be sure to match your left-hand argument to the value of your model requirements, and the right hand side to the value of the API properties you have loaded in.</b> <i></i>
  </li>

  <li>
    <b>In the service layer, set the active object to the AppState with the value of "new object". Then turn the AppState.on to listen for what you set.</b> <i></i>
  </li>

  <li>
    <b>Build your buttons in your Active model layer for basic page functionality.</b> <i></i>
  </li>

  <li>
    <b>Make your UserController for the active object and add your button onclick calls as a method in your constructor.</b> <i></i>
  </li>

  <li>
    <b>Go into your app.js to register your UserController.</b> <i></i>
  </li>

  <li>
    <b>Assign the UserController a UserService layer.</b> <i></i>
  </li>

  <li>
    <b>Retrieve the objects from the api with an async function for the user object in the controller layer for the user.</b> <i></i>
  </li>

  <li>
    <b>Do not try to load the User object on load. Call the AppState.on to first listen for the account id, then call for the user object that is now authorized via listening for the account id.</b> <i></i>
  </li>

  <li>
    <b>Use the .put() method to call the api in your service layer to toggle your object</b> <i></i>
  </li>

  <ul>
    <li>
      <b>You need to first go to your env.js file to import your Auth0 so you can assign your user login functionality.</b> <i></i>
    </li>
    <li>
      <b>Add your controller to your router. Wrap your controller name in an array e.g. [Controller, Controller, etc...] and get your first controller built</b> <i></i>
    </li>
    <li>
      <b>Access baseURL in your AxiosService.js by pasting the provided URL into your new baseURL.</b> <i></i>
    </li>
    <li>
      <b>Match the same name as a parameter and the parameter you want inside of your new "export const api" info in your AxiosService.js</b> <i></i>
    </li>
    <li>
      <b>Find and source the logged information of the date, explanation, title, and url for image to build inside your model. Copy and paste the information from your logged information into your code. Remove the info that you add into your model from the log info as you go.</b> <i></i>
    </li>
    <li>
      <b>Save the item into your AppState as multiple objects (array) or a single object (null).</b> <i></i>
    </li>
    <li>
      <b>If that object is an image or background, import it in by inserting this method into your first draw function (document.body.style.backgroundImage = (url name)).</b> <i></i>
    </li>
    <li>
      <b>Switch your appstate on to draw your image to your background</b> <i></i>
    </li>
    <li>
      <b>Build out a template in your html to put your other objects in your model on your page and flex them. Set your string interpolated items to the class and id name of their concurrent properties.</b> <i></i>
    </li>
    <li>
      <b>If you want a current date set the HTML tag's type name concurrently. If you want to target it later, give it a name and id that is concurrent to what you will call it as later in the MVC. Give it an onchange of what you will name your function.</b> <i></i>
    </li>
    <li>
      <b>While linking previous element's onchange to update it, set the query of "?object="</b> <i></i>
    </li>
    <li>
      <b></b> <i></i>
    </li>
  </ul>

  <li>
    <b>Always remember to add new controllers from your array into your router.</b> <i></i>
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

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

</ul>