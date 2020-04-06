---
layout: post
title:      "Slice vs. Splice"
date:       2020-04-06 03:42:08 +0000
permalink:  slice_vs_splice
---


In JavaScript, methods like `slice()` and `splice()` can be really confusing to use.  I hope to be able to explain them in simpler terms to help me remember their differences. 

**Slice**

In everyday life we think of slice in a few different ways.  To slice is the act of cutting a small portion of something.  A slice harkens memories of our favorite pie or the best pizza in town.  So, how can we understand the word slice as a method in JavaScript?

Pretty similar to cutting a piece of pie, the `slice()` method gives us a piece of an array.  When using the `slice()` method, we give it specific arguments that determine where we want the slicing of the array to begin and where we want it to end. 

For example, …

```
const fruits = [‘apple’, ‘pear’, ‘papaya’, ‘mango’, ‘pineapple’, ‘guava’]

console.log(fruits.slice(1, 4));     // prints [‘pear’, ‘papaya’, ‘mango’]
```

Notice the example above.  We are passing two arguments, the beginning (first argument) and end (second argument).  In other words, we want the slicing of the array to begin at index 1 and end at index 4.  When providing the second argument, the main thing to remember is that while it gives us a hard end to the slicing of the array, the slice we get back is not inclusive of this index.  We will only get back an array with elements found at index 1, index 2 and index 3.  What if we only pass one argument?

`console.log(fruits.slice(3));     // prints [‘mango’, ‘pineapple’, ‘guava’]`

By passing only one argument we’re giving our `slice()` method an explicit beginning without an explicit end.  This is interpreted in JavaScript as a request to slice the array starting at index 3 and give us all elements after index 3.  In other words, not having the second argument is the same as if we had explicitly added the following argument: `fruits.length`. 

`console.log(fruits.slice(3, fruits.length));     // prints [‘mango’, ‘pineapple’, ‘guava’]`
 
The most important detail to remember about using the `slice()` method is that slicing from the original array does not affect the original array.  When you `console.log()` `fruits` after previously using the `slice()` method, you see that the original `fruits` array remains unchanged.  

`console.log(fruits)	// prints [‘apple’, ‘pear’, ‘papaya’, ‘mango’, ‘pineapple’, ‘guava’]`


**Splice**

I had to look up the definition of splice to make sure that I understood it. In general, splicing refers to the joining of separate pieces of rope or cable.  So how do we use the `splice()` method?  Let’s revisit our `fruits` array from above. 

`const fruits = [‘apple’, ‘pear’, ‘papaya’, ‘mango’, ‘pineapple’, ‘guava’]`

When manipulating the above array, we have to understand how the arguments that we pass can manipulate the array.  Let’s try an example. 

`fruits.splice(2, 0, ‘banana’);`

The `splice()` method can take 3 arguments.  The first argument, 2, represents the index where we want the new element inserted.  The second argument, 0, represents the amount of elements that we want deleted from the array.  In our example we are not deleting any elements in order to insert the new element.  Finally, the third argument, `banana`, represents the new item that we want inserted at index 2.  Our new `fruits` array will look as follows:

`console.log(fruits);     // prints [‘apple’, ‘pear’, ‘banana’, ‘papaya’, ‘mango’, ‘pineapple’, ‘guava’]`

As you can see from the new array above, `banana` is in the second index of the array and we didn’t delete any of the other elements.  The original `fruits` array had 6 items; the new `fruits` array after using the `splice()` method has 7 items. 

Let’s look at another example.

```
fruits.splice(1, 1, ‘strawberry’);

console.log(fruits);     //	prints [‘apple’, ‘strawberry’, ‘banana’, ‘papaya’, ‘mango’, ‘pineapple’, ‘guava’]
```

In this last example we are replacing `pear` with `strawberry`.  

The `splice()` method is very versatile because of how it can be used.  The examples above demonstrate how items within an array can be inserted and replaced.  But you can also delete items very easily. 

Of the 3 arguments that can be passed the second and third arguments are optional. If you pass only one argument it’s indicating the index where we want to start deleting items from the array.  

```
fruits.splice(2);

console.log(fruits);     // prints [‘apple’, ‘strawberry’]
``` 

If we decide to exclude the third argument, our example would look something like this:

```
fruits.splice(2, 4);

console.log(fruits);     // prints [‘apple’, ‘strawberry’, ‘guava’]
```

In other words, starting at index 2 (`banana`) we delete the next 4 elements in the array (`[‘banana’, ‘papaya’, ‘mango’, ‘pineapple’]`).  When we print `fruits`, our array has gone from 7 items to 3 - `[‘apple’, ‘strawberry’, ‘guava’]`. 

If we pass only the first and third arguments, the array does not change at all.  However, if we pass only the third argument without the first two arguments, then all elements of the array are deleted, and when we print the `fruits` array then we get an empty array.  

```
fruits.splice(‘grapes’);

console.log(fruits);     //	prints []
```

To be safe the best approach is to use the arguments as they are intended, especially since the `splice()` method can be so destructive.  
 
**Conclusion**

Using `slice()` or `splice()` can be very useful in code, but it’s important to note their differences.  It’s really easy to get confused by them and not be entirely sure when or how to use them.  For starters, `splice()` should not be confused with `slice()`.  Whereas `slice()` does not change the content of the original array, `splice()` will certainly modify the original array.  Another thing to remember is that they may demonstrate very similar behavior, but you have to understand the different results of their use.  I know all of this takes time to figure out and learn, but with time and continued practice this too will soon be part of my ever-growing arsenal of code.





 

