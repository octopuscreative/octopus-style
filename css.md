# CSS

Cascading Style Sheets (CSS) enable the beautiful internet you know and love; from simple things like text and background color, to advanced animations and WebGL filters. A simple, declarative language, CSS is a powerhouse; many preprocessors ([LESS](http://lesscss.org/), [SASS](http://sass-lang.com/), [Roole](http://roole.org/), etc.) exist that help you write CSS better, faster, and DRYer. Octopus uses CSS (usually backed with SCSS) to make our applications and sites pixel-perfect and a joy to use.

* When at all possible, write new CSS in SCSS (or another preprocessor) instead.
* Even for static sites, better to use something like [Grind](https://github.com/paulstraw/grind) or [CodeKit](http://incident57.com/codekit/).
* Indent with tabs
* Selectors should contain the tag name as well as any other information (i.e., `div#something`, not `#something`)
* Put a space after the `:` in rule declarations
* Put a semicolon after every rule declaration
* Put a space before the `{` after selectors
* When possible, split your CSS out into files based on UI components, not pages. This helps keep things DRY, and generally reduces nested selectors
* Pixels are preferred over ems.
* The `.group` class in the CSS starter is really good. Use it.


# SCSS

* For a selector with no child selectors, its curly braces and rules should be on one line
	``` scss
	p#whatever { color: #f00; font-size: 30px; font-weight: bold; }
	```
* For a selector with child selectors, its opening curly brace should be on the same line as the selector, its rules should be on the line below, and its closing brace should be on its own line
	``` scss
	p#whatever {
		color: #f00; font-size: 18px; @include text-shadow(0 1px rgba(255, 255, 255, 0.3));

		span.phone { color: #00f; font-style: italic; }
	}
	```
* For selectors containing specifying selectors (`&`), the specifying selectors should come before any child selectors
	``` scss
	div.stuff {
		font-family: serif;

		&.things { font-family: monospace; }

		&:before { content: "hello!"; }

		div.things {
			font-family: "Proxima Nova", sans-serif;

			span { color: #f00; }
		}
	}
	```


## Starter

``` css
/* Reset + base: */
* { margin: 0; padding: 0; border: 0; -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }

html { overflow-y: scroll; } /* always show scrollbar in non-IE */

body, input, select, textarea, button { -webkit-font-smoothing: antialiased; text-rendering: optimizeLegibility; }

a { -webkit-tap-highlight-color: #FF5E99; }

::-moz-selection { background: #FF5E99; color: #fff; text-shadow: none; }
::selection { background: #FF5E99; color: #fff; text-shadow: none; }

img { -ms-interpolation-mode: bicubic; }
strong { font-weight: bold; }
em { font-style: italic; }

/* Clearfix: */
.group:after { content: "."; display: block; height: 0; clear: both; visibility: hidden; }
* html .group { height: 1%; } /* IE6 */
*:first-child+html .group { min-height: 1px; } /* IE7 */
/* End clearfix */
/* End reset + base */
```


# SCSS Mixins

``` scss
@mixin placeholder {
	&::-webkit-input-placeholder {
		@content;
	}
	&:-moz-placeholder {
		@content;
	}
	&::-moz-placeholder {
		@content;
	}
	&:-ms-input-placeholder {
		@content;
	}
}

@mixin max-width-media($width) {
	@media screen and (max-width: $width) {
		@content;
	}
}

@mixin retina-media() {
	@media (min--moz-device-pixel-ratio: 1.3), (-webkit-min-device-pixel-ratio: 1.3), (min-device-pixel-ratio: 1.3), (min-resolution: 1.3dppx) {
		@content;
	}
}

@mixin filter($properties) {
	-webkit-filter: $properties;
	-moz-filter: $properties;
	filter: $properties;
}

@mixin keyframes($name) {
	@-webkit-keyframes #{$name} {
		@content;
	}
	@-moz-keyframes #{$name} {
		@content;
	}
	@-ms-keyframes #{$name} {
		@content;
	}
	@keyframes #{$name} {
		@content;
	}
}

@mixin animation($name, $duration, $loop: infinite, $transition: linear, $direction: normal, $delay: 0s) {
	animation: $name $duration $loop $transition $direction;
	-ms-animation: $name $duration $loop $transition $direction;
	-moz-animation: $name $duration $loop $transition $direction;
	-webkit-animation: $name $duration $loop $transition $direction;

	animation-delay: $delay;
	-ms-animation-delay: $delay;
	-moz-animation-delay: $delay;
	-webkit-animation-delay: $delay;
}

@mixin text-shadow ($val1: none, $val2: none, $val3: none, $val4: none, $val5: none, $val6: none) {
	$val: $val1, $val2, $val3, $val4, $val5, $val6;

	@if $val6 == none {
		$val: $val1, $val2, $val3, $val4, $val6;
	}
	@if $val5 == none {
		$val: $val1, $val2, $val3, $val4;
	}
	@if $val4 == none {
		$val: $val1, $val2, $val3;
	}
	@if $val3 == none {
		$val: $val1, $val2;
	}
	@if $val2 == none {
		$val: $val1;
	}

	text-shadow: $val;
	-webkit-text-shadow: $val;
	-moz-text-shadow: $val;
	-o-text-shadow: $val;
}

@mixin appearance ($value: none) {
	appearance: $value;
	-moz-appearance: $value;
	-webkit-appearance: $value;
}

@mixin border-radius ($radius) {
	border-radius: $radius;
	-webkit-border-radius: $radius;
	-moz-border-radius: $radius;
	-o-border-radius: $radius;
}

@mixin background-clip ($clip) {
	background-clip: $clip !important;
	-webkit-background-clip: $clip !important;
	-moz-background-clip: $clip !important;
	-o-background-clip: $clip !important;
	-ms-background-clip: $clip !important;
}

@mixin box-sizing ($sizing: border-box) {
	box-sizing: $sizing;
	-webkit-box-sizing: $sizing;
	-moz-box-sizing: $sizing;
	-o-box-sizing: $sizing;
	-ms-box-sizing: $sizing;
}

@mixin box-shadow ($val1: none, $val2: none, $val3: none, $val4: none, $val5: none) {
	$val: $val1, $val2, $val3, $val4, $val5;

	@if $val5 == none {
		$val: $val1, $val2, $val3, $val4;
	}
	@if $val4 == none {
		$val: $val1, $val2, $val3;
	}
	@if $val3 == none {
		$val: $val1, $val2;
	}
	@if $val2 == none {
		$val: $val1;
	}

	box-shadow: $val;
	-webkit-box-shadow: $val;
	-moz-box-shadow: $val;
	-o-box-shadow: $val;
}

@mixin transition ($properties) {
	transition: $properties;
	-webkit-transition: $properties;
	-moz-transition: $properties;
	-o-transition: $properties;
	-ms-transition: $properties;
}

@mixin transform ($properties) {
	transform: $properties;
	-webkit-transform: $properties;
	-moz-transform: $properties;
	-o-transform: $properties;
	-ms-transform: $properties;
}

@mixin background-y ($top, $bottom, $fallback: transparent) {
	background-color: $fallback;
	background-image: -webkit-gradient(linear, left top, left bottom, from($top), to($bottom));
	background-image: -webkit-linear-gradient($top, $bottom);
	background-image: -moz-linear-gradient(center top, $top 0%, $bottom 100%);
	background-image: -moz-gradient(center top, $top 0%, $bottom 100%);
	background-image: -o-linear-gradient(top, $top 0%, $bottom 100%);
	background-image: -ms-linear-gradient(top, $top 0%, $bottom 100%);
}

@mixin background-y-image ($top, $bottom, $image, $fallback) {
	background-color: $fallback;
	background-image: $image;
	background-image: $image, -webkit-gradient(linear, left top, left bottom, from($top), to($bottom));
	background-image: $image, -webkit-linear-gradient($top, $bottom);
	background-image: $image, -moz-linear-gradient(center top, $top 0%, $bottom 100%);
	background-image: $image, -moz-gradient(center top, $top 0%, $bottom 100%);
	background-image: $image, -o-linear-gradient(top, $top 0%, $bottom 100%);
	background-image: $image, -ms-linear-gradient(top, $top 0%, $bottom 100%);
}

@mixin background-y-multi ($fallback: transparent, $val1: none, $val2: none, $val3: none, $val4: none, $val5: none) {
	$val: $val1, $val2, $val3, $val4, $val5;

	@if $val5 == none {
		$val: $val1, $val2, $val3, $val4;
	}
	@if $val4 == none {
		$val: $val1, $val2, $val3;
	}
	@if $val3 == none {
		$val: $val1, $val2;
	}
	@if $val2 == none {
		$val: $val1;
	}

	background: $fallback;
	background-image: -webkit-linear-gradient($val);
	background-image: -moz-linear-gradient(center top, $val);
	background-image: -moz-gradient(center top, $val);
	background-image: -o-linear-gradient(center top, $val);
	background-image: -ms-linear-gradient(center top, $val);
	background-image: linear-gradient(top, $val);
}

@mixin opacity ($opacity) {
	$ieval: $opacity * 100;

	zoom: 1;
	opacity: $opacity;
	-ms-filter:"progid:DXImageTransform.Microsoft.Alpha(Opacity=#{$ieval})";
	filter: alpha(opacity=$ieval);
}

@mixin user-select {
	-webkit-touch-callout: none;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
}
```
