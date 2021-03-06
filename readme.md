# General

* These are not to be blindly followed; strive to understand these and ask when in doubt.
* Don't duplicate the functionality of a built-in library.
* Don't swallow exceptions or "fail silently."
* Don't write code that guesses at future functionality.
* Don't commit commented out code unless there is a specific reason to.

# Linting

* All projects should be linted via gulp or an equivelent build tool to ensure code quality and that all code adheres to Octopus' code style guidelines. For convenience we've provided our linter configs for various linters. As another convenience we've included our preferred gulp setup [here](https://github.com/octopuscreative/gulp-util) if you're looking for somewhere to start.

# Git

* Once a project has been established, prefer [GitHub Flow](https://guides.github.com/introduction/flow/).

# JavaScript

* When possible (and sensible), write new JavaScript in CoffeeScript instead.
* Libraries like jQuery are incredibly useful, but knowing how to write "raw" JavaScript is also incredibly important.
* Indent with 2 spaces.
* Use camelCase for variables (Constructor functions and CoffeeScript classes should be in PascalCase).
* Use single quotes for strings except to avoid escaping.
* Commas should have a space after them.
* Always handle the err function parameter.
* Multiple blank lines not allowed.
* Understand the difference between `==` and `===`, and use them appropriately.
* Use [IIFEs](http://benalman.com/news/2010/11/immediately-invoked-function-expression/) to help with scope, readability, and more.
* Avoid binding to the same class in both your CSS and JavaScript.
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
* Take advice from http://ricostacruz.com/rsjs

# Vue.js

* 1 component per file.
* Order: Props, Data, Computed, Events, Methods, Lifecycle (Compiled, ready, etc), Template.
* Prefer using $broadcast/$dispatch to exposing methods that other components might talk to.
* As much as you can avoid two way binding.
* As much as you can keep shared state in one place (usually the Vue instance).
* When pre-registering data (data: -> thing: '') use the same type that will be used with real data. I.e don't use null values because that can cause problems in IE.
* Don't include large bits of vue markup in a page's html, but instead move into the component's template.
* Don't use `<template>` inside of `<select>` elements to build options lists, lest your select break in IE.

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
* Prefer CoffeeScript [comprehensions](https://coffeescript-cookbook.github.io/chapters/arrays/list-comprehensions) over regular for loops
* Take advice from https://coffeescript-cookbook.github.io

# Ruby

* Indent with two spaces.
* Single emptyline between method definitions 
* Methods should not be more than 6-ish lines each. (break long methods into new methods)
* Classes should have few public methods
* Each object should be limited in what it knows about other objects. user.profile (good) user.profile.links (bad)

# Rails

* Controllers should not manipulate objects that are persisted.

```ruby
#bad
user.role = 'buyer'
user.save!
```

```ruby
#better
user.make_buyer!.save
```

* Erb should only contain view layer code and should not trigger any new sql queries 
* Controllers should rarely have methods outside the standard rest methods. 

# CSS

* Consider [Expressive CSS](http://johnpolacek.github.io/expressive-css/)
* When possible (and sensible), write new CSS in SCSS instead.
* Use soft tabs (2 spaces) for indentation.
* Prefer dashes over camelCasing in class names.
* Do not use ID selectors.
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace { in rule declarations.
* In properties, put a space after, but not before, the : character.
* Put closing braces } of rule declarations on a new line.
* Put blank lines between rule declarations.
* Use Autoprefixer to generate vendor prefixes based on the project-specific browser support that is needed.
* Rems are preferred over pixels (desired px / base font size = rem value).
* Avoid binding to the same class in both your CSS and JavaScript.

# SCSS

* Prefer mixins to @extend.
* Take advice from http://rscss.io
* Do not nest scss selectors more than levels 3 deep.
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

      .highlight {
        color: #f00;
      }
    }
  }
  ```

# HTML

* Indent with 2 spaces
* Indent all block-level elements
* Use semantic tags when possible, but make sure to check your use case if you're not sure it's the right tag (Things like menu, nav, figure, and cite have very specific semantic meanings that might surprise you).
* Use `<button>` tags over `<a>` tags for actions.
* Text should not be be indented or on a new line inside, for example, a `p` tag, unless it has sibling nodes.
  ``` html
  <p>Lorem ipsum dolor sit amet.</p>

  <p>
    <em>Something</em>
    Hello world!
  </p>
  ```
