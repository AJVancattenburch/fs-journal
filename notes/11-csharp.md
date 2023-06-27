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
<br> <br>

* <h1><u>Day 2</u></h1>
  <b><h2>SQL</h2></b>
+ SQL, or `Structured Query Language`, is a language designed to allow both technical and non-technical users `query, manipulate, and transform data from a relational database.`
+ Due to its simplicity, SQL databases provide `safe and scalable storage` for millions of websites and mobile applications.
+ SQL has to be executed in order to be read.
+ To `execute` SQL, hover over the `query` and hit the `play` button.
+ One of the only things you will get back is a `number` that represents the `number of rows that were affected by the query.`
+ To insert `values` into a table, you must define the `columns` that you are inserting into.

+ ***Example:***
```sql
CREATE TABLE penguins
(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name TEXT NOT NULL,
  age INT DEFAULT 1,
  SPECIES TEXT,
  wearingTuxedo BOOLEAN DEFAULT true
);

INSERT INTO penguins 
(name, age, species)
VALUES
('Penny', 2, 'Macaroni');

INSERT INTO penguins
(name, species)
VALUES
('Rocky', 'Southern Rockhopper');

--NOTE: this example below will not work because the default value for age is 1, and we are not defining it.
INSERT INTO penguins 
(species)
VALUES
('Stinky');

INSERT INTO penguins
(name, wearingTuxedo)
VALUES
('Sloopy', false);
```

+ To `update` a table, you must define the `column` you are updating, and the `value` you are updating it to.
+ `TEXT` is shorthand for `VARCHAR(255)`, which is the maximum number of characters that can be stored in that column.
+ You can `increase the number of characters` that can be stored in a column, but you cannot `decrease` it.
+ If you want to use more `characters` for something like a description, for example, you can use `TEXT` instead of `VARCHAR(255)` or increase the varchar number to something like `VARCHAR(5000)`.
+ To select all information from `penguins`, you can use the `*` character.
+ Example:
```sql
SELECT * FROM penguins;
```
+ For only specific column information, you can use the column name and species like so.
+ Example:
```sql
SELECT name, species FROM penguins;
```
+ To grab information from specific penguins, you can use the `WHERE` clause.
+ Example:
```sql
SELECT * FROM penguins WHERE id = 1;
```
+ To select multiple specific penguins between an array of ID'S, you can use the `FROM` or `WHERE` clause in seperate cases like so:
+ Examples:
```sql
SELECT * FROM penguins FROM id = 1, 2, 3;
SELECT * FROM penguins WHERE id > 1 AND id < 4;
```
+ There is also a `LIKE, NOT LIKE, and IN` clause that can be used to select specific information. You can access them like this:
+ Examples:
```sql
SELECT * FROM penguins
WHERE name LIKE 'P%';
SELECT * FROM penguins
WHERE name NOT LIKE 'P%';
SELECT * FROM penguins
WHERE name IN ('Penny', 'Rocky');
```
+ To update your table, you can use the `UPDATE` clause.
+ Example:
```sql
UPDATE penguins SET
 `wearingTuxedo` = false 
WHERE id = 4;
```
+ To delete a specific penguin, you can use the `DELETE` clause.
+ Example:
```sql
DELETE FROM penguins
WHERE id = 3;
```
+ Moving on from penguins, lets try and `create some cars.`
+ Example:
```sql
CREATE TABLE cars
(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  make VARCHAR(100) NOT NULL,
  model VARCHAR(100) NOT NULL,
  year INT NOT NULL DEFAULT 1990,
  price DOUBLE NOT NULL DEFAULT 1.00,
  color VARCHAR(100) NOT NULL,
  description TEXT NOT NULL,
  mileage INT NOT NULL,
  isManual BOOLEAN NOT NULL DEFAULT true
  createdAt DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT 'Time Created',
  updatedAt DATETIME ON UPDATE CURRENT_TIMESTAMP COMMENT 'Time Updated',
) default charset utf8 COMMENT '';

INSERT INTO cars
(make, model, year, price, color, description, mileage, isManual)
VALUES
( 'Ford',
  'Mustang',
  1967,
  100000.00,
  'red',
  'This is a classic car.',
  100000,
  false
);

INSERT INTO cars
(make, model, year, price, color, description, mileage, isManual)
VALUES
( 'Chevy',
  'Camaro',
  2018,
  40000.00,
  'blue',
  'This is a classic car but at the same time it is not.',
  100000,
  false
);

INSERT INTO cars
(make, model, year, price, color, description, mileage, isManual)
VALUES
( 'Dodge',
  'Challenger',
  2020,
  100000.00,
  'green',
  'This is an awesome car.',
  100000,
  false
);
```
+ `To sort` this example by the time that it was updated at, you can do so like this:
+ Example:
```sql
SELECT * FROM cars
ORDER BY `createdAt` DESC;
```
+ To `add a filter` to this example, you can do so like this:
+ Example:
```sql
SELECT * FROM cars
WHERE price > 50000
ORDER BY `createdAt` DESC;
```
+ To `limit` the amount of information that is returned in this example, you can do so by using an `offset.`
+ To use an  `offset` in this example, you can do so like this:
+ Example:
```sql
SELECT * FROM cars
WHERE price > 50000
ORDER BY `createdAt` DESC
LIMIT 1 OFFSET 1;
```
+ A great website to source all the information on SQL and it's commands is `mysqltutorial.org`
+ To fill out your auth qualifications, you can do so like this in your `appsettings.json` file that looks like the below example.
+ Example:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*",
  "CONNECTION_STRING": "server=localhost;port=3306;database=catRoundUp;user=root;password=;Convert Zero Datetime=True",
  "AUTH0_DOMAIN": "dev-8q9q9q9q.us.auth0.com",
  "AUTH0_AUDIENCE": "https://localhost:5001",
}

