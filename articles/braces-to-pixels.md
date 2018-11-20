## Braces to Pixels

![Braces_to_Pixels](https://alistapart.com/d/braces-to-pixels/03_Braces_to_Pixels_8_2_696w.png "Braces_to_Pixels")
* Please refer to the [original article](https://alistapart.com/article/braces-to-pixels)

### Parsing
* Parse result
  * have a data structure with all the selectors, properties, and properties’ respective values
* Computation
  * any dimensional values are reduced to : auto, a percentage, or a pixel value 

### Cascade
* Specificity
  * determine which styles should apply to a given element by specificity
  * !important, style attribute, ID, class attribute, elements
* Origins
  * user, author and the user agent
* Doing the cascade
  * orgin, selector, property, name, value, specificity score, document order      
* CSS Object Model on DOM

### Layout
* Box tree
  * Formatting context
  * Containing block
  * Block direction 
* Resolving auto
* Dealing with float
* Understanding fragmentation

### Painting
* applied color, borders, shadows, and similar design treatments to the layout
* ultimately every layout element (even text) becomes an image
* Concerning the z-index
* Composition
  * create a layer, or layers, and render the bitmap(s) to the screen 

### Creating the illusion of interactivity
* The browser constantly tracks a variety of inputs, and while those inputs are moving it goes through a process called hit testing
