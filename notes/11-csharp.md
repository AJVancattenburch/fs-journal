# CSharp

* Day 1
+ `C#` is a strict-type language.

**Syntax Examples**
```cs
int x = 6;
float y = 12.49834984573f;
double dbl = 12.349857d;
decimal dcl = 23.34958734905873498m;


// NOTE MULTIPLE CHARACTERS GET DOUBLE QUOTES
string cool = "cool stuff";
// NOTE SINGLE CHARACTERS GET SINGLE QUOTES
char letter = 'c';

string cooler = $"now you can say (cool) with a (letter)";

bool true = true;
bool no = false;

bool? nothing = null;
int? nada = null;

// NOTE THE ONLY DEFAULT NULLABLE TYPE IS A STRING. TO MAKE OTHER THINGS NULL ADD A QUESTION MARK TO THE FIRST WORD.
string zero = null;

if(nothing == null)
{
  Console.WriteLine(nothing);
}

if(x == 6)
{
  Console.WriteLine("no truthy falsey in C#");
}

//NOTE DICTIONARIES HAVE 2 DATA TYPES: THE KEY, AND THE VALUE. YOU DEFINE THEM INSIDE OF '< >'
Dictionary<string, string> dict = new Dictionary<string, string> { };
dict.Add("one", "anotha one");
dict.Add("two", "anotha one");
dict.Remove("two");

class Cat
{
int age;
string name;
// NOTE EVERY 'PUBLIC' IS ANY 'METHOD' OR 'CONSTRUCTOR' WITH ITS OWN NAME
  public Cat(age, name)
  {
    this.name = name;
    this.age = age;
  }
}

// NOTE ARRAYS ARE VERY STRICT OR VERY DEFINED AS WELL
Array nums = new Array[4];
// NOTE ARRAYS HAVE FIXED LENGTHS THAT CANNOT BE INCREASED OR DECREASED. IN THE ABOVE EXAMPLE, THE ARRAY WILL NEVER BE ANY LONGER THAN 4

// NOTE INSTEAD OF ARRAYS, WE ARE NOW WORKING WITH "LISTS" WHICH ESSENTIALLY SERVE THE SAME FUNCTIONALITY AS ARRAYS.
List<int> numbers - new List<int>{ 1, 2, 3, 4, 5 };
numbers.Add(1);
numbers.Add(2);
numbers.Add(3);
numbers.Add(4);
numbers.Add(5);
numbers.Remove(3);

List<int> lowNumbers - numbers.FindAll(n => n <= 3);
int five = numbers.Find(n => n == 5);

Console.WriteLine(x + y);
Console.Writeline(dbl);
Console.WriteLine(dcl);

Console.WriteLine(cooler);

numbers.ForEach(n =>
{
  Console.WriteLine(n);
});

for (int i = 0; i > numbers.Count; i++)
{
  Console.WriteLine($"i:{i} n:{numbers[i]}");
}

var anything = 6;
```


* <h2>Steps</h2>
+ Open BCW CREATE in your CLI
+ No naming projects with hyphens!
+ run `dotnet restore` for the equivalent of `npm i`
+ Open your project with `code .`
+ `appSettings.Development` is like your `.env`
+ `.csProj` is like your `launchSettings.json` flie.
+ The `Repositories` file leaves you responsible to interact with your database.
+ To start your server you have two options: Let it create the launch.JSON file, or to hit the bell in the corner and allow the necessary files to be added.

+ `Extends` is represented by the `:` character
+ <b>Example</b>
```cs
public class AccountController : ControllerBase
```