```
+ To start a new database from scalegrid.io, you can do so by going to the website and creating a new database.
+ You can find your `connection string` by going to your database and clicking on the `connect` button.
+ To connect your database to your application, you can do so by going to your `appsettings.json` file and adding the `connection string` to the file.
+ Your `host` is your `master` connection endpoint.
+ Your `username` is your `user` connection endpoint.
+ Your `database` is your `database` connection endpoint.
+ Copy and paste these values into your `SQL` tab in vscode and hit the `play` button to execute the query.
+ Insert these values into your `appsettings.json` file into your `CONNECTION_STRING` like so:
+ Example:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*",
  "CONNECTION_STRING": "server=;port=;database=;id=;password=;Convert Zero Datetime=True",
  "AUTH0_DOMAIN": "dev-8q9q9q9q.us.auth0.com",
  "AUTH0_AUDIENCE": "https://localhost:5001",
}

```
+ `Zero Datetime` is a setting that allows you to use `0000-00-00 00:00:00` as a value in your database.
+ You need to make sure you are connected to the database by opening the query tabat the bottom of your screen and hitting the `play` button.
+ Once you are connected, you can use C# to `query` your database.
+ **<h2>You can start by creating a `model` for your database for your list of cars.**</h2>
+ Example:
```cs
namespace sharpList.Models;

public class Car
{
  public int Id { get; set; }
  public string Make { get; set; }
  public string Model { get; set; }
  public int Year { get; set; }
  public double Price { get; set; }
  public string Color { get; set; }
  public string Description { get; set; }
  public int Mileage { get; set; }
  public bool IsManual { get; set; }
  public DateTime CreatedAt { get; set; }
  public DateTime UpdatedAt { get; set; }
}
```

+ **<h2>Next, you can go onto `building out your controller.`**</h2>
+ Example:
```cs
namespace sharpList.Controllers;

[ApiController]
[Route("api/cars")]

public class CarsController : ControllerBase
{
  private readonly CarsService _carsService;

  public CarsController(CarsService carsService)
  {
    _carsService = carsService;
  }

  [HttpGet]
  public ActionResult<List<Car>> GetAllCars()
  {
    try
    {
      List<Car> cars = _carsService.GetAllCars();
      return Ok(cars);
    }
    catch (Exception e)
    {
      return BadRequest(e.Message);
    }
  }

  [HttpGet("{carId}")]
  public ActionResult<Car> GetCarById(int carId)
  {
    try
    {
      Car car = _carsService.GetCarById(carId);
      return Ok(car);
    }
    catch (Exception e)
    {
      return BadRequest(e.Message);
    }
  }

  [HttpPost]
  public ActionResult<Car> CreateCar([FromBody] Car carData)
  {
    try
    {
      Car car = _carsService.CreateCar(carData);
      return Ok(car);
    }
    catch (Exception e)
    {
      return BadRequest(e.Message);
    }
  }

  [HttpPut("{carId}")]
  public ActionResult<Car> UpdateCar(int carId, [FromBody] Car updateData)
  {
    try
    {
      updateData.Id = carId;
      Car car = _carsService.UpdateCar(carId, updateData);
      return Ok(car);
    }
    catch (Exception e)
    {
      return BadRequest(e.Message);
    }
  }

  [HttpDelete("{carId}")]
  public ActionResult<string> RemoveCar(int carId)
  {
    try
    {
      string message = _carsService.RemoveCar(carId);
      return Ok(message);
    }
    catch (Exception e)
    {
      return BadRequest(e.Message);
    }
  }
}
```

