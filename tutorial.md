<h1>React Basics</h1>

<h3>Setup</h3>
For the purposes of this exercise, you'll only need one file, index.html. You'll set it up with the basic HTML boilerplate, but in the with a few new scripts loaded in the head, and an extra script section at the bottom. Here's what it should look like:

```html
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

* React apps are built of snippets of code called <strong>components</strong>. Components can construct HTML elements as simple as a sentence, or as complicated as a Facebook user interface. (We're going to be sticking to the simpler elements here ... just so you keep your expectations reasonable!)

* Components can make use of a list of <strong>properties</strong>, which are listed in a separately-instantiated object. (Technically these aren't necessary, but it would make for a really boring app.)

* To use these components, you'll write a line of code instructing React to <strong>create your component</strong> as an element. That line will also link the component and the properties so that they can be rendered together.

* And you'll use another line of code to tell React <strong>where in the DOM</strong> to insert that element.

<h3>Code Structures</h3>
That all sounds great, but what does it actually look like? Let's make a super simple app called My Favorite Things. Here's the structure for a component, the snippets of code that create your app. You can go ahead and copy this (as well as the two chunks of code that follow) inside the `<script type="text/jsx"></script>` tags of your HTML.

```jsx
var AFavoriteThing = React.createClass({
	render: function() {
		// CODE GOES HERE
	}
});
```

.createClass is a method built into React that creates an object - hence the curly brackets. This object has one method called render. We'll define it later.

Next, we'll write an object that lists the component's properties:

```jsx
var favorites = {
	books: [{
		title: "Harry Potter",
		author: "JK Rowling",
		volumes: 7
	}, {
		title: "His Dark Materials",
		author: "Philip Pullman",
		volumes: 3
	}]
};
```

This object consists of one array of two objects, each of which have three key-property pairs.

These next two lines have two more built-in methods that come with React and ReactDOM, respectively. Notice where variables are being repeated.

```jsx
var element = React.createElement(AFavoriteThing, favorites);
ReactDOM.render(element, document.querySelector(".react-element"));
```

.createElement's parameters are the code you want to render on this page and its relevant data. In this case, that's `AFavoriteThing` and `favorites` - conveniently, the two objects we just built.

.render takes two arguments: the element to be rendered onto the page, and the element it should be inserted into. The first argument is `element`, because that's the creative variable we assigned the React.createElement method to. The second argument is for the element with the class react-element - which we actually haven't included in our HTML! 

Let's do that, and take a look at our file thus far:

```html
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

	var AFavoriteThing = React.createClass({
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
		}]
	};

	var element = React.createElement(AFavoriteThing, favorites);
	ReactDOM.render(element, document.querySelector(".react-element"));

</script>

</html>
```

Everything look good? Cool - now let's write some JSX!

<h3>JSX</h3>

Like I said before, JSX is a way of inserting HTML into a page that's easier than doing it in regular Javascript. You don't have to use it with React, but it makes your life a lot easier. For example, here's an example of code you'd write to insert a new five-word paragraph with vanilla Javascript:

```javascript
var newParagraph = document.createElement("p");
var paraText = document.createTextNode("I am a new paragraph.");
newParagraph.appendChild(paraText);

