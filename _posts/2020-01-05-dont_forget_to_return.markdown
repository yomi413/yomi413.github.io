---
layout: post
title:      "Don't Forget to `return`"
date:       2020-01-05 20:36:48 +0000
permalink:  dont_forget_to_return
---

It is January 2020!  As I start the new year, I have committed to upgrade myself and update my coding skills.  I have been doing a lot of coding with HTML and CSS to help build up those skills, but have put aside a lot of the object oriented principles I learned as a Flatiron student.  Despite having reviewed some JavaScript just a few months ago, and remembering the foundations and sytax of the language, I needed to practice the development of data structures and algorithms.  As they say, use it or lose it, and I was determined not to keep losing it.

So, as I made my return to JavaScript, I wanted to break down the actual concept of `return`.  It seems pretty straightforward, but it's easy to lose sight of how using the `return` keyword can affect our results.

# Where to Use `return`
The explicit use of `return` is primarily inside functions where we want a value returned.  However, we have to remember that `return` does not automatically print anything for us.  We will only see the returned value in the console when we invoke, or call, the function. 

![](https://i.imgur.com/8mvi8WQ.png)

It should not be confused with console.log(), which is a function that logs, or prints, information to the console.  That's a topic for another day, though.

# How `return` Sets Limits
When we use the `return` keyword inside the function we are effectively telling the computer to stop evaluating the function.  Anything within the function that comes *after* the `return` statement will not compute.  For instance, as in the example below, we set up a calculation to change the value of the `sum` variable, and then we want to return something else.  

![](https://i.imgur.com/xtfyywF.png)

However, if we changed the order in which we want the computer to evaluate the function, and place the `return` *before* the rest of what we want evaluated, the `return` ends the function.  Anything inside the function that comes after the `return` is obsolete. 

![](https://i.imgur.com/bvrgEiq.png)

# Lack of `return`
So, what happens when we don't explicitly use the `return` keyword?  

![](https://i.imgur.com/90APmpN.png)

As you can see from the image above, the lack of an explicit `return` implicitly returns `undefined`.  The only thing that changes is the value of the `sum` variable.  In this scenario, invoking the function will not return what we expect the function to return for us.    

# Conclusion
While the `return` keyword may not be necessary for the function to run and evaluate the way it was intended, not having it could give us some unintended and confusing results.  As with everything we do in code, follow best practices and explicitly use the `return` keyword to ensure you get the correct result you're looking for.  Ultimately, the trick is to understand what `return` is suppsed to do in the context of the function we are writing or using.