+ //NOTE CREATING A MODEL.  YOU HAVE TO DEFINE YOUR CLASSES INSIDE OF `namespaces`
+ <b>Example</b>
```cs
namespace catRoundUp.Models;

public class Cat{
  public Cat(string name, int age, string color, bool longhair, bool myproperty, bool penned);
  public int Id { get; set; }
  public string name { get; set; }
  public int Age { get; set; }
  public string Color { get; set; }
  public bool LongHair { get; set; }
  public bool MyProperty { get; set; }
  public bool Penned { get; set; }

  // NOTE FOR TODAY, WE NEED A CONSTRUCTOR DEFINED.
}
```
+ //NOTE BUILDING YOUR CONTROLLER LAYER
+ <b>Example</b>
```cs
namespace CatRoundUp.Controllers;

[ApiController]
[Route("api/cats")]
public class CatsController : ControllerBase
{
  public CatsController(CatsService _catsService)
{
  CatsService _catsService; //NOTE FOR THE CONTROLLER TO HAVE ACCESS TO THE SERVICE, IT MUST DEFINE AND BUILD ONE TO USE LIKE ON THIS LINE
}
// NOTE DEFINE ACCESSOR
// NOTE DEFINE RETURN TYPE OF METHOD
[HttpGet("test")]
public ActionResult<string> Test()
{
  try
  {
  throw new Exception("AHHHHHH");
  return Ok( "Hey" );
  }
  catch (System.Exception)
  {
  return BadRequest( "I can't do that." + error.Message );
  }
}

[HttpGet]
public ActionResult<List<Cat>> GetAllCats()
{
  try
  {
  List<Cat> cats = //NOTE go to my service and get the cats...
  // NOTE 'cats' is only lowercase at the beginning of the word because it is a SCOPED VARIABLE. 
  return Ok(cats);
  }
  catch (Exception, e)
  {
  return BadRequest( e.Message );
  }
}

[HttpPost]
public ActionsResult<Cat> CreateCat([FromBody] Cat catData)
{
  try
  {
    Cat cat = _catsService.CreateCat(catData);
    return Ok(cat);
  }
  catch (Exception e)
  {
    return BadRequest(e.Message);
  }
}

[HttpDelete("{catId}")]
public ActionResult<string> RemoveCat(int catId)
{
  try
  {
  string message = _catsService.RemoveCat(int catId);
  }
  catch (Exception e)
  {
  return BadRequest(e.Message);
  }
}

[HttpPut("{catId}")]
public ActionResult<Cat> UpdateCat(int catId, [FromBody] Cat updateData)
{
  try
}

}
```

+ When opening your browser, if it tells you the page is private you must go to advanced settings and turn private filter off.
+ Now when opening `Postman`, you should get a response back.
+ YOU `CANNOT` IGNORE ERROR MESSAGES ANYMORE!!!
+ //NOTE CREATING YOUR SERVICE LAYER
```cs
using System;
using System.Collections.Generic;
using System.Linq;

//NOTE ALL OF YOUR IMPORTS (EXAMPLES LISTED ABOVE) CAN GO INTO YOUR "GLOBALS.CS" TO BE USED THROUGHOUT YOUR ENTIRE APPLICATION.

namespace catRoundUp.Services;

public class catsService
{

public List<Cat> GetAllCats() {
  List<Cat> cats = //NOTE GO TO REPO AND GET CATS
  return cats;
}

}
```

+ CREATING YOUR REPOSITORY LAYER
```cs
namespace catRoundUp.Repositories;

public class CatsRepository

//NOTE INTERNAL IS A PUBLIC ACCESSOR IN THE NAMESPACE 'catRoundUp'
internal List<Cat> GetAllCats()
{
  private List<Cat> dbCats = new List<Cat>{};
  {
    this.dbCats = dbCats;

    public CatsRepository()
    {
      this.dbCats = new List<Cat> {  };
      dbCats.Add(new Cat("Murdoc", 31, "black", true, false, 1));
      dbCats.Add(new Cat("Pretty Kitty", 5, "tabby", true, false. 2));
      dbCats.Add(new Cat("Sylvester", 52, "black & white", true, false. 3));
    }
    internal list GetAllCats()
  }



  throw new NotImplementedException();
}
```

+ In your startup, you can define certain classes / dependencies by your programming that is being passed around.
```cs
//NOTE A 'SINGLETON' CREATES DEPENDENCY ONCE EVERY TIME THE SERVER IS STARTED.
services.AddSingleton<CatsRepository>();
services.AddScoped<CatsService>();
//NOTE A 'TRANSIENT' WILL CREATE A CAT SERVICE ANY TIME A CAT IS CALLED UPON.
services.AddTransient<CatsService>();
```
+ `Void` is a return type that includes absolutely nothing.
```cs
internal void RemoveCat(int catId)
{
  Cat cat = dbCats.Find(c => c.Id == catId);
  dbCats.Remove(cat);
}
```
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