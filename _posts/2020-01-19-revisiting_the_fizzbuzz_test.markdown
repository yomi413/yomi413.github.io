---
layout: post
title:      "Revisiting the FizzBuzz Test "
date:       2020-01-19 23:24:42 -0500
permalink:  revisiting_the_fizzbuzz_test
---


I first encountered the FizzBuzz test back in July 2017.  I remember having so much trouble with the lab that I wanted to document my observations about it.  Here are my notes in all their glory.  

> ![](https://i.imgur.com/T9WoDWAm.png)               ![](https://i.imgur.com/seXsWPb.png)

I was really perplexed by the final solution back then.  Fast forward to January 2020 and here I am revisiting FizzBuzz.  As I’ve taken the month of January to review some of the major concepts of JavaScript and Ruby, I stumbled upon the FizzBuzz problem again and tried to make sense of the logic that correctly solves the problem.  

# Understanding Control Flow

Every programming language has what is called control flow.  The flow of how a function or a method works is established by the code that is written to structure the solution.  In the FizzBuzz example the different conditional statements will set up the flow for us.  Let’s understand what the FizzBuzz statement is asking us to do so that we can correctly implement the right control flow .  

# FizzBuzz - The Problem

There are a bunch of variations of the FizzBuzz problem on the interwebs.  Since my first introduction to FizzBuzz came from a Flatiron lab, and since it's the one I vented about in the post I shared above, I will use that example to help make sense of the final solution.  The problem was originally meant to be solved using Ruby, but the same logic applies to JavaScript and probably any other language you want to use.  We’ll solve it using JavaScript.

Here’s the problem:

>  “The goal of FizzBuzz is to build a program that can take a number and if the number is evenly divisible by 3, it should return "Fizz", if it's divisible by 5, it should return "Buzz", and if it's divisible by both 3 and 5, it should return "FizzBuzz".”

It seems simple to construct.  Here’s what we can gather from this word problem.  

1. We must build a function that takes an argument of a number.
2. If the number is a multiple of 3, return “Fizz”.
3. If the number is a multiple of 5, return “Buzz”.
4. If the number is a multiple of both 3 and 5, return “FizzBuzz”.

When you first look at the problem the first expectation is that it should be solved in a linear way from top to bottom.  So, let’s start there.  

```

function fizzBuzz(num) {
	if (num % 3 === 0) {
		return “Fizz”;
	}
}

fizzBuzz(6);     // returns “Fizz”
fizzBuzz(7);     // returns undefined

```

Okay, we’ve established the condition for multiples of 3, but we have a whole lot of numbers to account for.  Before we move on, let’s look at the modulo operator in this function.  Why use modulo?  Understanding that the modulo operator will give us a remainder, we know that when we divide a given number (the multiple) by 3, we want the remainder to be zero (0).  With the first condition we are establishing that if the number is divided by 3 and the remainder is zero we want to return “Fizz”.  Now, let’s add the next condition to the function, also using the modulo operator. 

```

function fizzBuzz(num) {
	if (num % 3 === 0) {
		return “Fizz”;
	} else if (num % 5 === 0) {
		return “Buzz”;
	}
}

fizzBuzz(21);     // returns “Fizz”
fizzBuzz(25);     // returns “Buzz”
fizzBuzz(15);     // returns “Fizz”

```

Okay, we’ve established our second condition for multiples of 5, but is it working properly?  For the most part yes.  If you put in different numbers that are respective multiples of 3 and 5 and we get the result we’re looking for.  But what happens when we put in a number that is a multiple of both 3 and 5, like 15?  The return value is “Fizz”.  Huh, ok, let’s add the condition to account for both and see if the result changes. 

```

function fizzBuzz(num) {
	if (num % 3 === 0) {
		return “Fizz”;
	} else if (num % 5 === 0) {
		return “Buzz”;
	} else if ((num % 3 === 0) && (num % 5 ===)) {
		return “FizzBuzz”;
	}
}

fizzBuzz(15);     // returns “Fizz”

```

Wait, but we have our condition, so what gives?  Let’s review.  

Let’s take the number 15.  We know that 15 is a multiple of 3 and a multiple of 5.  We should have gotten a return of “FizzBuzz”.  But here’s the tricky part.  Because the function goes from top to bottom every line of code in the condition will be read to establish if the condition is true.  Since the condition `num % 3 === 0` is true, then the return for 15 will be “Fizz” and the rest of the function will not run.  It’s not exactly wrong, but it’s not exactly right either.  

Since we know of many instances in the number line with numbers that are divisible by 3 and 5, we have to make sure that the condition that returns true for the combination of those two facts must come first in the function if we want the correct result to be returned.  Let’s rewrite the function to ensure that all conditions work properly. 

```

function fizzBuzz(num) {
	if ((num % 3 === 0) && (num % 5 ===)) {
		return “FizzBuzz”;
	} else if (num % 3 === 0) {
		return “Fizz”;
	} else if (num % 5 === 0) {
		return “Buzz”;
	}
}

fizzBuzz(15);     // return “FizzBuzz”
fizzBuzz(27);     // return “Fizz”
fizzBuzz(35);     // return “Buzz”
fizzBuzz(90);     // return “FizzBuzz”

```

Perfect!  It works the way we want it to.  

For good measure let’s account for any numbers that don’t fall into any of the conditions already established. 

```

function fizzBuzz(num) {
	if ((num % 3 === 0) && (num % 5 ===)) {
		return “FizzBuzz”;
	} else if (num % 3 === 0) {
		return “Fizz”;
	} else if (num % 5 === 0) {
		return “Buzz”;
	} else {
		return `${num} is not a multiple of 3 or 5.`
	}
}

fizzBuzz(15);     // return “FizzBuzz”
fizzBuzz(27);     // return “Fizz”
fizzBuzz(35);     // return “Buzz”
fizzBuzz(90);     // return “FizzBuzz”
fizzBuzz(34);     // returns “34 is not a multiple of 3 or 5.”

```

# Conclusion

The biggest lesson out of this is that every line of code you write will have consequences.  Logically the code makes sense when expressed in a linear way.  However, you have to be prepared to take a hard look at the code you write and understand what each line is doing. The FizzBuzz test is not necessarily a difficult problem, but taking the time to think about each line in the context of the problem you’re trying to solve will make a huge difference in helping you build good clean code.

