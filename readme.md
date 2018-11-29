# Modules in NodeJS

## Require Statements

When you're coding a website and you want to use someone else's library of code, you need to use a `<script src="path/to/library"></script>` tag. However, in NodeJS programs we don't have access to a HTML file, so `<script>` tags aren't an option!

That's where `require('path/to/library')` statements come in. They essentially do the same work as a script tag - they find the file in question, execute it, and return a pointer to the "module" it just loaded.

```
var myModule = require('./modules/addNumbers.js');
```

Let's try some exercises to get us comfortable with require() statements. Each exercise below has a corresponding folder in this repository.

1) Write an run a program that requires all 3 files in this folder. When you run your program, you should see 3 separate strings logged to the console.
	- This should prove that your require() statments will execute the code within each file, one by one.
2) Require 3 files that export different things. Console log them to see what the values are
3) Require a file that exports an array. Loop through the array and log the elements.
4) Require a file that exports a add function. Use that function to add the first two program arguments
5) Require a file that exports a cat ascii and a file that exports a dog ascii. ALso, require a function that takes two arguments and randomly returns one of them. Use those three to write and run a file that will randomly return a dog or a cat

See, modules aren't really that complicated! When a module is required, it will run its code and return some value. It's up to you what to do with that module.

## Node's built in modules

I admit, those first exercises were a bit silly, so let's use require statements to utilize some of Node's built in modules. You'll notice that you don't need to provide a full file path to these modules - you just need to pass in the name of the module!
```
var fs = require('fs');
```
Try the exercises below. (These exercises don't have corresponding folders in this repository)

1) Write a program that uses the 'os' module to console log the amount of free memory on your computer
https://www.w3schools.com/nodejs/ref_os.asp
2) Write a program that uses the 'dns' module to console log the IP address of a given URL (pass a URL as an argument to your program)
https://www.w3schools.com/nodejs/ref_dns.asp
3) Use the "timers" module to write a program that logs "tic" and "tock" every second
https://www.w3schools.com/nodejs/ref_timers.asp


## Writing your own modules

If you want to write your own module, all you need to do is write an "export" line at the bottom of your file:

```
// file1.js
module.exports = 3;

// file2.js
var variable = "hi";
variable = "hi".repeat(10);
console.log("You can write whatever code you want in a module!");
console.log("Just make sure to export something at the bottom of the file");
module.exports = variable;

// file3.js
module.exports = {
	foo: "bar",
	otherFoo: "otherBar"
}

// file4.js
module.exports = function() {
	return "someValue"
}
```
You can have your module export any type of JavaScript value! `module.exports` behaves similarly to `return` statements.

Here's another way to think about it. The value on the right hand side of `module.exports =` gets passed to the variable on the left hand side of `= require('./some/file')`

```
// foo.js
module.exports = "this is a value";

// bar.js
var foo = require('./foo.js');
console.log(foo); // "this is a value"
```

1) Write a file that exports the number three. Write a file that exports the number five. Write a program that requires those files and console logs the sum of three and five
2) Write a file that exports the string 'Hello'. Write another file that requires the 'Hello' file and appends ' World' to that value and exports it. Write a third file that requires the previous file and console logs its value. You should see "Hello World" logged in your console.
3) Write a file named russianDoll.js that defines this variable below and exports it. Write another file that requires russianDoll.js and uses a loop that iterates through the doll, console logging every "value" along the way.
```
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
```

## Circular Dependencies

Now that you're getting the hang of modules, you should be aware of "circular dependencies". It's possible for two files to require each other:

```
// file1.js
var foo = require('./file2.js);

// file2.js
var foo = require('./file1.js);
```

Node doesn't know how to handle this scenario! (When you run file1.js, the require statement will cause file2.js to run, which will cause file1.js to run again, which will cause file2.js to run again, etc...) This is called a circular dependency. 

1) Write a file called one.js that requires two.js. Write a file called two.js that requires three.js. Write a file called three.js that requires one.js. Try to run one.js and see what happens!


## CHALLENGE PROBLEM:

Write a module named "calculator.js". Have it export an object with four keys, "add", "subtract", "multiply", and "divide". Each of these keys should point to a function that implements the given arithmetic operator.

Test your module by writing another file that requires your calculator and uses the arithmetic functions you implemented.
