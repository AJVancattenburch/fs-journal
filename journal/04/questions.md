# Understanding Asynchronous Code, and API's
01. What is the difference between `asynchronous` code and `synchronous` code?

  > | `synchronous` code happens immediately and simultaneously, while `asynchronous` code waits on `listeners` to fire an `event` that triggers it. |

02. What is an event listener?

  > | An event that triggers on `asynchronous functions.`
  <br>  
  (e.g. using appState.on( '', ) to fire an event that is listening for an asynchronous function). |

03. What does *REST* stand for, and in simple terms what does it mean??

  > | It's what processes like `get, post, put,` and `delete` do to instantiate a class. |

04. What is a callback / higher order function?

  > | A callback is what you call within an asynchronous function to handle said functions completion.  |

05. What is a `promise`? How do you capture an error from a `promise`?

  > | It essentially means that either something happens, or it doesn't. And if it doesn't - to fire another event in it's place. |

06. Name three processes used to make requests over `HTTP`?

  > | `get, post,` and `put`. |

07. What does the `API` acronym stand for?

  > | Application Programming Interface |

08. What must you do in order to `await` a promise inside of a function?

  > | You must call it within an `asynchronous function` immediately after initiating it.
  <br>
  <b>Example:</b>
  <br>
  ```js
  async doThis(thing)
    try {
      await thatService.doThis(thing);
    } catch (error) {
        Pop.error(error)
  
    }
  ```
|

09. What is the purpose of encapsulation in programming?

  > | It is the process of packing data, functions, and methods that instantiate a class into a single object. |

10. What is `HTTP` response code for a successful request?

  > | It is when an the server successful receives information and in response fires the requested action (Response code 200). |

11. What is a 400 error?

  > | It is a "bad request" when information is not accepted by the server due to improper syntax or missing information. |
