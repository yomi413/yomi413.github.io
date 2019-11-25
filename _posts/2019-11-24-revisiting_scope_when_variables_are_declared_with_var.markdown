---
layout: post
title:      "Revisiting Scope - When Variables Are Declared With `var`"
date:       2019-11-24 23:55:58 -0500
permalink:  revisiting_scope_when_variables_are_declared_with_var
---


![](https://i.imgur.com/GtwPCi5.gif)



I promise I’m okay after last week’s post.  [`var` has not ruined my life](http://yescano.com/how_var_ruined_my_life).  I still think we should not use it at all, but I think I have to provide a better reason for getting rid of `var` than “I don’t like it”. The post I wrote last week was primarily based on my own frustrated opinion of the use of the `var` keyword in JavaScript tutorials.  Some tutorials would explicitly say don’t use `var`, but then use `var` in all of their sample code and only provide tests that require the use of `var` to pass their specific lab tests.  Even I’m guilty of this!  

In a [blog post](http://yescano.com/how_understanding_scope_and_hoisting_are_fundamental_to_learning_javascript) I wrote a few months ago I used `var` throughout the article to get my point across.  In my defense, that article was more about scope and hoisting in general and not so much about the proper use of each type of declaratory keyword.  So, what is it about `var` and scope anyway?  Why is it that I advocate for the discontinuation of the use of `var` and what does scope have to do with it?  Let’s discuss.  

**`var` and Scope**

While the `var` keyword allows for easy global and function declarations, the `var` keyword is indifferent when it comes to declaring variables within a specific block scope.  

```
**// Global Scope**

var myFirstName = "Yomaira";
var myLastName = "Escano";
 
function myName() {
 console.log(myFirstName, myLastName);
}

myName();  // prints Yomaira Escano to the console
```



```
**// Function Scope**

function myName() {
 var myFirstName = "Yomaira";
 var myLastName = "Escano";
}
 
console.log(myFirstName, myLastName); // Uncaught ReferenceError: myFirstName is not defined```



```
**// Block Scope**

function myName() {
 var names = ["Ana", "Tina", "Ben"];
 
 for (var i = 0; i < names.length; i++) {
   var name = "Daniel";
 }
 console.log(name);
}
 
myName(); // prints Daniel to the console
```


As you can see in the example directly above, a variable declared within a loop, switch statement or conditional statement belongs to the function where it is declared.  Why is this important?  

In our effort to put out good, clean code, we should strive to be intentional with every line of code we write.  When declaring variables, the `var` keyword is fine and does its job, but we want to make sure that our variables are defined within the proper context for their use.  In simple pieces of code, using `var` over `const` or `let` might not matter much.  In a controlled environment where you are the sole author and maintainer of every line of code, it’s easier to keep track of your variables, where they’re defined and how they’re being used.  However, in large projects with multiple authors and maintainers you need to use keywords that can easily throw up errors and allow for easy debugging.  

**Are all variables meant to be reassigned?**

The simple answer is no.  There are instances where you want and need certain variables to remain constant.  The volatility of the `var` keyword does not allow for keeping track of variables that were meant to be constants.  Being able to unknowingly overwrite variables could be chaotic and confusing when attempting to write good, working and DRY code. 

**Conclusion**

I know I’ve written a lot about this topic and I promise to move on.  I keep coming back to it because it is complicated to understand the declaration of variables, especially when you have different keywords that allow for similar functionality.  However, the more I dive into this topic the better I understand how something as minute as properly declaring variables can affect my entire code. 

