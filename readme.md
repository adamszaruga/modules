# Modules in NodeJS

### Require Statements

When you're coding a website and you want to use someone else's library of code, you need to use a `<script src="path/to/library"></script>` tag. However, in NodeJS programs we don't have access to a HTML file, so `<script>` tags aren't an option!

That's where `require('path/to/library')` statements come in. They essentially do the same work as a script tag - they find the file in question, execute it, and return a pointer to the "module" it just loaded.

```
var myModule = require('./modules/addNumbers.js');
```

Let's try some exercises to get us comfortable with require() statements:

1) Write an run a program that requires 3 files that execute a console.log() statement
	- This should prove that those files get run
2) Require 3 files that export different things. Console log them to see what the values are
3) Require a file that exports an array. Loop through the array and log the elements.
4) Require a file that exports a add function. Use that function to add the first two program arguments
5) Require a file that exports a cat ascii and a file that exports a dog ascii. ALso, require a function that takes two arguments and randomly returns one of them. Use those three to write and run a file that will randomly return a dog or a cat

See, modules aren't really that complicated! When a module is required, it will run its code and return some value. It's up to you what to do with that module.

I admit, those modules you were requiring are a bit silly, so let's use require statements to use some of Node's built in modules. You'll notice that you don't need to provide a full file path to these modules - you just need to pass in the name of the module!

var fs = require('fs');

1) Write a program that uses the 'os' module to console log the amount of free memory on your computer
https://www.w3schools.com/nodejs/ref_os.asp
2) Write a program that uses the 'dns' module to console log the IP address of a given URL (pass a URL as an argument to your program)
https://www.w3schools.com/nodejs/ref_dns.asp
3) Use the "timers" module to write a program that logs "tic" and "tock" every second
https://www.w3schools.com/nodejs/ref_timers.asp


If you want to write your own module, all you need to do is write an "export" line at the bottom of your file:

module.exports = 3;

var variable = "hi";
module.exports = variable;

module.exports = {
	foo: "bar",
	otherFoo: "otherBar"
}

module.exports = function() {
	return "someValue"
}

When you (or someone else) require a module, the value that gets returned is what you 

Here's another way to think about it. The value on the right hand side of "module.exports =" gets passed to the variable on the left hand side of "= require('./some/file')"

foo.js
module.exports = "this is a value";

bar.js
var foo = require('./foo.js');
console.log(foo); // "this is a value"

1) Write a file that exports the number three. Write a file that exports the number five. Write a program that requires those files and console logs the sum of three and five
2) Write a file that exports the string 'Hello'. Write another file that requires the 'Hello' file and exports 'Hello World'. Write a third file that requires the previous file and exports 'Hello World!'
3) Write a file that defines this variable and exports it:
var russionDoll = {
	value: "Big Doll",
	child: {
		value: "Medium Doll",
		child: {
			value: "Small Doll",
			child: {
				value: "Tiny Doll"
			}
		}
	}
}
Write a file that requires the russion doll, and iterates through it and logs the innermost value

Now that you're getting the hang of modules, you should be aware of "circular dependencies". It's possible for two files to require each other

1) Write a file called one.js that requires two.js. Write a file called two.js that requires three.js. Write a file called three.js that requires one.js. Try to run one.js and see what happens!


CHALLENGE PROJECT:

Write a module named "calculator.js". Have it export an object with four keys, "add", "subtract", "multiply", and "divide". Each of these keys should point to a function that implements the given arithmetic operator.

Test your module by writing another file that requires your calculator and uses the arithmetic functions you implemented
