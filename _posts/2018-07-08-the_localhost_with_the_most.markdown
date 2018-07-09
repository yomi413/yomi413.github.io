---
layout: post
title:      "The `localhost` With the Most"
date:       2018-07-09 03:28:39 +0000
permalink:  the_localhost_with_the_most
---


In the process of creating my final Rails project, I encountered a situation that was unexpected.  I thought I was on a roll while trying to implement omniauth authentication credentials for a Google strategy.  My code was correct (confirmed by references found online), and all of my files from `config/initializer/omniauth.rb` to the `route.rb` file to the `.env` file, seemed to have lined up quite nicely.  Then, I tried to log in to my application using omniauth authentication.  Well, let's just say my confidence took a nosedive.

I got the following error message when I attempted to log in using Google.

![](https://i.imgur.com/EckqAEf.pnghttp://)

Huh?  I looked at my code again, checked the list of whitelisted URIs, and read up on what could possibly be creating this mini crisis for me.  Nothing seem to make sense.  I felt stuck.  I even tried changing my code and resetting my databases.  I became desperate and my reactions became unnecessary and extreme (all of which I will address at a later date).  One afternoon, I happened to be on the phone with my brother.  Disclaimer: He’s a software engineer.  When I explained the problem I was having he suggested something so obviously simple that I felt embarrassed that I hadn’t seen it sooner.  

So here is the problem - when we open our application using the http://0.0.0.0:3000 URI, there shouldn’t be anything impeding our application from opening and being used.  I did just as I had done prior to adding the Google strategy to my application.  

![](https://i.imgur.com/ge8zRKA.pnghttp://)

However, when using omniauth authentication we are not able to whitelist http://0.0.0.0:3000.  When trying to whitelist this URL with the Google strategy it sends us a message that the action is invalid (see below).

![](https://i.imgur.com/Tx8CeyZ.pnghttp://)

The simple solution that my brother the engineer suggested was to use http://localhost:3000 when opening my application.  If you see the whitelisted URIs in the image above, it happens to be the very first URI listed.  It all made sense!  As soon as I made that change, the application worked smoothly and I was able to log in using my newly implemented omniauth authentication.  

In conclusion, while http://0.0.0.0:3000 and http://localhost:3000 tend to be used interchangeably, omniauth authentication adds another layer of unexpected results.  Please note that this was my experience with the implementation of the Google strategy, but I have not tested this theory with any other strategies such as Facebook, GitHub, etc.  For future projects I will test both URIs and see if there are any differences to point out.  In the meantime, I will continue to use http://localhost:3000 and hope to avoid any future problems.  

