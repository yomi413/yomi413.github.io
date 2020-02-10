---
layout: post
title:      "Deconstructing JavaScript - Spread Operator"
date:       2020-02-09 23:31:29 -0500
permalink:  deconstructing_javascript_-_spread_operator
---


In the midst of making sense of a programming language we tend to focus on the big picture items - the building blocks of how things work, the different components that make up a language.  I recently had to use the spread operator to solve a problem and it got me thinking - what is the spread operator (or spread syntax as it is defined in the MDN documentation) and what does it do?

**The spread operator**

The spread operator is a simple expression.  According to the definition found in the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) 
> “Spread syntax allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.”

It is represented by 3 dots (...) that precede an iterable data structure.  The key to understanding the spread operator is understanding that you’re using each element as an argument.  Let’s dive a little deeper into what this means.

**Spreading an array**

To spread the operator just means that the iterable data is being spread out of the array.  For example, 

```
const args = [0, 1, 2, 3]
console.log(args)     // prints [0, 1, 2, 3]

console.log(...args)     // prints 0 1 2 3
```

Let’s see it in action in a different context.  Say we have a function to help us find the length of the longest word in a string.  The function will take a string as an argument.

```
const arr = [ ];

function findLongestWordLength(str) {
	let words = str.split(“ “);
const arr = [ ];
	
	for (let i = 0; i < words.length; i++) {
		arr.push(words[i].length)
	}
	return Math.max(...arr)
}

console.log(arr)     // prints [2, 2, 2, 3, 2, 3, 4, 2, 3, 8]
console.log(findLongestWordLength(“To be or not to be, that is the question”))     // prints 8
```

In the function above the first thing we do is convert the given string into an array.  Next, we create a new data structure that will be used to store information.  Once that part is done we can iterate through the array using a `for` loop.  Inside the loop, we want to go through each element in the array and then store the length of each of those elements into the empty array we previously declared.  

We know we need to return a number.  The new `arr` stores all of our lengths (see the first console.log call above).  But we essentially only want the biggest number in the array.  Thankfully we have a nice clean method for that - we can return the biggest number by running `Math.max()` and passing the array as an argument into `Math.max()`.  Not so fast though.  You can’t just pass the array.  You have to pass the array with the spread operator in order to get the correct result.  Why?  As previously explained the spread operator spreads the array elements so that each element can be seen as its own argument.  `Math.max(arr)` is interpreted as a single argument, but doesn’t reach each element within that argument.  `Math.max(...arr)` is interpreted as a series of arguments that are being passed into `Math.max()` and that will give us the correct result. 

It can be a little complicated to understand this concept.  It might even take a few practice problems to really wrap your head around this.  Give it a try and keep practicing.

**Copy an array**

The spread operator can also create a copy of the array.  We are still spreading the array, but because we want to keep the elements in an array format we must surround the call with an array literal, or square brackets.  This is a simple and clean way to keep things separate if you want to mutate the elements of the array without mutating the original array.  

```
const ages = [21, 36, 55, 34]
const allAges = [...ages]

console.log(ages)     // prints [21, 36, 55, 34]
console.log(allAges)     // prints [21, 36, 55, 34] 
```

**Concatenation of arrays**

The spread operator can also concatenate, or combine, two or more arrays.

```
const arr1 = [0, 1, 2]
const arr2 = [3, 4, 5] 
const arr3 = [...arr1, ...arr2]

console.log(arr3)     // prints [0, 1, 2, 3, 4, 5]
```

One important thing to keep in mind is that the rules of the declaration of variables still apply.  If we want to change one of the arrays already declared then we would have had to use `let` to declare said variable.  For instance, if we want to add `arr2` to `arr1` but didn’t want to declare a brand new variable for this action, `arr1` would have had to be declared with `let`.  Since `arr1` was declared using the `const` keyword, trying to add another array using the spread operator would give us an error message.  

This won’t work...
```
const arr1 = [0, 1, 2]
const arr2 = [3, 4, 5]
arr1 = [...arr1, ...arr2]     // Uncaught TypeError: Assignment to constant variable.
```

