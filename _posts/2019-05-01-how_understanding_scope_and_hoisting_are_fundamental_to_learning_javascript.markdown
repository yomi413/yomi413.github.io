---
layout: post
title:      "How Understanding Scope and Hoisting Are Fundamental to Learning JavaScript"
date:       2019-05-01 16:19:17 -0400
permalink:  how_understanding_scope_and_hoisting_are_fundamental_to_learning_javascript
---

# **What exactly is scope?**

When it comes to reading and using variables we need to understand the context in which that small piece of code is allowed to be used.  This is where scope comes in.  In basic terms scope is the area in which something is available to us.  

Within code we are constantly dealing with different areas. We have to think of each piece of code as small microcosms, and try to understand how the variables and functions we declare fit into each small piece.  Certain rules apply for how scope is applied, and we need to be aware of how to identify our scopes.  We will explore the three different scopes we deal with in JavaScript.  

# **Global Scope**

Global scope refers to variables declared outside of functions and are available to use throughout the program. They are usually declared at the top of a text editor as follows: 

`var name = “Giants”;`

However, variables defined within functions that are not prefaced with a declarative keyword (`var`, `let` or `const`) also belong to the global scope.  For instance, 

```
function team() {
	teamName = “Giants”;
}

team();

console.log(teamName);     // prints Giants
```

# **Function Scope**

As the name implies, variables declared within functions are now considered to be in the local, or function scope.  These variables are available to that specific function where they are defined, but cannot be accessed outside of said function.  For example, let’s modify our previous example to demonstrate function scope. 

```
function team() {
	var teamName = “Giants”;
}

console.log(teamName);     // ReferenceError: teamName is not defined
```

By declaring the variable with the `var` keyword it is now only available to the `team()` function.  

# **Block Scope**

ES6 brought us many changes to JavaScript, including new keywords to declare variables.  `let` and `const` were introduced to help us identify our variables more specifically, while also allowing for scope to be more direct.  

Whereas `var` allows for function scope, `let` and `const` allow for block scope.  For instance, variables declared with `var` are accessible anywhere within its function regardless of the block within which it was defined.  

```
function student(age) {
	if (age < 12) {
		var grade = ‘elementary’;
	}
	console.log(grade);
}

student(10);     // prints elementary 
```

On the other hand, `let` and `const` provide for a variable’s accessibility within a block, but not to the function.  Our modified function will look as follows, returning a specific error message:

```
function student(age) {
	if (age < 12) {
		let grade = ‘elementary’;
	}
	console.log(grade)
}

student(10);     // ReferenceError: grade is not defined
```

In the last example we see that we cannot invoke `grade` because it is specifically defined inside the `if` block.  If we want the entire function to have access to `grade`, then `grade` must be defined outside of the `if` block and directly inside the function. 

```
function student(age) {
	let grade;
if (age < 12) {
	grade = ‘elementary’;
} else if (age > 14) {
	grade = ‘high school’;
}
console.log(grade);
}

student(10);     // prints elementary
```

**A quick note on the use of `let` and `const`:** In the example above I used `let` to demonstrate how changing the scope of a variable can affect our results.  One important difference between `let` and `const` is that `let` allows for reassignment, while `const` must remain constant.  Therefore, we can declare a variable with `let` at the top of our scope and not assign a value to it until later in the scope; `const` does not allow for this behavior.  Whenever `const` is used we must immediately assign a specific value to our variable.  
	
# **What is Hoisting?**

In JavaScript, hoisting is the mechanism by which variable and function declarations are hoisted to the top of their respective scope before any code is executed.  Hoisting is not a simple concept to understand, so we’ll take it step by step.  

We tend to declare variables like this `var player = “Derek Jeter”;` and don’t consider how the machine is interpreting this piece of information.  This format is not exactly how variables are interpreted by the JavaScript engine.  In fact, when declaring variables the engine is actually interpreting this piece of code as two distinct parts - the declaration and the assignment. 

```
var player;                 // variable declaration
 
player = “Derek Jeter”;     // variable assignment
```

One important thing to understand about hoisting is that while the variable declaration is hoisted, the variable assignment remains in place where ever it is defined in our code. 

If the variable exists inside a function, then the variable declaration gets hoisted to the top of the function scope.  However, when the function is invoked we get back `undefined`.  Interesting, right?

```
function team() {
	console.log(teamName);
	var teamName = “Giants”;
}

team();          // prints undefined
```

This is a bit confusing to understand.  Inside the function the engine is still interpreting the variable declaration first, but it is not reaching the assignment at all.  This may be one of those mysteries that we may never fully wrap our heads around.  We can completely avoid weird results like this in our code by declaring and assigning (or initializing) our variable simultaneously at the top of the function scope.  

```
function team() {
	var teamName = “Giants”;
	console.log(teamName);
}

team();          // prints Giants
```


# **Function Declarations vs. Function Expressions**

We can identify the type of function we are dealing with by the placement of the word function.  A function declaration starts with the word function, whereas a function expression declares a variable which is assigned the value of a function.  

Function declarations get hoisted while function expressions do not.  This means that we can call a function before it is officially defined in our code.   

```
team();                         // invoked function
 
function team() {               // function declaration
	var teamName = “Giants”;
	console.log(teamName);
}                               // prints Giants
```

Calling a function that is defined as a function expression will yield a TypeError.

```
team();                               // TypeError: team is not a function
 
var team = function() {               // function expression
	console.log(‘What sport do we want to see?’);
}
```

The piece of code directly above is interpreted much the same as a variable.  In other words, the variable declaration (`var team`) gets hoisted, but the assignment to a function is not recognized.  The interpreter does not read `team` as a function because it’s actually reading `team` as a variable declaration.

# **The Effects of ES6 Syntax in Hoisting**

As previously discussed, ES6 provides for the use of `let` and `const` to declare variables, so how do these keywords affect the hoisting of variable and function declarations?

`let` and `const` have proven great for organizing code and ensuring that we always declare and assign our variables before anything else is done.  Case in point…

```
console.log(player);

let player = “Derek Jeter”;     // ReferenceError: player is not defined
```

The engine is still interpreting our variable by splitting the left and right sides and hoisting the declaration, but it won’t find the assigned value of the variable in our code.  No matter the scope in which the variables or functions are being declared, using `let` and `const` will return the same ReferenceError.  This reinforces the notion that all variables declared with `let` and `const` should always be declared at the top of our scope.   We will avoid volatility in our code and it will be easier to debug when we know that all variables can be found in one place - at the top of their respective scope.