var body = document.getElementById("body");
body.appendChild(newParagraph);
```

... and here's that exact same code, in JSX.

```jsx
var NewPara = React.createClass({
	render: function() {
		return <p>I am a new paragraph</p>
	{
});
```

A few things to notice:

* the `var NewPara =` line is, essentially, the same as the `var AFavoriteThing` line in our code.
* The entire content of the `render` method is some HTML, prefaced by the command `return`.

You could make a much more elaborate element, with nesting HTML tags and IDs and classes. As you get into those more complex elements, however, there are two easy trip-ups to be aware of.

* Every HTML tag <strong>must be explicitly closed</strong>. This means that self-closing tags, like images or line breaks, <strong>must</strong> include a forward slash before they close. So they'll look like `<img src="myImage.jpg" />` or `<br />`, NOT `<img src="myImage.jpg">` or `<br>`.

* You can include IDs or classes within any HTML element. But because React includes its own .createClass that does something pretty different than what regular HTML classes do, you need to <strong>designate classes with `className="box"`</strong> instead of `class="box"`. So a div element might look like `<div id="top" className="narrow">`.

* Whatever element directly follows `return` has to enclose <strong>all the HTML</strong> that you're returning. So if you have a component with an h1 and a p element, you should enclose it all within a `<div>`. (Remind you of anything? Maybe another front-end framework that rhymes with "pangular"??)


If you copy and paste that `return <p>I am a new paragraph</p>` into your AFavoriteThing render function, save it, and open index.html in your browser, you'll see it - as you might expect - rendered in the browser. Cool!

What would be cooler is if we could use React to do something other than write HTML in a really complex way. Luckily, we can.

<h3>Properties</h3>

Earlier, I said that React components can make use of properties. In ths app, our properties are stored as an object in the variable `favorites`, and linked them to the component we're creating in the line `var element = React.createElement(AFavoriteThing, favorites);
`. So how do we get to them?

React objects - remember, our component is technically an object - come with a handy property called, originally, `.props`. We can attach it to `this` (so that it knows which object's properties it's looking for - in future projects, you could have many different components). From there, you know how to grab a particular value from an object - something like `this.props.books[0].title` is one way to do it.

But how do you get an HTML element to return a value you've grabbed via Javascript? {Curly braces, that's how!}

Try this:

```jsx
var AFavoriteThing = React.createClass({
	render: function() {
		return <div>
			<h1>{this.props.books[0].title}</h1>
			<h2>{this.props.books[0].volumes} books by {this.props.books[0].author}</h2>
		</div>
	}
});
```

When we need to access properties within some HTML we're returning, all you need to do is wrap them in a single set of curly brackets.

<h4>Looping Through Properties</h4>

OK, so we can display properties through their index number. We should be able to display them all by looping through them, right?

We're going to create a new component to do this. This new component will be a list of ALL of our favorite things, not just one. Let's call it ListOfThings. Inside ListOfThings, the component AFavoriteThing will display once for every object in our data. Here's how we do this:

```jsx
var ListOfThings = React.createClass({
	render: function() {
		var list = this.props.books.map(function(favoriteProps){
			return <AFavoriteThing {...favoriteProps} />
		});

		return <div>
			{list}
		</div>
	}
});
```

The third line, where `var list` is first defined, should be familiar. We're iterating through `this.props.books`, and mapping the values to a function. That function is where things get a little complicated.

* We're calling the properties that we're iterating through `favoriteProps` (this could be anything, as long as you're consistent and name it the same thing on the next line).
* We're returning what looks like a made-up element: `<AFavoriteThing />`. What we're really returning, though, is <em>an instance of the </em><strong>component</strong> called AFavoriteThing - one for each instance (in this case, book) of `this.props.books` in our data.
* Inside of `<AFavoriteThing />`, we're including this this weird-looking `{...favoriteProps}` line. This is because we're iterating through this.props.books within ListOfThings, and in order to render its component, AFavoriteThing needs to be able to access the properties ListOfThings is generating. By including `{...favoriteProps}`, we're passing all of these properties to AFavoriteThing.
 * You could pass each property individually, but that's pretty tedious. This `{...var}` structure gives you a shortcut.

There's two final things you should do for this mapping function to work. 

1. Since we're now accessing the properties defined in our `favorites` object in ListOfThings, not AFavoriteThing, we need to change `var element = React.createElement(AFavoriteThing, favorites);` to `var element = React.createElement(ListOfThings, favorites);`. Remember, whenever AFavoriteThings needs to use the data from `favorites`, we've instructed ListOfThings to give it to them, with the `<AFavoriteThing / {...favoriteProps>` code.

2. We need to update AFavoriteThing so that we can reuse it for every book in our data. We don't want it to just generate Harry Potter data every time. So make sure it includes this code:

```jsx
var AFavoriteThing = React.createClass({
	render: function() {
		return <div className="thing">
			<h1>{this.props.title}</h1>
			<h2>{this.props.volumes} books by {this.props.author}</h2>
		</div>
	}
});
```

Each time ListOfThings generates an AFavoriteThing component while iterating through our data, it will replace `{this.props.title}` et. al. with the title, number of volumes, and books for the relevant item.

<h3>States</h3>

You might expect React to be somewhat, well, reactive. It is! That's where states come in. States are a property of any React component, and they're accessed via `this.state`. You can set states to show or hide an element, display an element in a different style - basically any manipulation you can do in regular Javascript. And states can have multiple properties, so you might have a `this.state.show_div` state with its own possible options, as well as a `this.state.style' state with others.

We're going to set up an extremely simple (and pretty pointless) style state, but it will familiarize you with the general structure of states. Our state is going to toggle the color of our text when we click a button.

If this were a regular Javascript function we were writing, we'd set a toggling onClick event to change the font to red when we clicked our button, and then back to black when we clicked it again. That's honestly not that different from what we'll do here.

Our button will live within the ListOfThings object. It will listen for a click, and when it hears it, it will run a method called handleClick to decide what to do. Here's what our button looks like:

```jsx
return <div>
	{list}
	<button onClick={this.handleClick}>Toggle State</button>
</div>
```

Now, let's define the handleClick method. Before the render method in ListOfThings, make sure the following code is included. It's a simple toggle function that decides what to set `this.state.style` to, depending on what that value currently is. 

```jsx
var ListOfThings = React.createClass({
	handleClick: function() {
		if (this.state.style === "colorful") {
			this.setState({
				style: "uncolorful"
			})
		} else {
			this.setState({
				style: "colorful"
			})
		}
	},
```

So we're passing in an object using `this.setState`, with one key-value pair. You need to use `this.setState`, instead of just assigning `this.state.style` to colorful or uncolorful, because a simple assignment <strong>will not rerender the page</strong>. Only setState will. 

Please note:
* You could include multiple key-value pairs in the setState object, if you wanted!
* You can include as many event handling items as you want. You could have handleClickOnButton, handleClickOnText, handleKeyDown, etc., as long as you include an event listener on the appropriate element
* <strong>Don't forget the comma</strong> between the end of this method, and the beginning of the render method. It will break your app.

There's one last thing we need to do, and that's to set React.createClass's built-in method, getInitialState. Unsurprisingly, this is what React runs when a page first loads, to get its initial state.

Paste this code as the first method of ListOfThings (it is <em>initial</em> state, after all). And don't forget the comma!

```jsx
getInitialState: function() {
	return { style: "uncolorful" }
},
```

Finally, we need the class we're toggling by changing the variable `style` to actually change something. You could write inline CSS for this, but you should know by now how to set up a separate stylesheet and link to it. Here's the bare-bones code I used:

```css
.colorful {
	color: red;
}

.uncolorful {
	color: black;
}
```

<h3>That's it!</h3>

Your index.html file will now show a lovely list of two books that changes colors upon the click of a button. If it's not, take a look at <a href="https://github.com/rebeccaestes/react-tutorial/blob/master/index.html">my solution code</a> to try and figure out where you went wrong.

<h4>What's next?</h4>

Check out <a href="https://facebook.github.io/react/index.html">React's documentation</a>. If you have a few dollars laying around I recommend the Udemy course <a href="https://www.udemy.com/learn-and-understand-reactjs">Build Web Apps with React JS and Flux</a>. 
