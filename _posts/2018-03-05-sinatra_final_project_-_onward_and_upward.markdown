---
layout: post
title:      "Sinatra Final Project - Onward and Upward"
date:       2018-03-05 14:46:33 +0000
permalink:  sinatra_final_project_-_onward_and_upward
---


For our final Sinatra project we were supposed to pick a collection of something we care about and build a CRUD (Create, Read, Update, Destroy) application that incorporates as many of the lessons that we learned in the SQL/Rack/ActiveRecord/Sinatra section. Since my daughter had a lot to do with my CLI Gem Project, this time I picked something that my son is obsessed with - CARS.  Blame it on the Disney Cars Trilogy or the fact that he loves any and all cars, but I thought it would be cool to create an application that would allow users to create a collection of their vehicles.  I would imagine that eventually this type of collection could be useful for someone in the rental car business or some kind of ride sharing service or someone that just likes to collect cars.  In any case, this could be built upon if necessary and would give me a good foundation for a future project. 

Back to the business at hand:  There was a lot going on in this section, from learning about building databases, erb templating, authentication, validations, and building MVC file structures to implementing Ruby logic learned through the fundamentals, HTML, learning about new Ruby gems, etc., etc., etc.  With all of this information to make sense of, there were some parts that I loved more than others, but I guess that’s a very normal part of learning a new subject matter.  

The one thing I really enjoyed about learning Sinatra was seeing how the code I wrote translated to HTML.  Although my own small application is very primitive, it is fascinating to see my code in action and how each line interacts with the next.  I loved seeing how building a helper method such as `logged_in?` helped to make my code flow...

```
helpers do
    def logged_in?
      !!current_user
    end

    def current_user
      @current_user ||= User.find(session[:user_id]) if session[:user_id]
    end
  end
```
	
```
class CarsController < ApplicationController
use Rack::Flash

get '/cars' do 
	@user = User.find_by(id: session[:user_id])

	if logged_in?
		erb :'/cars/cars'
	else
		redirect to '/login'
	end
end 

get '/cars/new' do
	@car = Car.find_by(make: params[:make])

	if logged_in?
		erb :'/cars/new_car'
	else
		redirect to '/login'
	end
end
```
	
… or how using a single line of code such as `validates_presence_of` can ensure that the user always fills in the blanks.


```
class Car < ActiveRecord::Base
  belongs_to :user
  validates_presence_of :make, :model, :year
end
```


As I tie up my final project in the Sinatra section, I can’t help but be in awe of this little thing we call the web.  In 2018, we can’t imagine life without the internet and access to all the applications that are available to make our lives easier.  In the short time the web has been part of our human history, it has single-handedly become one of the most important tools in our arsenal for gathering and disseminating information. In the 10+ months that I have been coding I realize that I will never know everything there is to know about the internet, but I can definitely learn to build good, functional and working applications.



