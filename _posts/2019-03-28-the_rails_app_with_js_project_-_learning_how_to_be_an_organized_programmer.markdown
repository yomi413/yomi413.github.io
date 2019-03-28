---
layout: post
title:      "The Rails App with JS Project - Learning How to Be An Organized Programmer"
date:       2019-03-28 18:40:23 +0000
permalink:  the_rails_app_with_js_project_-_learning_how_to_be_an_organized_programmer
---



In this final Rails App with JavaScript project, having a fully working Rails application gave me a lot of confidence that the next project wouldn’t be so bad.  Before I started this final project, I had somehow convinced myself that it would be easier than all other projects.  For starters, I wasn’t starting something from scratch.  I had what I thought to be a really good foundation in my Rails application.  It is not a perfect project, but good enough that implementing some JavaScript functionality should not break my project... or my brain for that matter.  Despite my inflated sense confidence, I struggled with organization and setting myself up for success. 

Once I started to look at my final Rails project more closely, I had no idea where to begin.  ***Which file should I add first?  What should I delete?  Should I look at the Gemfile?***  I would love to tell you that like a scene from *The Matrix* I was able to download into my brain the perfect code to a perfect solution.  Well, not quite.  I started touching too many files at the same time - messed with the controllers, created serializers, created my `.js` file, messed with the `html` files before knowing what to change in them.  Nothing was working, and my frustration and anxiety were through the roof. There was no rhyme, reason, or cohesion to my thought process.  I just wanted something to work!

Eventually, I realized how messy I was being.  I needed to take a step back and give myself more structure.  I decided to stop and start again with a more organized approach.  I wanted to have a better understanding of what to do rather than just creating or deleting files.  Below is how I rethought my process.  This really helped me put things in perspective.   

1. **Organize my thoughts** -  I read the project instructions and requirements over and over.  Despite having read them countless times, I couldn’t figure out where to begin.  While the instructions actually don’t tell us where to begin, they do give an idea of how to set up a blueprint for next steps.  Once I started to write things down I realized that I should focus on the following routes in my project:
 ```
 cars  GET  /cars(.:format)  cars#index
 
 car  GET  /cars/:id(.:format)  cars#show
 
 new_car  GET  /cars/new(.:format)  cars#new
 
          POST  /cars(.:format)  cars#create
 
 user  GET  /users/:id(.:format)  users#show
 ```
 These routes relate directly to each of the requirements in the project instructions.  Now that I had this on paper I was able to focus my attention on these routes and their respective entries in the controllers and `html` files.

2. **Updating the Gemfile** - When I completed my Rails application it was working perfectly.  However, I had recently received a couple of notifications that a handful of my dependencies were presenting a high severity security vulnerability.  I had no idea what that meant.  After taking some time to look through my `Gemfile` and doing some research on the quickest and cleanest way to fix the problem, I found that all I needed to do was add `gem ‘sqlite3’, ‘~> 1.3.6’` and then run `bundle update`.  Luckily, this was an easy fix.  Now that the my Rails application was fixed I could move on to recreating it for my new Rails App with JavaScript Frontend project.

3. **Understanding the Gemfile** - Looking at the `Gemfile` without knowing what gems are needed can be daunting.  In reality even reviewing the Gemfile in its current state may not give you any clues as to what gems will come in handy for any particular project.  I did, however, know that I wanted to use serializers and jQuery to write the new code.  I added `gem ‘active_model_serializers’` and `gem ‘jquery-rails’` to the `Gemfile` and then ran `bundle install`. It wasn’t immediately apparent if any other gems would be necessary, but I knew I would discover it as I went along.  

4. **Looking at the js manifest** - Obviously, the more code we need the more files will be necessary as well.  In the js manifest, which can be found in the `app/assets/javascripts/application.js` file, we are requiring the necessary JavaScript files that the application will need.  For purposes of this project, I didn’t have to add any specific `js` files because all of the files in the `javascripts` folder are being loaded with `//= require_tree .`.  The only addition to the manifest was `//= require jquery`.

5. **Build one piece at a time** - This bit of takeaway is really obvious.  However, what piece should be built first?  Since my serializers would only be used to hold attributes and to make associations to connect the `json` serializers, it made the most sense to start here.  Someone else might find it more useful to start with the controllers since we need to ensure that we are rendering `json` properly.  This may come down to a personal choice.  Lastly, building out the `js` file and making necessary changes to the `html` files will come once we have those other foundational items done.  This is not to say that we won’t be revisiting all files to double-check our work.

6. **Refactor** - As we've learned in this coding journey the most important thing is to get the code we write to work.  Once I had good working code I started to refactor.  Initially I had a single `cars_users.js` file that contained all of my new code, including `AJAX 'GET'` and `'POST'` requests and classes.  As this file continued to grow, it was making me a bit nervous that something somewhere would get messed up.  Separating the classes out from the `AJAX` requests made a lot of sense.  

As stated above, the goal is to have a working application.  I’m sure that more experienced programmers will have their own perspective on how they approach a project.  I truly believe that there are multiple ways to solve a problem.  Ultimately, we all have to find our own path.  Going forward, I will need to follow this or a similar blueprint to ensure a successful outcome.  As I gain more experience in this field this type of organization should become second nature, and I can’t wait for that day to come.  

