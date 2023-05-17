# MVC

<h1>
  <u>
    Model View Controller
<br>
    <b>Week 1</b>
  </u>
</h1>

## <b><u>DAY 1</u></b>

## Figma Visual Explanation


  "![Alt text](MVCS%20Diagram.png)" 
<br><br>
<ul>

  <li>
    <b>View</b> is what the user sees and experiences.
  </li>
  <li>
    <b>Service</b> Model is responsible for your business logic. In the sense that it calculates the <i>actions</i> that the user enacts with the controller. It is the "meat and potatoes" of almost every application.
  </li>
  <li>
    Try not to worry too much about the <i>"inner guts"</i> of provided code while utilizing MVC.  Focus more on the way your organization is implemented.
  </li>
  <li>
    The <b>observer pattern</b> is not MVC. It is part of the design pattern to help to understand how the app state will actually work.
  </li>
  <li>
    The <b>constructor</b> is responsible for building things for the <b>controller</b>. It is a special function used for <i>instantiating</i> a class or an instance of a class.
  </li>

  <li>
    The "data" or <i>raw material</i> of the <b>constructor</b> gets passed like a function parameter to create classes it's properties for you.
  </li>
  <li>
    The hotkey <b>/**</b> when creating a constructor will automatically fill out the <i>data fields</i> for you that is to be passed through the constructor.
  </li>
  <li>
    <b>"this."</b> essentially stands for <i>"this thing this time around</i>
  </li>
  <li>
    If you are styling the inside of a class, <b>let or const</b> does not need to be used to establish values.
  </li>
  <li>
    The <b>"new"</b> property assignment is reserved for class styling.
  </li>
  <li>
    In the <b>controller, any declaration written above the constructor</b> is considered "private" until it is invoked either within or below the constructor.
  </li>
  
  <br>

  <li>
    The <b>constructor</b> is always called upon when any class is being invoked with <i>new properties.</i>
  </li>

  <br>

  <li>
    It is <b>never</b> the job of the <b>controller to modify data. It is highly unrecommended.</b> <i></i>
  </li>

  <li>
    The <b>singleton pattern</b> means that there is <i>only one</i> heroes service.
  </li>

  <li>
    The <b>appstate.emit('string')</b> works like a forEach in combination with an addEventListener() when you need to find the properties of all <i>'string'</i> objects in an array.
  </li>
<br>

## <b><u>DAY 2</u></b>


  <li>
    There is <b>no need to make files and folders for each project while using MVC opened with the bcw create command in the command prompt.</b> Just go  <i></i>
  </li>

  <li>
    <b>ALWAYS start at the model at the beginning of an MVC project.</b> It is the foundation of the way you're <i>application will look as a "model".</i>
  </li>

  <li>
    The name of your file should <b>match the name of your class</b> that you are <i>creating in your file.</i>
  </li>

  <li>
    If you are going to pull references into other files elsewhere in your project,  <b>make sure you add an "export file"</b> before <i>defining it.</i>
  </li>

  <li>
    Creating attributes for an object in your model is similar to <b>creating a class</b> in <i>CSS.</i>
  </li>

  <li>
    Any time you want to build or instantiate a class, you're creating a <b>blueprint</b> of what it will look like in the <i>model in your bottom defining curly brackets.</i>
  </li>

  <li>
    Inside the parenthesis located after the constructor is where you place curly brackets. <b>Inside those curly brackets further classify</b> what those <i>blueprint attributes would look like.</i>

<br><br>


<h4><b>Example 1:</b></h4>

<br>

```js
export class House {

constructor(walls, floor, windows) {
  this.walls = walls
  this.floor = floors
  this.windows = windows
  this.crownMolding = true
  this.lightbulbs = 0
}
}

  new House({walls: 'plywood', floors: 'tile', windows: 'glass'})

  new House({walls: 'sheetrock', floors: 'wood', windows: 'stained glass'})
```

<br><br>


<h4><b>Example 2:</b></h4>

<br>

```js
export class Gachamon {

constructor(name, emoji, rarity, skin) {
  this.name = gachamon.name
  this.emoji = gachamon.emoji
  this.rarity = gachamon.rarity
  this.skin = ''
}
}

  new House({walls: 'plywood', floors: 'tile', windows: 'glass'})

  new House({walls: 'sheetrock', floors: 'wood', windows: 'stained glass'})
```

<br><br>

  </li>

  <li>
    After we are done defining what the class will look like in the <b>model</b>, we <b>go to the AppState to store them, and then define their properties and values.</b>
    <br>
    It is the <i>window</i> between your HTML (the user) and the rest of your JavaScript.
  </li>

<h4><b>Example 2:</b></h4>

<br>

```js
gachamon = [
  new Gachamon ({name: gachamon.name, emoji: gachamon.emoji,  rarity: gachamon.rarity})
]
```

<br>

  <li>
    To handle <b>default values,</b> we use symbols like <b>''</b> or <b>||</b> <i></i>
  </li>

  <li>
    Whenever we want to change, alter or manipulate the stored data in the AppState, we move to the <b>Service</b> layer in MVC. <i></i>
  </li>

  <li>
    The first thing we do in service is <b>single instance for a single need in a given class.</b> After that, we move to the <b>controller,</b> which handles inputs.
    <br>
    <i>The filter layer between the users and the rest of your application code.</i>
  </li>

  <li>
    Anything the user will interact with will be handled from <b>the controller</b> layer. <i></i>
  </li>
  <br><br>

  ```js
export class GachamonController {
  constructor() {
    console.log('hello from the gachamon controller')
  }
}
```
<br><br>

  <li>
    If you want to draw something form the <b>console to the page,</b> you do so in the <i>index.html</i> and then make your template in your <b>model</b> layer.
  </li>
  <br><br>

```js
getListTemplate( {
  return `
  whatever you have as your   html.index template goes here`
})
```
  <li>
    Any time you want to manipulate or change what the user sees (DOM), <b>that will happen in the controller.</b>
    <br>
    (e.g. when you draw something to the page). <i></i>
  </li>

  <li>
    When you want your object to be drawn to the console, you do so in the <b>controller</b> layer. <i></i>
  </li>

  <br><br>
```js
function _drawGachemon() {
  let gachamon = appState.gachamon
  let template =''
  template
  gachamon.forEach(g => template+= g.template)
  //NOTE - this does the same thing as 'document.getElementById, second argument is the actual HTML//
  setHTML ('gachamon', template)
}
```

  <li>
    "Private" functions are being written in the controller, they get an <b>underscore between the word "function" and the name it is given,</b> like in the example above. <i></i>
  </li>

  <li>
    <b>Encapsulation</b> is what you hide from the user in your code in an additional layer. We only call them within a method with a single instance. This is to protect the developer application code. <i></i>
  </li>

  <li>
    Clicking on a piece of code then using the hotkey <b>Ctrl + .</b> will copy/paste that code into another selected layer of the <i>MVC.</i>
  </li>

  <li>
    Use the <b>appState.on</b> method when you want to <i>change anything that is not being shown to the user by grabbing those appState.on values from the controller layer.</i>
  </li>

  <li>
    Typically; to get a new element or object to draw to the user screen, move about a new user interactive element's addition in this order on MVC if you aren't creating your already working on a project:
    <br><br>
    <b>Controller, service, appState; controller, appState (for initial console.log);
    <br><br>
    index.html, controller, service, appState (to further add functionality to first console.log);
    <br><br>
    controller again to pull values from appState(to draw in console.log what you want to appear later on screen);
    <br><br>
    controller.</b>
     </br> <i></i>
  </li>

  <li>
    The <b>setHTML(object, MVC layer location)</b> and <b>setText(object, MVC layer location)</b> methods are the same as using <b>innerHTML</b> or <b>innerText</b> (respectively) as you would writing a simple 3 document HTML, JS, CSS document <b>while writing code in MVC.</b> <i></i>
  </li>

  <li>
    <b>appState.emit</b> triggers a function that <i>appState.on</i> is calling for.
  </li>

  <li>
    <b>saveState(banana word, load request)</b> is what saves information like "JSON.stringify()" from the MVC.
    <br>
    The first argument is a "banana" word and the second argument is what you want to load from your local storage.<i></i>
  </li>

  <li>
    <b>loadState(load request, the type you want it changed into)</b> is what loads information like "JSON.parse()" from the MVC.
    <br>
    The first argument is the name of the collection that you would like to load, and the second argument is what you want that element to change into. <i></i>
  </li>
  <br><br>

## <b><u>DAY 1</u></b>

  <br><br>

  <li>
    The <b>.slice()</b> method is used to show what you would like to see in your displayed document. <i></i>
  </li>

  <li>
    Take the <b>body</b> and turn it into an array of individual words by using <b>.split()</b> method by taking those words and putting them into their own individual array. <i></i>
  </li>

  <li>
    The <b>.map()</b> method looks at and "transforms" the entirety of what it is functioned to look at inside of it's parenthesis into whatever you direct it to transform.<i></i>
  </li>

  <li>
    The <b>.join()</b> method is used to do the opposite of what <i>.split()</i> does.
  </li>

  <li>
    The <b>.focus()</b> method is used to direct your cursor to the method or function that is is called in.  <i></i>
  </li>

  <li>
    The <b>onblur=""</b> event saves your text when you click out of a text area. <i></i>
  </li>

<br>
<h2><b><u>Week 2</u></b></h2>
<br>
<h3><b><u>Day 2 - Sandbox APIs</u></b></h3>
<br>

  <li>
    <b>To find the data sitting in each sandbox API,</b> you add the path to the end of the URL where you obtain the example. (e.g. sondbox.codeworksacademy.com/car) <i></i>
  </li>

  <li>
    When you hit the "login" button, it logs you into the sandbox API and gives you a large key.<b></b> <i></i>
  </li>

  <li>
    If you paste said key into <b>jwt.io,</b> it will give you information about the key you obtained in the sandbox, which has your login information. <i></i>
  </li>

  <li>
    <b>You can then move to codeworksclassroom.auth0?</b> <i></i>
  </li>

  <li>
    <b>Select the auth option when creating project in bcw create on the command line.</b> <i></i>
  </li>

  <li>
    <b>***<u>STEPS TO TODAYS LAB PROJECT</u>***</b> <i></i>
  </li>

  <li>
    New folders in the auth files are <b>env.js (loads environment for application) and router.js () </b> <i></i>
  </li>

  <li>
    <b>You can delete the footer in your HTML.</b> <i></i>
  </li>

  <li>
    <b>Copy/paste: domain, audience and clientId from your env.js for the value of your sandbox API auth0 settings @ export const baseURL.</b> <i></i>
  </li>

  <li>
    <b>change baseURL from the localhost to classroom sandbox URL in the env.js file.</b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b>Click login to get same login screen.</b> <i></i>
  </li>

  <li>
    <b>Logging in at this point plugs in your auth0 settings info but you can log in as anyone.</b> <i></i>
  </li>

  <li>
    <b>Set account equal to null on appstate with @type parameter.</b> <i></i>
  </li>

  <br>*********

  <li>
    <b>router.js has a Path and a Controller.</b> <i></i>
  </li>

  <li>
    <b>Tells you which controller to use. Does not say "new controller". Use whichever one aligns with the "href" in your HTML document.</b> <i></i>
  </li>

  <li>
    <b>When setting up new "#/yourPath" links, be sure to link them to the proper controller.</b> <i></i>
  </li>

  <li>
    <b>Once you get to service, create an async function that connects to your API with the "let res=" function.</b> <i></i>
  </li>

  <li>
    <b>Write the same function as an async function under your export class carsController</b> <i></i>
  </li>

  <li>
    <b>From service layer, give your API function something to call on in your Model layer by constructing your export class object in that Model layer.</b> <i></i>
  </li>

  <li>
    <b>If a property of an object is not required you may have to write a default method in it's function.</b> <i></i>
  </li>

  <li>
    <b>Create the "get" template for your API in your Model layer. (e.g. get carCard(){return `template info`})</b> <i></i>
  </li>

  <li>
    <b>appstate.object = res.data.map(o => )... under your template.</b> <i></i>
  </li>

  <li>
    <b>go into appstate and set object = [] and it's required @param type.</b> <i></i>
  </li>

  <li>
    <b>Make a template for that object in your controller layer.</b> <i></i>
  </li>

  <li>
    <b>Do this with let template='', then a forEach statement for it being equal to the template, then setting the HTML, and finally going into your constructor and turning the appstate.on on to listen to your object in your template, and setting the setHTML() method as the first method under your constructor. This last step should draw the object to your page.</b> <i></i>
  </li>

  <li>
    <b>Be sure to remember to set the "name" and "id" of your HTML tag that is to be set to the same name of the object property (e.g. ${this.id} etc.).</b> <i></i>
  </li>

  <li>
    <b>Continue by setting the HTML under the setHTML for your object template so it also appears in your template to the "id" location.  The second argument is where you want it to be placed with the syntax "Object.ObjectForm".</b> <i></i>
  </li>

  <li>
    <b>If using a modal, remember to set "data-bs-toggle" to "id of object" and "data-bs-target" to the id name as well, but with a "#" in front of it to signify that it is the "id name". If it's a canvas, the "data-bs-target" location changes from the top of the modal to wherever the offcanvas is going to slide open from.</b> <i></i>
  </li>

  <li>
    <b>Make it so the modal or offcanvas only opens on it's respective page by creating a button to open it only in the instance of the page it's located on by creating a button on the page the modal of offcanvas is on specifically. Then set the button to the same ID as the setHTML, and as the location paste the #/pageName that you want it to be in.</b> <i></i>
  </li>

  <li>
    <b>After you set that HTML, set another HTML with the same ID under the template in your model where you do not want it to appear.</b> <i></i>
  </li>

  <li>
    <b>Set your appstate.on with the argument as the currently logged in account, with the second argument as drawing the button, then pasting that setHTML info into your function for drawing a button.</b> <i></i>
  </li>

  <li>
    <b>Set an if statement to appstate.account as the conditional underneath your command to setHTML.</b> <i></i>
  </li>

  <li>
    <b>Any time you ever set up an async function, always use the "try catch" method within it first and set the bottom argument as pop.error(error)</b> <i></i>
  </li>

  <li>
    <b>When building the form, be sure to await the service.createobject.</b> <i></i>
  </li>

  <li>
    <b>Now in service, put the function into the server from your service with the "res" function with const res = await api.post('api/object', formData). Be sure to console.log('banana', res.data)</b> <i></i>
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
    <b>Auth Token is the users access token.</b> <i></i>
  </li>

  <br><br>
  


  <br>

</ul>

<i></i>

<b></b>

<i></i>

<b></b>

<i></i>

<ul>
  <li>
    <ul>
      <li></li>
    </ul>
  </li>
</ul>

### CONSTRUCTOR SAMPLE BEFORE IT IS EXPORTED TO THE APP STATE

<br>

```js

@param {{id: string, name: string, picture: string, health: number, level: number}}

  constructor(data) {
    this.id = data.id || generateId()
    this.name = data.name
    this.picture = data.picture
    this.health = data.health
    this.level = data.level
  }
```

## <b><u>DAY 2</u></b>

  <li>
    <b>data-bs-toggle data-bs-target</b> are (sequentially) like an "event" and "target" that you set to the same name as your modal "id".<i></i>
  </li>

  <li>
    Inside the <b>"modal content"</b> is where you can set sizing properties for the chosen modal.<i></i>
  </li>

  <li>
     Inside the <b>"modal dialogue"</b> is what is actually displayed in the modal. <i></i>
  </li>

  <li>
    <b>Rows</b> are typically your parent container that you will leave in your index.html when you cut and paste your html template into the controller. <i></i>
  </li>

  <li>
    <b>"Static"</b> (rather than get or set) does <i>not</i> "get" or "set" but in the sense that it stays the way it is.  To change something in the "static" you need to set a parameter for it.
  </li>

  <li>
    Using the keyword <b>"new"</b> is what is referred to as instantiation. You are instantiating a new value to a pre-existing class. <i></i>
  </li>

  <li>
    The <b>value</b> is what a user actually puts into an input. <i></i>
  </li>

  <li>
    The <b>name=""</b> attribute in HTML is pulled from the classes "left hand" property argument. <i>(e.g. this.name= and this.price=);</i> "name" and "price" are the values that get pulled from the "name=" attribute.
  </li>

  <li>
    In order to clear a form, we use the <b>boostrap.Modal.getOrCreateInstance(#modal).hide()</b> method. <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>

  <li>
    <b></b> <i></i>
  </li>