...but this will.
```
let arr1 = [0, 1, 2]
const arr2 = [3, 4, 5]
arr1 = [...arr1, ...arr2]     // prints [0, 1, 2, 3, 4, 5]
```

**Spread operator and strings**

So how does the spread operator work with strings? Let’s check it out.  

You can spread the strings the same as the array. 

```
const str = “Tomorrow”
console.log(...str)     // prints T o m o r r o w
```

You can also put each character from the string into an array. 

```
console.log([...str])     // prints [“T”, “o”, “m”, “o”, “r”, “r”, “o”, “w”]
```

However, attempting to copy the string won’t work the same way as with arrays.  If you put quotes around the spread string, you will get the literal representation of anything inside the quotes. 

```
console.log(“...str”)     // prints ...str
```

**Spread operator and objects**

When used within objects, the spread operator is somewhat similar to the array.  However, there are differences that are important to note to make sure you know what to expect. 

Very much like arrays you can use the spread operator on an object to create a copy of the object. 

```
const obj1 = {firstName: “Sam”, lastName: “Oh”}
const obj2 = {...obj1}

console.log(obj2)     // prints {firstName: “Sam”, lastName: “Oh”}
```

What if we try to spread the original object without object literals?

```
console.log(...obj1)     // Uncaught TypeError: Found non-callable @@iterator
```

What if we add array literals to the spread object?

```
console.log([...obj1])     // Uncaught TypeError: obj1 is not iterable
```

So to recap, you can’t spread the object without the object literal, and you can’t create an array of the spread object.  Why?  The MDN documentation explains this perfectly: 
> Objects themselves are not iterable, but they become iterable when used in an Array, or with iterating functions such as `map()`, `reduce()`, and `assign()`. 

Because objects are not iterable there are no elements from the object to spread.  Once again, you have to be mindful of how you want to use the spread operator and understand the consequences that follow.

You can also combine objects, but only as long as the keys are different.  If the keys are different, the objects will come together to form a larger object.  However, if the keys are the same, only the second object will be copied into the newly formed object.  

```
const obj1 = {firstName: “Sam”, lastName: “Oh”}
const obj2 = {firstName: “Charlie”, lastName: “Rose”}
const obj3 = {address: “1234 Main Street”, city: “Bronx”, state: “NY”}

const newObj = {...obj1, ...obj2, ...obj3}
console.log(newObj)   // prints {firstName: “Charlie”, lastName: “Rose”, address: “1234 Main Street”, city: “Bronx”, state: “NY”}
```

Notice how `...obj1` argument is completely left out of the `newObj` variable. 

**A note on rest parameters (or rest syntax)**

The rest parameter looks exactly like the spread operator, but performs differently.  It is used for destructuring arrays and objects, and seemingly condenses elements rather than expanding them.  For example, when writing the following function we pass the function an argument as a rest parameter.  The rest parameter allows you to call the function with any number of arguments that the function may call for. 

```
const myFunction = (...names) => console.log(names)
myFunction(“Jenny”, “Simone”, “Maria”, “Wyatt”)   // prints [“Jenny”, “Simone”, “Maria”, “Wyatt”]
```

A similar construct can be used for objects.

```
const obj1 = {firstName: “Sam”, lastName: “Oh”}
const obj2 = {firstName: “Charlie”, lastName: “Rose”}
const obj3 = {address: “1234 Main Street”, city: “Bronx”, state: “NY”}

const merge = (...objects) => console.log({ ...objects })     
merge(obj1, obj2, obj3)     // prints {0: {firstName: “Sam”, lastName: “Oh”}, 1: {firstName: “Charlie”, lastName: “Rose”}, 2: {address: “1234 Main Street”, city: “Bronx”, state: “NY”}}
merge(obj1, obj3)     // prints {0: {firstName: “Sam”, lastName: “Oh”}, 1: {address: “1234 Main Street”, city: “Bronx”, state: “NY”}}
```

**Conclusion**

Simple syntax can really make a difference in your code.  It can help break things down while also making it easier to read.  The use of the spread operator requires study and understanding so as to not end up with unexpected results.  This is now becoming my new favorite syntax.  





