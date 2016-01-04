<h1>React Basics</h1>

<h2>Setup</h2>
For the purposes of this exercise, you'll only need one file, index.html. You'll set it up with the basic HTML boilerplate, but in the with a few new scripts loaded in the head, and an extra script section at the bottom. Here's what it should look like:

```
<!DOCTYPE html>
<html>
<head>

	<script src="https://fb.me/react-0.14.3.js"></script>
	<script src="https://fb.me/react-dom-0.14.3.js"></script>
	<script src="https://fb.me/JSXTransformer-0.12.2.js"></script>

	<title>My First React App</title>
</head>
<body>

</body>

<script type="text/jsx">

</script>

</html>
```

The three scripts we're loading are:
<ol><li><strong>React</strong>, which inserts the code you write;</li>
<li><strong>ReactDOM</strong>, which lets React navigate the DOM so it knows where to put that code; and</li>
<li><strong>JSX Transformer</strong>, which interprets JSX code.</li></ol>

JSX code is a way of inserting HTML into a page that's a lot easier than creating and appending an element with regular JavaScript. Here we're going to be inserting it directly into the page, enclosed in the `<script type="text/jsx"> </script>` tags. Normally you would OF COURSE separate this out from the HTML - in more advanced React apps, you definitely do - but for the purposes of this exercise, we're just going to cheat and include it here. :wink:

Here's a conceptual overview of how to build a basic React app. Don't worry if it doesn't make much sense; I'll be showing you the actual code in a moment. If you're familiar with Javascript, none of the code should look that weird to you.

<ul><li>React apps are built of snippets of code called <strong>components</strong>. Components can construct HTML elements as simple as a sentence, or as complicated as a Facebook user interface. (We're going to be sticking to the simpler elements here ... just so you keep your expectations reasonable!)</li>

<li>Components can make use of a list of <strong>properties</strong>, which are listed in a separately-instantiated object. (Technically these aren't necessary, but it would make for a really boring app.)</li>

<li>To use these components, you'll write a line of code instructing React to <strong>create your component</strong> as an element. That line will also link the component and the properties so that they can be rendered together.</li> 

<li>And you'll use another line of code to tell React <strong>where in the DOM</strong> to insert that element.</li></ul>

<h2>Code Structures</h2>
That all sounds great, but what does it actually look like? Let's make a super simple app called My Favorite Things. Here's the structure for a component, the snippets of code that create your app. You can go ahead and copy this (as well as the two chunks of code that follow) inside the `<script type="text/jsx"></script>` tags of your HTML.

```
var MyFavoriteThings = React.createClass({
	render: function() {
		// CODE GOES HERE
	}
});
```

.createClass is a method built into React that creates an object - hence the curly brackets. This object has one method called render. We'll define it later.

Next, we'll write an object that lists the component's properties might look something like this:

```
var favorites = {
	books: [{
		title: "Harry Potter",
		author: "JK Rowling",
		volumes: 7
	}, {
		title: "His Dark Materials",
		author: "Philip Pullman",
		volumes: 3
	}],
	shows: [{
		title: "Friday Night Lights",
		network: ["NBC", "DirecTV"],
		seasons: 5
	}, {	
		title: "Jessica Jones",
		network: "Netflix",
		seasons: 1
	]
};
```

This too is an object. It consists of two arrays, each of which contain two objects, each of which have three key-property values.

These next two lines are React-specific. Don't worry too much about their exact structure, just notice where variables are being repeated.

```
var element = React.createElement(MyFavoriteThings, favorites);
ReactDOM.render(element, document.querySelector(".react-element");
```

.createElement is another built-in React method. Its parameters are the code you want to render on this page and its relevant data. In this case, that's `MyFavoriteThings` and `favorites` - conveniently, the two objects we just built.

.render is a built-in ReactDOM method that takes two arguments: the element to be rendered onto the page, and the element it should be inserted into. The first argument is `element`, because that's the creative variable we assigned the React.createElement method to. The second argument is for the element with the class react-element - which we actually haven't included in our HTML! Let's do that.

Here's what your entire index.html file should look like now:

```
<!DOCTYPE html>
<html>
<head>

	<script src="https://fb.me/react-0.14.3.js"></script>
	<script src="https://fb.me/react-dom-0.14.3.js"></script>
	<script src="https://fb.me/JSXTransformer-0.12.2.js"></script>

	<title>My First React App</title>

</head>
<body>

	<div class="react-element"></div>

</body>

<script type="text/jsx">

	var MyFavoriteThings = React.createClass({
		render: function() {
			// CODE GOES HERE
		}
	});

	var favorites = {
		books: [{
			title: "Harry Potter",
			author: "JK Rowling",
			volumes: 7
		}, {
			title: "His Dark Materials",
			author: "Philip Pullman",
			volumes: 3
		}],
		shows: [{
			title: "Friday Night Lights",
			network: ["NBC", "DirecTV"],
			seasons: 5
		}, {	
			title: "Jessica Jones",
			network: "Netflix",
			seasons: 1
		]
	};

	var element = React.createElement(MyFavoriteThings, favorites);
	ReactDOM.render(element, document.querySelector(".react-element");

</script>

</html>
```

Everything look good? Cool - now let's write some JSX!

<h2>JSX</h2>

Like I said before, JSX is a way of inserting HTML into a page that's easier than doing it in regular Javascript. You don't have to use it with React, but it makes your life a lot easier. For example, here's an example of code you'd write to insert a new five-word paragraph with vanilla Javascript:

```
var newParagraph = document.createElement("p");
var paraText = document.createTextNode("I am a new paragraph.");
para.appendChild(paraText);

var body = document.getElementById("body");
body.appendChild(para);
```

... and here's that exact same code, in JSX.

```
var NewPara = React.createClass({
	render: function() {
		return <p>I am a new paragraph</p>
	{
});
```

A few things to notice:
<ul><li>the `var NewPara =` line is, essentially, the same as the `var MyFavoriteThings` line in our code.</li>
<li>The entire content of the `render` method is some HTML, prefaced by the command `return`.</li></ul>

You could make a much more elaborate element, with nesting HTML tags and IDs and classes. As you get into those more complex elements, however, there are two easy trip-ups to be aware of.

<ol><li>Every HTML tag <strong>must be explicitly closed</strong>. This means that self-closing tags, like images or line breaks, <strong>must</strong> include a forward slash before they close. So they'll look like `<img src="myImage.jpg" />` or `<br />`, NOT <img src="myImage.jpg"> or <br>.</li>
<li>You can include IDs or classes within any HTML element. But because React includes its own .createClass that does something pretty different than what regular HTML classes do, you need to <strong>designate classes with `className="box"`</strong> instead of `class="box"`. So a div element might look like `<div id="top" className="narrow">`. </li></ol>


	

(A [literal!] parenthetical on ReactDOM: older versions of React included the code that makes up the ReactDOM script, but now it's been separated out. So out in the wilds of the internet, you might see older code structured exactly like the ReactDOM.render line, except it says React.render. It's doing the same thing.)


It's sort of similar to Angular, and if you've had any experience with Node, you'll recognize some familiar structure. It was (at least originally) meant for building easily rendered user interfaces. One pro of React, in comparison to Angular, is that you can integrate it with any other technology or framework you want.
