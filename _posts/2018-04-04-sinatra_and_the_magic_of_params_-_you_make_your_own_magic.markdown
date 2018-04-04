---
layout: post
title:      "Sinatra and the Magic of `params` - You Make Your Own Magic"
date:       2018-04-04 06:25:48 +0000
permalink:  sinatra_and_the_magic_of_params_-_you_make_your_own_magic
---


When the methods we use seem to sprinkle a little bit of magic to make things happen, we become excited by the possibilities.  For me, `params` is one of those things that seem to provide a certain level of *je ne sais quoi*.  But, are `params` really magic?  

In the process of learning Sinatra and other frameworks, we have learned about methods that are available to us to help make our lives easier. It’s easy to take these methods for granted when you do not fully understand the purpose they serve. Admittedly, when I was first introduced to `params`, I didn’t understand the full scope of what `params` do for us.  Even after reading and researching and investigating, trying to make sense of `params` is not so simple.  `params` as a concept is cloaked in layers of mystery.  Once you’ve peeled away one layer, another one appears, further complicating my basic understanding of what it all means, what it does and where it comes from.  Just when you think you understand, you feel like you’re back at square one.  However, for the time being, I just want to make sense of `params` in the context of the little Sinatra application I’ve built - [my cars collection](https://github.com/yomi413/sinatra_project_final).

So, what exactly is `params`?  

In Sinatra, `params` is a method that renders a hash or a key/value pair that is encoded into our HTTP requests. Simply put our `params` hash can look something like this:  
	
	`params =  {:username => "mira", :password => "vacation"}`  

There are two basic ways that a `params` hash is used.  The first way is in the URL routes.  For example, when we add the following code to our application ...

![](https://i.imgur.com/WCqGQBU.png)

 
   ... the browser gives us this.

![](https://i.imgur.com/bvjAogS.png)


All this means is that we have tapped into the id value of 9 in our database satisfying a specific query; therefore, our page is giving us only information that pertains to this object as shown below.

![](https://i.imgur.com/rPGkzeX.png)


The second way that `params` is used is in the HTTP POST request.  The parameters established in the HTTP POST request, also referred to as POST data, is the information that a user will fill in through an HTML form.  In the example below we are defining the parameters we want our new object to have upon instantiation.

![](https://i.imgur.com/sysLhVh.png)


The HTML form itself is able to access the `params` keys through the name attribute.  The values that correspond to said keys will be the input from the user.

![](https://i.imgur.com/e7wpCTA.png)


In conclusion, through `params` we are given the power to produce dynamic code in our web applications.  In turn, this allows for our program to make proper connections and to establish a flow for how to write, read and apply good code.  I think that this is a good first step in beginning to understand `params` and what a powerful piece of code it is.  So is it magic?  Sure, we can think of it as magic, but in the end the magic only works if you know how to use it and the power it holds.  Happy coding!



