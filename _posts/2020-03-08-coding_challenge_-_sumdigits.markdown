---
layout: post
title:      "Coding Challenge - sumDigits()"
date:       2020-03-09 03:39:38 +0000
permalink:  coding_challenge_-_sumdigits
---


Personally I am not a fan of coding challenges in general.  I strongly dislike being put on the spot and I really don’t appreciate having to solve a problem under a time crunch.  However, understanding that they are necessary helps me wrap my head around these types of challenges.  Additionally, I need to know what will be expected of me when I face these challenges.  I want to get better at them and I know I have it in me to improve.   

Problem solving is not so much about solving the actual problem as much as it is about the strategies that can help to solve said problem.  I want to find ways to help me think about about a problem that will ultimately help me come up with the best possible solution.  Let’s look at a problem together.  

I encountered this problem on [CodeWars.](https://www.codewars.com/dashboard)

*Write a function named sumDigits which takes a number as input and returns the sum of the absolute value of each of the number's decimal digits. For example:

    sumDigits(10);     // Returns 1
    sumDigits(99);     // Returns 18
    sumDigits(-32);     // Returns 5
		 
Let's assume that all numbers in the input will be integer values.*


I decided to use a technique that my kids have been using in school and that I’m sure I learned years ago in elementary school.  Before we write any code let’s decode the problem at hand.  Let’s read through the problem, and underline or highlight clues that can help us  come up with a solution.

*Write a function named sumDigits which takes a number as input and **returns the sum** of the **absolute value** of **each of the number's decimal digits** . For example:*

    sumDigits(10);     // Returns 1
    sumDigits(99);     // Returns 18
    sumDigits(-32);     // Returns 5
		
*Let's assume that **all numbers in the input will be integer values**.*

Let’s unpack this a little more, looking at some specific clues more closely.  Before we write any code let’s break down the problem into smaller pieces.  While we look at the clues, keep in mind that you don’t have to look at each clue in the same order as they were given to you.  For this problem I wanted to start from the end and work my way up. 

1. “**all numbers in the input will be integer values**” => We can automatically discount any floating numbers (13.45) or other non-numerical inputs (no letters).  Also, our data type will be an integer; therefore, no strings, arrays, objects or booleans. Now that we know what the input will NOT be, let’s proceed with the next clue.  This is the number being passed in. 

2. “**absolute value**” => What is meant by absolute value?  Even if we don’t know what the absolute value of a number is, we know it will be important to the final result.  Look up what the absolute value of a number is in order to know how you will find the absolute value of your result.

3. “**each of the number’s decimal digits**” => Honestly, I don’t know what decimal digits are.  I ran a search for a definition and it is still unclear.  However, based on the examples that were given (*sumDigits(10);     // Returns 1*) I know that I have to separate the given number into separate digits.  In other words, the number 10 has a 1 and a 0, and we will have to do something with those separate digits.

4. “**return the sum**” => Simply put, we will be adding at least 2 items together get the sum of something.  

And now the real fun begins.  Let’s go back to the original problem.  Now that we’ve decoded parts of the problem, let’s start to put some code down. 

Let’s start by declaring the function as described in the problem.  
```
function sumDigits(number) {
	// return sum
}
```

Now that the function has been declared we can “fill in the blanks” of the rest of the function based on the notes that we wrote above.  

**Absolute Value**

For this problem I knew I had to find the absolute value of our number first.  So, what is the absolute value of a number anyway?  To think of a number’s absolute value means to think of the number as its distance from 0.  Think of a number line.

![](https://i.imgur.com/RP5V6kA.png)

The distance between -6 and 0 is 6, which is the same as the distance between 0 and 6.  In other words, regardless of the distance on the positive or negative side of 0, the absolute value will be the same and will always be positive.  

Before we do anything else let’s make absolutely certain that all the numbers we use are positive.  Thankfully, JavaScript gives us a great method for us to use - `Math.abs()`.  

Let’s add some code to the function to make sure all numbers passed in are positive.
```
function sumDigits(number) {
    const absoluteNum = Math.abs(number)
	
	console.log(absoluteNum)
  // return sum
}

sumDigits(-99);	     // prints 99
```

Okay, cool!  It worked.  Now that we’re dealing with only positive numbers it should make our lives much easier.  

**Create an Array of Strings**

The next step is to separate the number into separate digits that could be added.  In fact, this next step requires two distinct steps that will be happening at the same time by chaining methods together.  First, we have to convert the number into a string by using the `toString()` method.  Second, we have to split the string into an array using the `split()` method.  That would look as follows:
```
function sumDigits(number) {
	  const absoluteNum = Math.abs(number)
	  const digitsArr = absoluteNum.toString().split(‘’)
	  console.log(digitsArr)
    // return sum
}

sumDigits(-99);	     // prints [“9”, “9”]
```

Notice how all of the methods we’ve implemented are reflected in the last printed item above.  

**Iterating**

Finally, we know that we have to come up with the sum of the digits in the array.  One way to do it is initializing a `sum` variable and assign it to a value of 0.  By having this variable declared you can now use it in your final solution and you can return that sum.
```
function sumDigits(number) {
	const absoluteNum = Math.abs(number);
	const digitsArr = absoluteNum.toString().split(‘’);
	let sum = 0;
	
  return sum;
}

sumDigits(-99);	     // returns 0
```
Right now, because the `sum` variable has been assigned a value of 0, when you return `sum`, calling the function will return 0.  We need one very important step in order to get the correct result.

The final step is iterating through digitsArr to get the sum total of the digits that make up the passed in number.  For this I decided to use the `map()` method as the iterator.   What does the the `map()` method give us?
```
function sumDigits(number) {
	  const absoluteNum = Math.abs(number);
	  const digitsArr = absoluteNum.toString().split(‘’);
	  let sum = 0;

	  digitsArr.map(num => {
		  console.log(num)
	  })
	
    return sum;
}

sumDigits(34);     // prints 3 4
```

Running this function prints each digit separately.  Now we can use the `sum` variable to add each of those numbers to the sum. 
```
function sumDigits(number) {
	const absoluteNum = Math.abs(number);
	const digitsArr = absoluteNum.toString().split(‘’);
	let sum = 0;

	digitsArr.map(num => {
		sum += num
	})
	
  return sum;
}

sumDigits(-99);	     // returns “099”
```
Hmmm, something went wrong.  Let’s analyze.  

Clearly adding the num variable to the `sum` isn’t working the way we expected it to.  Why is that?  For starters, we’re forgetting that the `num` variable that we are getting back after iterating is still a string.  Each element in the `digitsArr` is not an integer.  All we need to do is make sure that any value that gets added to `sum` is in fact an integer and not a string.  (Remember that when you add strings you are actually concatenating them into a larger string.)

So what can we do to change this?  We must use the `parseInt()` method in order to convert the `num` variable from a string to an integer.  Once we do that, our `sum` will be returned as a proper integer.  
```
function sumDigits(number) {
	  const absoluteNum = Math.abs(number);
	  const digitsArr = absoluteNum.toString().split(‘’);
	  let sum = 0;

	  digitsArr.map(num => {
		  sum += parseInt(num)
	  })
	
  return sum;
}

sumDigits(-99);	     // returns 18
```

And that’s it!  We get exactly what we expected to return, the sum of the digits from the number passed into the function.  

I know that a problem like this can be solved in many different ways (`reduce()` method anyone?).  I’ve even seen this problem solved as a one-liner.  I don’t necessarily recommend it because it could be harder to read and understand the full chain of methods that are being used.  In my humble opinion, taking the time to solve it this way allows you to think through each portion of what’s happening in the function and allows you to give each line of your code a very specific task.  Let’s keep these challenges coming.  I know it's the only way to get better at them. 

