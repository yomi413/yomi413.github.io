---
layout: post
title:      "Building My First HTML Email Newsletter"
date:       2019-12-08 23:32:02 -0500
permalink:  building_my_first_html_email_newsletter
---


Prior to my foray into learning about all things technology, I hadn’t given much thought to our everyday interactions with some of the technology we use everyday.  Email is one of those things.  While the majority of the emails we receive or send involve basic text, we also sign up for newsletters from our favorite publications or retail stores.  Focusing on said newsletters, let’s talk about how those cool email newsletters are generated.  

## The Code Behind It All

Email newsletters are just something I passively interact with, solely as a consumer of them.  I had not considered what it takes to put it all together.  A lot of the modern email newsletters we get today look like attention grabbing mini web pages designed to appeal to us.  If they look like mini web pages, are they built like web pages? 

In simplest terms, the answer to our question is yes.  Web pages and email newsletters use HTML and CSS.  However, the majority of modern web pages use a heavy dose of JavaScript to allow for user interaction.  Email newsletters are basic in structure using table layouts in order to keep things organized.

> <iframe height="265" style="width: 100%;" scrolling="no" title="Email Newsletter (Header)" src="https://codepen.io/yomi413/embed/MWYKyJO?height=265&theme-id=default&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/yomi413/pen/MWYKyJO'>Email Newsletter (Header)</a> by Yomaira Escano
  (<a href='https://codepen.io/yomi413'>@yomi413</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


Looking at the piece of code on the left you see at least two `<table>` tags, one nested inside another.  This code is straight-forward, giving us the layout for the small header introducing the newsletter (see result on the right). 

The reason why tables are used is that they provide a good layout that easily translates throughout all major email platforms.  Additionally, most email clients do not support the `<div>` that most developers prefer to use when building the modern web page.  

Looking at another part of our email newsletter you can see the dominant table layout throughout.  But another major part of the structure of this code is the inline CSS code included inside our HTML.  The tables provide for clean lines and division of space, but the added style attributes allow for the beautification of the newsletter - color, fonts and spacing to name a few of the properties that can be manipulated.  See the code below with its accompanying result.

> <iframe height="265" style="width: 100%;" scrolling="no" title="Email Newsletter (Header &amp; Bronx)" src="https://codepen.io/yomi413/embed/qBEbZPg?height=265&theme-id=default&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/yomi413/pen/qBEbZPg'>Email Newsletter (Header &amp; Bronx)</a> by Yomaira Escano
  (<a href='https://codepen.io/yomi413'>@yomi413</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## Conclusion

For all the talk about writing and maintaining DRY code and separating concerns by have separate files for separate pieces of code, it's worth noting that there are always exceptions to the rule.  Email newsletters seem to be that exception.  The development of email newsletters may seem to be stuck in a different time.  In some ways they are, what with using only HTML and CSS to build them.  But they work.  They fulfill their sole function of keeping us in the know about anything and everything.  Building my first email newsletter was fun.  I really had no idea that there are developers out there solely dedicated to building something we really don’t always pay much attention to.  We all see them.  Now let’s admire them for a little longer and appreciate what it takes to put them together. 

