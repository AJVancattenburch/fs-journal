# A bit more CSharp and SQL
1. What does ***inheritance*** accomplish for us in C#?

  > | ANSWER HERE |

2. How does ***member inheritance*** work in C#? Does a `Class` inherit all members of the base `Class`?

  > | ANSWER HERE |

3. How does ***accessibility*** affect inheritance?

  > | ANSWER HERE |

4. What is the difference between a `PRIMARY KEY` and a `FOREIGN KEY`

  > | ANSWER HERE |

5. What is an ***alias***?

  > | ANSWER HERE |

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

  > | ANSWER HERE |
