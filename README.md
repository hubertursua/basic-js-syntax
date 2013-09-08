# Basic JavaScript Syntax

## Contents

* Variables and data types
	* Strings
	* Numbers
	* Booleans
	* Functions
	* Arrays
	* JSON objects
* Conditions
	* if statements
	* switch statements
	* Comparison operators
	* Logical operators
* Loops
	* for loops
	* for-each loops
	* while loops
	* do-while loops
* Functions
	* Named functions
	* Anonymous functions
	* Invoking a function
	* Default parameter values
* Comments

## Variables and data types
Declaring variables in JavaScript is done using the `var` keyword. JavaScript is a weakly-typed language, thus you do not need to specify a data type. It will try to detect it automatically.

```js
var x;
// The variable x was declared with an undefined value.
```

### Strings
You can use single or double quotes for string values. As with other languages, the double quotes will evaluate escaped characters while single quotes will treat them as-is.

```js
var name = "John Doe";

var address = 'Quezon City';
```

### Numbers
JavaScript accepts integers and floating numbers.

```js
var two = 2;
var pi = 3.1416;
```

### Booleans
Booleans can either have the value `true` or `false`.

```js
var yes = true;
```

### Functions
To assign a function to a variable:

```js
var foo = function () {

};
```

More about functions in the section below.

### Arrays
Arrays in JavaScript do not require a predefined size. Use `[ ]` to specify that your data is an array.

```js
var blank = [];
```

To add values in an array, just add any element separated by a `,`.

```js
// Array with preset values
var numbers = [3, 7, 1, 14];
```

To add elements in a pre-existing array, use `.push()`.

```js
// Array with added values
var animals = ["duck", "mouse"];
animals.push("dog");
animals.push("cat");
animals.push("pig");
```

To get the length of an array, use `.length`.

```js
// Array with added values
var animals = ["duck", "mouse"];
console.log(animals.length);
```

To remove the contents of an array, reset it using `.length`.

```js
// Array with added values
var animals = ["duck", "mouse"];
animals.length = 0;
console.log(animals.length);
```

### JSON objects
You can create JavaScript objects on the fly using JSON. It is created using `{ }`. It follows a property-value separated by a `:`. Multiple properties are separated by a `,`.

```js
var person = {
	first_name: "John",
	last_name: "Doe"
};
```

Moreover, it contain any data type, including other JSON objects. Therefore, you can have something complex like this:

```js
var dog = {
	breed: "beagle",
	age: 3,
	appearance: {
		colors: [
			"white",
			"brown",
			"orange"
		],
		height: "short"
	},
	bark: function () {
		return "woof!";
	}
};
```

There are other data types, but they are mostly variants of those that we discussed.

## Conditions

### if statements
```js
if (<condition>) {
	// code here
}
else if(<condition>) {
	// code here
}
else {
	// code here
}
```

### switch statements
JavaScript will accept any data type in switch statements but I recommend you stick with the basic data types (i.e. strings, numbers, booleans).

```js
switch(<condition>) {
	case <value>:
		// code here
		break;
	case <value>:
		// code here
		break;
	case <value>:
		// code here
		break;
	default:
		// code here
}
```

### Comparison operators

* `>` -- greater than
* `<` -- less than
* `>=` -- greater than or equal to
* `<=` -- less than or equal to
* `==` -- is equal to
* `!=` -- is not to
* `===` -- is equal to and have the same type
* `!==` -- is not equal to or does not have the same type

Even though JavaScript will try to automatically convert some of your data types to what you need in a situation, it's best if you do not rely on this. Always make sure that a variable will contain its intended data type. Always use `===` and `!==` instead of `==` and `!=`.

### Logical operators

* `&&` -- AND
* `||` -- OR
* `!` -- NOT

## Loops

### for loops
```js
for (<initializer>; <condition>; <iterator>) {
	// code here
}
```

```js
// Example
for (var i = 0; i < 10; ++i) {
	console.log("hello " + i);
}
```

### for-each loops
There are two ways to do a for-each in JavaScript.

The first is this:

```js
for (var <index_variable> in <array>) {
	// code here
}
```

```js
// Example
var animals = ["dog", "cat", "pig"];

for (var i in animals) {
	var animal = animals[i];
	console.log(animal);
}
```

There's a second way of doing a for-each but this isn't supported by older browsers.

```js
<array>.forEach(function (<element>) {
	// code here
});
```

```js
// Example
var animals = ["dog", "cat", "pig"];

animals.forEach(function (animal) {
	console.log(animal);
});
```

### while loops

```js
while (<condition>) {
	// code here
}
```

```js
// Example
var x = 0;
while (x < 10) {
	console.log("hello " + x);
	++x;
}
```

### do-while loops

```js
do {
	// code here
} while(<condition>);
```

```js
// Example
var x = 0;
do {
	console.log("hello " + x);
	++x;
} while (x < 10);
```

## Functions

### Named functions

```js
function foo (x, y) {
	return x + y;
}
```

### Anonymous functions

```js
var foo = function (x, y) {
	return x + y;
};
```

### Invoking a function
Call a function using its name followed by `()`. If it has parameters, pass them separated by a `,`.

```js
var foo = function (x, y) {
	return x + y;
};

var s = foo(5, 3);

console.log(s);
```

### Default parameter values
In JavaScript, a function call will not break if you have incomplete parameters.

However, the problem is you cannot assign default values to a function parameter through its signature.

```js
// This will NOT work
var hello = function (name = "john") {
	return "hello " + name;
};
```

Instead, we have to use conditions. There are two ways to do this.

The first method is this:

```js
var hello = function (name) {
	name = name || "john";
	// code here
};
```

The segment `name || "john"` will evaluate as follows:
1. Check the value of `name`. If it is `true`, then return its value and ignore the right side of `||`.
1. If the left side of `||` is `false`, return the right side of `||`.
1. The returned values are assigned to the variable. In this case, we reassign a new value for `name`.

Method #1 works for most cases except when dealing with numbers and booleans since `0` and `false` will evaluate as `false` (forcing the whole statement to return the right side of `||`).

The second method is an extension of the first.

```js
var foo = function (x, y) {
	x = x || (x === 0 ? x : 100);
	y = y || (y === 0 ? y : 100);
	return x + y;
};
```

The right side of `||` now looks more complex. This is a shorthand `if-else` statement. Since we are expecting numbers as a value of `x`, our problem is the value `0`. So after the left side of `||` fails, we do another check. This time we strictly check the type and value using `===`. If it is `true`, then we return the value of x. Otherwise, we finally return our default value which is `100`.

## Comments

```js
// Single-line comment

/*
Multi-line
comment
*/
```
