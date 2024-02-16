## Combinator Cheat Sheet:
  - `+  -  Directly Adjacent Sibling` (div.class-one + div.class-two)
    ```html
    <div class="class-one">
    <div class="class-two"> <-- Directly Adjacent Sibling
    ```
  - `~  -  All Adjacent Siblings` (div.class-one ~ div.class-two)
    ```html
    <div class="class-one">
    ⋮
    <div class="class-two"> <-- All Adjacent Siblings (including this first one)
    ```

  - `>  -  Direct Child` (div.class-one > div.class-two)
    ```html
    <div class="class-one">
      <div class="class-two"> <-- Direct Child
    ```
  - `' ' (white-space)  -  Descendant` (div.class-one div.class-two)
    ```html
    <div class="class-one">
    …
    <div class="class-two"> <-- Descendant (Similar to '+', but doesn't have to be DIRECTLY adjacent)
    ```


  ## Nesting using the `&`, `>`, `~`, `*`, and `+` Combinators: 

  ### & - Reference to the parent selector when you are nesting your styles.
  ```css
  ⛔ Bad ⛔
  div.my-class {
    div:after {
      /...Styles... /
    }
  }
  ```
  ```html
  -- THE ABOVE WOULD TARGET THIS IN YOUR HTML --
  <div class="my-class">
    <div> <-- This div
  </div>
  ```
  ```css
  ✅ Good ✅
  div {
    &:after {
      /...Styles... /
    }
  }
  ```
  
  ```html
  -- THE ABOVE WOULD TARGET THIS IN YOUR HTML --
  <div class="my-class"> <-- This div
  </div>
  ```

  + #### Learn more: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors/Selectors_and_combinators

  ## Pseudo-Elements:

  ### `::before` and `::after` - **Basics**:

  > * *NOTE: Using either `:before` or `:after` instead of `::before` or `::after` is still acceptable and there is no difference in their effect. The double colon `::` was introduced in CSS3 to distinguish between pseudo-classes and pseudo-elements. However, `:before` and `:after` are still widely used and supported by all browsers, and there is a lot of developer preference on which to use. So there is no right or wrong answer here, the most important thing is to be consistent!*

  - `::before` - Adds content before the selected element.
    ```css
    div::before {
      content: "👈";
    }
    ```
    ```html
    <div> <-- On the `left side` of this div, placed before the content or behind the border 
    ```

  - `::after` - Adds content after the selected element.
    ```css
    div::after {
      content: "👉";
    }
    ```
    ```html
    <div> <-- On the `right side` of this div, placed after the content or in front of the border
    ```

  ### `::before` and `::after` - **Making Shapes in the image of the selected element**:

  - `::before` and `::after` can be used to create shapes that are the same size and shape as the selected element(set to 100% of its width and height), or they can be used to create shapes that are different from the selected element. This can be done by setting the `content` property to an empty string, and then using the `position` `width`, `height`, `border`, `border-radius`, `background`, and more to style the shape.
    ```css
    .selected-element {
      position: relative;
      height: 600px;
      width: 800px;
      background: lightgreen;
    }
    .my-class::before {
      content: "";
      position: absolute;
      top: 0; /* <-- Top edge of content to top edge of the selected element */
      left: 0; /* <-- Left edge of content to left edge of the selected element */
      width: 100%; /* <-- Make width 100% of the selected elements width */
      height: 100%; /* <-- Make height 100% of the selected elements height */
      background: #00000080;
    }
    ```
    >The above example would cover a light green rectangle with a semi-transparent black rectangle. This is one of many approaches that can be used to create a variety of shapes and effects. With a little creativity, the possibilities are endless! Some examples include:
        >- `adding gradients` to your background;
        >- using the `border` property to create triangles;
        >- `border-radius` to create circles;
        >- `transform` to `rotate or scale` the shape, and more!
    >> * ***HACK:** There is an easy way to create a reflection of an image by using a property known as `-webkit-box-reflect` which can be used to create a reflection of an image. The syntax is as follows:*
       ```css
        .shape {
          -webkit-box-reflect: below 0px #00000080;
          /* The first value is the direction of the reflection, and the second value is the offset of the reflection, so this would create a 'flipped' version of the shape below the original shape with a semi-transparent reflection. */
        }
      ```

  ### Paragraph and Heading Helpers - `::first-letter` and `::first-line`

  - `::first-letter` - Selects the first letter of the selected element. This can be used to style the first letter of a paragraph or heading, making it larger or a different color like in a book or magazine.
    ```css
    p.paragraph::first-letter {
      font-size: 2em;
      color: red;
    }
    ```
    ```html
    <p class="paragraph"> <-- The `first letter` of this paragraph will be larger and red
    ```
    - `::first-line` - Also good for styling the first line of a paragraph or heading, creating an indentation for proper formatting.
    ```css
    p.paragraph::first-line {
      text-indent: 2em;
    }
    ```
    ```html
    <p class="paragraph"> <-- The first line of the paragraph will be indented
    ```

    + #### Learn More:  https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements

  # Pseudo-Classes:

  - `:first-child` - Selects all elements that are the first child of their parent.
    ```css
    .parent:first-child {
      /...Styles... /
    }
    ```
    ```html
    <div class="parent">
      <div class="child"></div> <-- This div
      <div class="child"></div>
      <div class="child"></div>
    </div>
    ```

  - `:last-child` - Selects element that is the last child of their parent.
    ```css
    div.parent:last-child {
      /...Styles... /
    }
    ```
    ```html
    <div class="parent">
      <div class="child"></div>
      <div class="child"></div>
      <div class="child"></div> <-- This div
    </div>
    ```

  - `:nth-child()` - Selects all elements that are the nth-child of their parent. 'nth-child(number)' can be used to select specific elements. If no argument is given, it will select every child element.
    ```css
    div.parent:nth-child(2) {
      /...Styles... /
    }
    ```
    ```html
    <div class="parent">
      <div class="child"></div>
      <div class="child"></div> <-- This div
      <div class="child"></div>
    </div>
    ```

  - `:nth-of-type()` - Selects all elements that are the nth-child of their parent. 'nth-of-type(odd)' or 'nth-of-type(even)' can be used to select odd or even elements. If no argument is given, it will select every child element.
    ```css
    div.parent:nth-of-type(odd) {
      /...Styles... /
    }
    ```
    ```html
    <div class="parent">
      <div class="child"></div> <-- This div
      <div class="child"></div>
      <div class="child"></div> <-- This div
    </div>
    ```

  - `:empty` - Selects all elements that have no children.
      ```css
      div:empty {
        /...Styles... /
      }
      ```
      ```html
      <div class="parent">
        <div class="child"></div>
        <div class="child"></div>
        <div class="child"></div>
      </div>

      <div class="peace-and-quiet"></div> <-- This div
      ```

