---
layout: post
title:      "How `var` Ruined My Life"
date:       2019-11-18 04:52:35 +0000
permalink:  how_var_ruined_my_life
---


Ok, I’m being a little dramatic and entirely hyperbolic with the title, but I have my reasons.  My life has not been ruined yet.  But, can we please have a discussion about why we are still using `var` in 2019?

In some JavaScript tutorials and lessons I’ve encountered, I still see `var` peppered throughout the material.  When I first encountered JavaScript, variables were solely declared using the `var` keyword.  By all accounts it seemed easy to have the single keyword to declare all variables.  There were probably limitations, I just didn’t know about because before I knew it `const` and `let` were being introduced to declare variables too.  Adding two extra declaratory keywords seemed fine until I started understanding that `const` and `let` served us much better than `var` could.  By allowing for very specific uses of each keyword we could write more code that flowed better.

While `const` is to be used to declare a variable that needs to remain constant throughout the life of your code, `let` allows for flexibility in our declarations.  With `const`, variables must be assigned a value upon declaration and the value cannot be modified. 

`const myName = “Yomaira”;          *// variable declaration and assignment*`

You can use `let` to declare variables that would need to be changed at some point in your code.  Variables that serve as counters, or variables initially declared as empty strings, can be declared using `let` for this very flexibility.  In addition, variables declared with `let` do not have to be assigned a value upon declaration. 

`let counter;           *// variable declaration*`

`counter = 1;          *// variable assignment*`

The above can also be written as follows using `let`:

`let counter = 1;          *// variable declaration and assignment*`

`const` and `let` encompass all that is right with variable declaration.  So what’s the problem?  The problem that I have (which is not really a problem, but more of a pet peeve) is that a lot of the JavaScript tutorials and learning materials out there still use `var`.  I understand that a lot of the tutorials have been in existence for a long time, before ES6 became the gold standard in JavaScript; therefore, `var` was the norm.  However, these learning materials should be updated to reflect the evolution of JavaScript.   

I have spoken to some programmers that argue that the reason `var` still exists is so that new programmers know what it is when they encounter legacy code.  Other people have argued that it’s because old browsers are more compatible with older JavaScript language conventions.  To a certain extent, these are understandable, but why must we all suffer for a 3-letter keyword that is not a viable part of modern JavaScript?  I really hope that things will start to change in the near future.  I don’t know if I can continue watching tutorials or reading lessons where `var` is still so heavily used to declare variables.  Please put `var` out of its misery once and for all.  I, for one, would really appreciate it.

