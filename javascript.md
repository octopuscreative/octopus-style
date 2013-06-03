# JavaScript

According to the great [Douglas Crockford](http://www.crockford.com/), JavaScript is the "[World's most misunderstood programming language](http://javascript.crockford.com/javascript.html)". Despite its many shortcomings, JavaScript has become one of the most — if not _the_ most — popular programming languages in the world, and is now widely used on both the client and server to help create great user experiences. At Octopus Creative, we harness the "good parts" of JavaScript to create concise, maintainable frontend (and sometimes backend) code.

* When possible (and sensible), write new JavaScript in CoffeeScript instead
* Libraries like jQuery are incredibly useful, but knowing how to write "raw" JavaScript is also incredibly important
* Indent with tabs
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
* When instantiating multiple variables at once, use this format:
	``` javascript
	var foo = 'a',
		bar = 'b',
		baz = [
			1,
			2,
			3
		],
		qux = {
			a: 'b',
			b: 'c',
			c: 'd',
		},
		zoobie;
	```
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

* Intent with soft tabs, two spaces