# CSharp and SQL Fundamentals
01. What is the purpose of a `namespace`?

  > | It `organizes code` elements and `avoids naming conflicts` |

02. What is the difference between a `class` and an `interface`?

  > | A `class` is a `blueprint for creating objects.`
  An `interface defines a what classes can implement` under the parameters of specified methods. |

03. What is the method that returns an instance of a class, yet it has no return type?

  > | Constructor |

05. In the Car example what is the access modifier of the `Start()` method?

  ```c#
  abstract class Car
  {
    public string Start()
    {

      return "Vroooom";

    }
  }
  ```

  > | Visual answer provided below |
```c#
abstract class Car
{
    ⬇️⬇️⬇️
 ➡️ public ⬅️ string Start()
  { ⬆️⬆️⬆️

    return "Vroooom";

  }
}
```

06. In the Car example what is `string` an indication of?

  > | The `return type.` |

07. In the Car example what is `abstract` preventing?

  > | It `prevents the Car class` from being `instantiated` directly. |

08. In a SQL table, what is the difference between information in a row and information in a column?

  > | A `row` is an `instance of a record` and a `column` is a `property of a record.` |

09. Demonstrate the necessary SQL for creating a table called `characters` with the values `name, age, description` as strings, and an `int` id.

  > | Example Below: |
  ```sql
  CREATE TABLE characters (
  id INT,
  name VARCHAR(255) NOT NULL UNIQUE,
  age VARCHAR(100) NOT NULL,
  description VARCHAR(1000)
  ) default charset utf8 COMMENT '';

  FOREIGN KEY (id) REFERENCES characters(id) ON DELETE CASCADE
  ```

10. In SQL how can you query more than a single table? Provide an example.

  > | Example Below: |
  ```sql
  SELECT * FROM characters
  JOIN accounts ON characters.creatorId = accounts.id
  ```