### `:not()`, `:has()`, and `:is()` - **Advanced Selectors**:
  - NOTE: These selectors can be used in combination with other selectors to create complex and specific styles. They can also be used to create styles that are more efficient and easier to read than using multiple selectors.

  - `:not()` - Selects all elements that do not match the given selector.
    ```css
    .house:not(.kitchen) {
      /*...Styles for the house that are not the kitchen...*/
    }
    ```
    ```html
    <div class="house">
      <div class="bedroom"></div> <-- This div
      <div class="bathroom"></div> <-- This div
      <div class="kitchen"></div>
      <div class="living-room"></div> <-- This div
    </div>
    ```

    + #### Learn more: https://css-tricks.com/css-not-with-multiple-classes/

  - `:has()` - Selects a parent element that `contain elements` that match the given selector.
    ```css
    .parent:has(.grand-child) {
      /...Styles... /
    }
    ```
    ```html
    <div class="parent">
      <div class="child"></div>
      <div class="child">
        <div class="grand-child"></div> <-- This div
      </div>
      <div class="child"></div>
    </div>
    ```
     + #### Learn more: https://css-tricks.com/the-css-has-selector/

  - `:is()` - Selects `elements that match any of the selectors listed`. This can make quick work of selecting specific elements `similar to the logic of preprocessor nesting.`
    ```css
    /* ✅ Less Code ✅ */
    div:is(.card-one, .card-two, .card-three) :is(.mdi, .sub-title) {
      /...Styles... /
    }
    /* ⛔ More Code ⛔ */
    div.card-one .sub-title, div.card-one .mdi, div.card-two .sub-title, div.card-two .mdi, div.card-three .sub-title, div.card-three .mdi {
      /...Styles... /
    }
    ```
    ```html
    <div class="card-one">
      <h5 class="card-header"></h5>
      <div class="sub-title"></div> <-- This div
      <div class="card-body">
        <div class="card-text"></div>
        <i class="mdi mdi-cat"></i> <-- This div
      </div>
    </div>
    <div class="card-two">
      <h5 class="card-header"></h5>
      <div class="sub-title"></div> <-- This div
      <div class="card-body">
        <div class="card-text"></div>
        <i class="mdi mdi-dog"></i> <-- This div
      </div>
    </div>
    <div class="card-three">
      <h5 class="card-header"></h5>
      <div class="sub-title"></div> <-- This div
      <div class="card-body">
        <div class="card-text"></div>
        <i class="mdi mdi-bird"></i> <-- This div
      </div>
    </div>
    ```
      + #### Learn more: https://css-tricks.com/is-is-useful/


  - `:placeholder-shown` - Selects input elements that are currently displaying placeholder text.
    ```css
      input.style-placeholder:placeholder-shown {
        /...Styles... /
      }
      ```
      ```html
      <input type="text" class="style-placeholder" placeholder="Placeholder Text"> <-- This inputs placeholder will be styled
      ```

  - `:checked` - Selects input elements that are checked.

    >**HINT:** You can also use this to `style elements that are NOT checked` by using `:not(:checked)` YOU CAN USE THE `:not()` SELECTOR ON ANY OF THE SELECTORS IN THIS CHEAT SHEET INCLUDING `:has()`. 
    ```css
    input.check-input:checked {
      background-color: green;
      color: white;
    }
    input.check-input:not(:checked) {
      background-color: red;
      color: white;
    }
    ```
    ```html
    <input type="checkbox" class="check-input" checked> <-- This input will be styled. If it is checked, the background will be green, if it is not checked, the background will be red.
    ```

  - `:disabled` - Selects input elements that are disabled.
    ```css
    input.disabled-input:disabled {
      background-color: red;
      color: #7f7f7f;
    }
    ```
    ```html
    <input type="text" class="disabled-input" disabled> <-- This input will be styled
    ```

  - `:focus` - Selects the element that has focus.
    > NOTE: Keep in mind although this is SIMILAR to the `:active` selector, but `:focus` is used for when the user clicks on an element, and `the style will remain until the user clicks on another element`.

    ```css
    button.focused-btn:focus {
      background-color: lightblue;
      color: white;
    }
    ```
    ```html
    <button class="focused-btn">Click Me</button> <-- Style will remain until the user clicks on another element
    ```

    - `:focus-within` - Selects the parent element that contains the element that has focus.
      > NOTE: Although this may seem similar to the `:focus` selector, `:focus-within` is used to select the parent element of the element that has focus, and the style will remain until the user clicks on another element. This is useful, for example, highlighting an entire `<form>` container when the user focuses on one of its `<input>` fields.
      ```css
      form.my-form {
        border: 1px solid;
        color: gray;
        padding: 4px;
        &:focus-within {
          background: #ff8;
          color: black;
        }
      }
      input {
        margin: 4px;
      }
      ```
      ```html
      <form class="my-form">
        <input type="text" placeholder="First Name">
        <input type="text" placeholder="Last Name">
        <input type="email" placeholder="Email">
        <input type="password" placeholder="Password">
      </form> <-- The entire form will be highlighted when the user focuses on any of its input fields
      ```



  ### Attribute Selectors:

   - `[attribute="value"]` - Selects all elements with the specified attribute and value.
      ```css
      input[type="checkbox"] {
        /...Styles... /
      }
      ```
      ```html
      <input type="checkbox"> <-- This input will be styled
      ```

  ### Miscellaneous Tips and Tricks:

  - You can utilize the `white-space` property to either force a line to have `multiple lines`, or to display as a `single line` of text.
    ```css
    .multi-line {
      white-space: pre-line;
      /* NOTE - `pre-line` value will collapse multiple spaces into a single space and will wrap the text to the next line when necessary. If no width is specified, it will wrap once it reaches the edge of the container. */
    }
    .single-line {
      white-space: nowrap;
      /* NOTE - `nowrap` value will force the text to display as a single line, and will not wrap to the next line. This is useful when you can't control the width of the container, and you want to ensure the text will not break to the next line or 'wrap' to the next line. */
    }
    ```
    ```html
    <div class="multi-line">This text will be displayed as multiple lines whenever the edge of the container is reached. Change the width of the multiline class selector to control when the line will break</div>
    <div class="single-line">This text will be displayed as a single line</div>
    ```

  
  - You can use the `attr()` function to `display the value of an attribute as content`. This can be useful for `displaying the value of an attribute as a pseudo-element`, as well.

    ```css
    [purse-thief]::before {
      content: attr(purse-thief) " ";
    }
    ```
    ```html
    <span purse-thief="That's my purse"> I don't know you!</span> <-- This would display on screen as "That's my purse I don't know you!"    
    ```

  - You can use the `content` property to `display an image as content` using the `url()` function. This can be useful for `displaying an image as a pseudo-element`, as well.

    ```css
    .image::before {
      content: url('https://bcw.blob.core.windows.net/public/img/7815839041305055');
    }
    ```
    ```html
    <div class="image"></div> <-- This would display on screen as the image below
    ```

  ### Styling `<select>` and `<option>` Elements:

  - Let's face it, targeting and styling the `<select>` and `<option>` elements can be a bit tricky. Here are a few tips and tricks to help you style these elements by showing you how to `target their specific selectors properties`:

    ### Selectors:

    - `border` and `outline`: You can use the `border` and `outline` properties to `style the border and outline of the select element`. This can be useful for `adding a border` and `removing the default outline` of the select element. This is a tried and true way to get rid of the default outline that is always added to the select element when it is clicked.

      ```css
      select {
        border: 1px solid #000;
        outline: none;
      }
      ```

    - `background`: You can use the `background` property to `style the background of the select element`. This `will not style the background of the options`, if you want both backgrounds to match, you have to `style the options separately`.

      ```css
      select {
        background: transparent;
        border: 1px solid #000;
        outline: none;
        option {
          background: transparent;
        }
      }
      ```
      ```html
      <select>
        <option value="1">Option 1</option>
        <option value="2">Option 2</option>
        <option value="3">Option 3</option>
      </select> <-- This would display on screen as the select element with transparent background with a 1px think border and no outline. The options would have a transparent background
      ```

    - You can use the `appearance` property to `style the appearance of the select element`. This can be useful for `hiding the default arrow` and `styling the select element` to match the rest of your site.

      ```css
      select {
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        padding: 8px 16px;
        border: 1px solid #000;
        background: #fff;
        color: #000;
        font-size: 1em;
        font-family: Arial, sans-serif;
      }
      ```