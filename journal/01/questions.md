# Foundations of Web Development
01. In your own words, why do we use Git?
    > | To upload new repositories and connect with and view other users projects and profiles. |

02. In the terminal, what is the command `mkdir` used for?
    > | For creating new **directory folder.** As opposed to **touch** which simply creates a new file. |

03. What is a ***pseudo-class*** and what are some of the most common ones you think you will use?
    > | A pseudo class is essentially a "class within a class" that **styles an existing one** (e.g. :hover, :active, :disabled, etc.).
    <br>
    I foresee that we will most commonly be using the ?**":hover"** pseudo class; as it is activated consistently while browsing a webpage.  An example would include literally any time you are *hovering* over a *button* on most websites.  
    <br>
    Many will also have other elements with this pseudo class like; for instance, hovering over a *link* and/or *icon.* |

04. What is ***specificity*** and how might you use it to your benefit?
    > | It is viewed as the **"importance" of an element's class** by specifying a number value for said class of that element. If i remember correctly, ID's have a specificity of 100, classes are 10, and calling a literal tag "<></>" has a specificity of 1.
    <br>
    Whichever overruling class in specificity value will take priority on the class properties that are used to style that element. |

05. What problems do you think you could run into if you over-utilized the `!important` feature?
    > | You'd be **creating a series of class properties with extremely high specificity values**, which could in turn make your project difficult to apply further properties to, or other complications. |

06. What are the three components that makeup a `CSS` rule? <br> Example:

    ```css
        h1 {
            color: rgba(255, 210, 33, .75);
        }
    ```

    > | An **element** to call upon **(css, .css, #css, etc.)**, a **class name** given to said element to call a style property to **(h1)**, and a **styling property** for that class **(color).** |

07. How do you think good design influences people when visiting a website, and what sorts of things could you convey through design alone?
    > | Smoothly styled transitions, quick load times, appropriately chosen color scheme usage, properly placed animation sequences, etc. are the cornerstone of keeping someone on your site and interested. |
    <br>
    | **ALL** of these concepts can be achieved from design alone, and can make or break a successful website. Even down to the colors you use to convey your companies message effect this and must be carefully considered when designing anything in software development for the utmost success rate. |

08. What is the purpose of ***wireframing***?
    > | For creating a "visual blueprint" of sorts. A program used for designating an outline of the page you're building while creating a project page with code in another program. |

09. Do you think wireframes are worth the time, energy, and effort that they require? Why or Why not?
    > | **Absolutely.** I feel they are essential for keeping track of the layout you are building while simultaneously being an essential aide for project presentation before it is engineered. |

10. Define the display `:flex property:`
    > | "Flex" is what is used to place objects where you want on your page. Examples include the following with descriptions of their actions:
    <br>
    **flex-start:** flexes object to the left;
    <br>
    **flex-end:** flexes object to the right;
    <br>
    **flex-column:** flexes objects downward in the same column;
    <br>
    These are just a few of the many examples of a flex property. |

11. What `CSS` properties affect the size of a box model?
    > | Properties like **border-box, content-box, height, width** can all effect the size of the box model.  |