+ **<h2>Next, you can go on creating your `repository` for your cars.**</h2>
+ Example:
```cs
namespace sharpList.Repositories;

public class CarsRepository
{
  private readonly IDbConnection _db;

  public CarsRepository(IDbConnection db)
  {
    _db = db;
  }

  internal List<Car> GetAllCars()
  {
    string sql = "SELECT * FROM cars ORDER BY createdAt DESC;";
    List<Car> cars = _db.Query<Car>(sql).ToList();
    return cars;
  }

  internal Car GetCarById(int carId)
  {
    string sql = "SELECT * FROM cars WHERE id = @carId;";
    Car car = _db.Query<Car>(sql, new { carId }).firstOrDefault();
    List <Car> cars = _db.Query<Car>(sql).ToList();
    return car;
  }

  internal Car CreateCar(Car carData)
  {
    string sql = @"
    INSERT INTO cars
    (make, model, year, price, color, description, mileage, isManual)
    VALUES
    (@Make, @Model, @Year, @Price, @Color, @Description, @Mileage, @IsManual);
    SELECT LAST_INSERT_ID();";
    Car car = _db.Query<Car>(sql, carData);
    // int id = _db.ExecuteScalar<int>(sql, carData);
    carData.Id = id;
    return carData;
  }
```
+ You can add your `SELECT` statement to your `dbSetup.sql` file like so:
```sql
SELECT * FROM cars
WHERE id = LAST_INSERT_ID();
``` 
+ Continuing on with Example...
```cs
  internal Car UpdateCar(Car car)
  {
    string sql = @"
    UPDATE cars
    SET
      make = @Make,
      model = @Model,
      year = @Year,
      price = @Price,
      color = @Color,
      description = @Description,
      mileage = @Mileage,
      isManual = @IsManual
    WHERE id = @Id;";
    _db.Execute(sql, car);
    return car;
  }

  internal int DeleteCar(int carId)
  {
    string sql = "DELETE FROM cars WHERE id = @carId LIMIT 1;";
    int rows = _db.Execute(sql, new { carId });
    return rows;
  }
}
```

+ `Remember to go into your startup.cs file` and add the following code to your `ConfigureServices` method.
+ Example:
```cs
services.AddScoped<CarsRepository>();
services.AddScoped<CarsService>();
```

+ **<h2>Next, you can create your `service layer` for your cars.**</h2>
+ Example:
```cs
namespace sharpList.Services;

public class CarsService
{
  private readonly CarsRepository _carsRepository;

  public CarsService(CarsRepository carsRepository)
  {
    _carsRepository = carsRepository;
  }

  internal List<Car> GetAllCars()
  {
    return _repo.GetAllCars();
  }

  internal Car GetCarById(int carId)
  {
    Car car = _repo.GetCarById(carId);
    if (car == null)
    {
      throw new Exception("Invalid Id");
    }
    return car;
  }

  internal Car CreateCar(Car carData)
  {
    Car car = _repo.CreateCar(carData);
    return car;
  }

  internal Car UpdateCar(int carId, Car updateData)
  {
    Car original = getCarById(updateData.Id);
    car.Make = updateData.Make != null ? updateData.Make : original.Make;
    car.Model = updateData.Model != null ? updateData.Model : original.Model;
    car.Year = updateData.Year != null ? updateData.Year : original.Year;
    car.Price = updateData.Price != null ? updateData.Price : original.Price;
    car.Color = updateData.Color != null ? updateData.Color : original.Color;
    car.Description = updateData.Description != null ? updateData.Description : original.Description;
    car.Mileage = updateData.Mileage != null ? updateData.Mileage : original.Mileage;
    car.IsManual = updateData.IsManual != null ? updateData.IsManual : original.IsManual;
    _repo.UpdateCar(original);
    return original;
  }

  internal Car DeleteCar(int carId)
  {
    Car car = GetCarById(carId);
    //TODO check if you are authorized to do this!
    int rows = _repo.DeleteCar(carId);
    if (rows > 1) throw new Exception("Something has gone terribly wrong. Multiple vehicles has been deleted!");
    return car;
  }
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
* <h2>Steps to integrate SQL into your <u><b>SharpList</b></u></h2>
+ 
+ 
+ 
+ 
+ 
+ 