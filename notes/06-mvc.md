# MVC

<h1><u>Model View Controller</u></h1>

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
    Inside the parenthesis located after the constructor is where you place curly brackets. <b>Inside those curly brackets further classify</b> what those <i>blueprint attributes would look like.</i>\

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
  this.name = walls
  this.emoji = floors
  this.rarity = windows
  this.skin = true
}
}

  new House({walls: 'plywood', floors: 'tile', windows: 'glass'})

  new House({walls: 'sheetrock', floors: 'wood', windows: 'stained glass'})
```

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

<h3><u>APP STATE EXPORTATION</u></h3>


<!-- does col and col-12 have differing attributes to how they effect your page? Some projects I've worked on will scrunch my row down slightly when i use col instead of col-12. But I have not ever noticed col-12 shrinking down. -->