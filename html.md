# HTML

The web is HTML is the web. Early versions of HTML (HyperText Markup Language) simply displayed text and links to other HTML pages (hence the name: "hyper"link), but the specification has evolved over time to incorporate images, audio, video, and many more interactive elements. Octopus Creative believes in clean HTML that's as easy to read as it is to write.

* Indent with tabs
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