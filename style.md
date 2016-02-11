# JavaScript

According to the great [Douglas Crockford](http://www.crockford.com/), JavaScript is the "[World's most misunderstood programming language](http://javascript.crockford.com/javascript.html)". Despite its many shortcomings, JavaScript has become one of the most — if not _the_ most — popular programming languages in the world, and is now widely used on both the client and server to help create great user experiences. At Octopus Creative, we harness the "good parts" of JavaScript to create concise, maintainable frontend (and sometimes backend) code.

* When possible (and sensible), write new JavaScript in CoffeeScript instead
* Libraries like jQuery are incredibly useful, but knowing how to write "raw" JavaScript is also incredibly important
* Indent with 2 spaces
* Use camelCase for variables (Constructor functions and CoffeeScript classes should be in PascalCase)
* Semicolons are **not** optional
* Understand the difference between `==` and `===`, and use them appropriately
* Use [IIFEs](http://benalman.com/news/2010/11/immediately-invoked-function-expression/) to help with scope, readability, and more
* Spaces, curlies and newlines for `if/else/while/try` are almost always **not** optional
  ``` javascript
  if (something) {
    // do stuff
  }

  for (var i = 0; i < 10; i++) {
    // loopy
  }

  // If you're simply returning (or similar), it's fine to do a compact `if`:
  if (error) return;

  if (error) throw new Error('Something went wrong');
  ```
* Declare and call functions like this (note argument, parentheses, and curly brace placement):
  ``` javascript
  function add(a, b) {
    return a + b;
  }

  add(2, 4);
  ```
* Keep variables in the proper scope (remember your `var` statements)
* "Private" variables should be prefixed with an underscore


# jQuery

* When writing selectors in jQuery (or plain JS, for that matter), use the fastest selector possible. A few basic guidelines:
  - `$('#id')` is faster than `$('div#id')`
  - `$('#id').find('.class')` is faster than `$('#id .class')`
  - Advanced selectors (`$('ul#stuff li.things:not(.other)[data-something="blah"]')`) are, in general, very slow. Avoid them when possible, and if you must use them, make sure they're cached.
* Cache your selectors
  ``` javascript
  // Do this
  var elements = $('.some-class');
  elements.doSomething();
  // …later
  elements.doSomethingElse();

  // Not this
  $('.some-class').doSomething();
  // …later
  $('.some-class').doSomethingElse();
  ```
* Don't use AJAX shortcut methods like `$.get` or `$.post`. Instead use `$.ajax` and provide both success **and** error handlers.
* Use `$('selector').on()`, **not** `$('selector').bind/delegate/live()`


# CoffeeScript

* Intent with two spaces

# CSS

Cascading Style Sheets (CSS) enable the beautiful internet you know and love; from simple things like text and background color, to advanced animations and WebGL filters. A simple, declarative language, CSS is a powerhouse; many preprocessors ([SASS](http://sass-lang.com/)) exist that help you write CSS better, faster, and DRYer. Octopus uses CSS (usually backed with SCSS) to make our applications and sites pixel-perfect and a joy to use.

* When at all possible, write new CSS in SCSS instead.
* Indent with 2 spaces.
* Selectors should not contain the tag name as well as any other information (i.e., `.something`, not `div.something`)
* Put a space after the `:` in rule declarations.
* Put a semicolon after every rule declaration.
* Put a space before the `{` after selectors.
* When possible, split your CSS out into files based on UI components, not pages. This helps keep things DRY, and generally reduces nested selectors.
* Do not nest scss selectors more than levels 3 deep.
* Rems are preferred over pixels (designer px / base font size = rem value).
* Use Autoprefixer to generate vendor prefixes based on the project-specific browser support that is needed.

# SCSS

* Prefer mixins to @extend.
* For a selector with no child selectors, its curly braces and rules should be on one line
  ``` scss
  p#whatever { color: #f00; font-size: 30px; font-weight: bold; }
  ```
* For a selector with child selectors, its opening curly brace should be on the same line as the selector, its rules should be on the line below, and its closing brace should be on its own line
  ``` scss
  .whatever {
    color: #f00;
    font-size: 1rem;

    .phone {
      color: #00f;
      font-style: italic;
    }
  }
  ```
* For selectors containing specifying selectors (`&`), the specifying selectors should come before any child selectors
  ``` scss
  .stuff {
    font-family: serif;

    &.things {
      font-family: monospace;
    }

    &:before {
      content: "hello!";
    }

    .things {
      font-family: "Proxima Nova", sans-serif;

      .highlight { color: #f00; }
    }
  }
  ```

# HTML

The web is HTML is the web. Early versions of HTML (HyperText Markup Language) simply displayed text and links to other HTML pages (hence the name: "hyper"link), but the specification has evolved over time to incorporate images, audio, video, and many more interactive elements. Octopus Creative believes in clean HTML that's as easy to read as it is to write.

* Indent with 2 spaces
* Indent all block-level elements
* Use semantic tags when possible, but make sure to check your use case if you're not sure it's the right tag (Things like menu, nav, figure, and cite have very specific semantic meanings that might surprise you)
* Text should not be be indented or on a new line inside, for example, a `p` tag, unless it has sibling nodes
  ``` html
  <p>Lorem ipsum dolor sit amet.</p>

  <p>
    <em>Something</em>
    Hello world!
  </p>
  ```


## Starter

``` html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <meta name="description" content="">
    <meta name="designer" content="Octopus Creative">
    <meta name="developer" content="Octopus Creative">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <!-- Add "maximum-scale=1" to fix the weird iOS auto-zoom bug on orientation changes. -->

    <title></title>

    <!--[if lt IE 9]>
      <script src="HTML5 SHIM"></script>
    <![endif]-->

    <link rel="shortcut icon" href="">
    <link rel="stylesheet" media="screen, projection" href="">

    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
  </head>

  <body>

  </body>
</html>
```
