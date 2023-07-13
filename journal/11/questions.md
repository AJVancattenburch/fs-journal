# A bit more CSharp and SQL
1. What does ***inheritance*** accomplish for us in C#?

  > | It enables us to `create a class(es) off of an instance of a class that already exists.` | <br>
      Example: 
  ```cs
    class User {
      public string Name { get; set; }
      public string Email { get; set; }
      public string Password { get; set; }
    }

    class GithubProject : User {
      public string RepoName { get; set; }
      public string RepoUrl { get; set; }
    }
  ```
  <br>

2. How does ***member inheritance*** work in C#? Does a `Class` inherit all members of the base `Class`?

  > | It is when a `Class` inherits all of the members of the base `Class`. |

3. How does ***accessibility*** affect inheritance?

  > | It determines whether classes can access the members `of the base class`. `public` and  `private` are examples of instances of accessibility after inheritance. |

4. What is the difference between a `PRIMARY KEY` and a `FOREIGN KEY`

  > | A `PRIMARY KEY` is the `unique id` of a table, while a `FOREIGN KEY` is `referenced` in another table to `create a relationship` between tables. |

5. What is an ***alias***?

  > | An `alias` is a `temporary name` for a `table` or `column` in a `database`. |
    Example of `acts` being an alias for `accounts`:
  ```SQL
    SELECT
    acts.*
    FROM accounts acts
    WHERE acts.id = LAST_INSERT_ID();
  ```
  <br>

6. Demonstrate how you would query a join statement that would get all of a doctors patients from the following collections:

  ```SQL
  CREATE TABLE doctors (
    id INT NOT NULL AUTO_INCREMENT,
    -- CODE OMITTED
    PRIMARY KEY (id)
  )

  CREATE TABLE patients (
    id INT NOT NULL AUTO_INCREMENT,
    -- CODE OMITTED
    PRIMARY KEY (id)
  )

  CREATE TABLE patient_doctors (
    id INT NOT NULL AUTO_INCREMENT,
    doctorId INT NOT NULL,
    patientId INT NOT NULL,

    FOREIGN KEY (doctorId)
      REFERENCES doctors(id),
    FOREIGN KEY (patientId)
      REFERENCES patients(id),
  )

  ```

  > | 
  ```SQL
    SELECT
    pats.*
    docs.*
    FROM patients
    JOIN doctors ON docs.id = pats.doctorId
    WHERE pats.doctorId = @doctorId;
  ```
    |
