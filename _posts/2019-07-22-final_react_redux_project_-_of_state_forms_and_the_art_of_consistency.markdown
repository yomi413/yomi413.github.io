---
layout: post
title:      "Final React/Redux Project - Of `state`, `forms` and the Art of Consistency"
date:       2019-07-22 01:44:34 -0400
permalink:  final_react_redux_project_-_of_state_forms_and_the_art_of_consistency
---


We know that part of becoming a good coder is being detail-oriented.  You have to train your eyes and your brain to look out for the most obscure mistakes.  In my final [React/Redux project](https://github.com/yomi413/final-react-redux-portfolio-project) I set up a few forms for the entry of information.  Forms are pretty straight forward and innocuous, so what could possibly go wrong? 

In one form I had an entry that looked like this:

```
   <div className="form-group">
       <label htmlFor="certificate_of_occupancy">
             Certificate of Occupancy
       </label>
			 
       <input
         type="text"
         className="form-control"
         name="certificate_of_occupancy"
         placeholder="Certificate of Occupancy"
         onChange={props.onChange}
       />
   </div>
```

This one field appears properly structured, with no anticipated obstacles.  When we fill out the form, the field even appears welcoming.  However, upon submission of the form, the new building we are creating does not save at all.

![](https://i.imgur.com/SCZ56MQ.png)

The network returns a 422 status error, which indicates an unprocessable error.  In other words, the form submitted, but apparently there is missing information for that field. 

![](https://i.imgur.com/QgqQiVK.png)

I know I filled in the form correctly, so why is this error popping up?  After some testing and some trial and error, I had to consult with a mentor who made me look at the React console.  Remember that we were trying to fill out the field for `certificate_of_occupancy`?

![](https://i.imgur.com/D6yZ5IX.png)


The React console helped to provide some clues.  After looking at the list of properties in `state` we found our first clue.  Under state we have our property listed as `certificateOfOccupancy` in camel case.  However, the form is expecting `certificate_of_occupancy` in snake case.  So what’s the difference and why is our application making a big deal of this?  In short, `certificateOfOccupancy` and `certificate_of_occupancy` are obviously not the same thing.  It may not seem like a big deal, but our application is telling us that it doesn’t recognize the field as we structured it in the form.  In addition the React console telling what it does recognize.  

![](https://i.imgur.com/pTDKTHj.png)

The above image is listing both options under `state`, but only populating the snake case example.  The camel case option is remaining blank because we are not triggering the correct change to the `state`.  Let’s dive a little deeper into our code to make sure that we fix the problem.  

The piece of code that is handling our request is as follows:

```
class CreateBuilding extends Component {

state = {
   address: "",
   description: "",
   image: "",
   numberOfApartments: "",
   deed: "",
   mortgage1: "",
   mortgage2: "",
   satisfactionOfMortgage1: "",
   satisfactionOfMortgage2: "",
   certificateOfOccupancy: "",
   error: ""
 };


handleSubmit = event => {
   event.preventDefault();
   fetch("http://localhost:3001/buildings", {
     method: "POST",
     headers: {
       "Content-Type": "application/json",
       Accept: "application/json"
     },
     body: JSON.stringify({
       uid: localStorage["json.sessionUid"],
       address: this.state.address,
       description: this.state.description,
       image: this.state.image,
       numberOfApartments: this.state.numberOfApartments,
       document_attributes: {
         deed: this.state.deed,
         mortgage_1: this.state.mortgage1,
         mortgage_2: this.state.mortgage2,
         satisfaction_of_mortgage_1: this.state.satisfactionOfMortgage1,
         satisfaction_of_mortgage_2: this.state.satisfactionOfMortgage2,
         certificate_of_occupancy: this.state.certificateOfOccupancy
       }
     })
   }).then(() => {
     this.props.history.push("/user-welcome");
   });
 };
```


And herein lies the inconsistency of what our program is attempting to make sense of.  We told it to populate an entry for `certificate_of_occupancy` through the form, but we are requesting information for `certificateOfOccupancy` in `state`.  We originally declared the initial state as `certificateOfOccupancy`.  Since the goal is to change the `state` we have to ensure that any reference to this `state` is the exact same throughout.  The quick fix is to change the form to reflect how it should handle the `state` of our field.

![](https://i.imgur.com/0N70wmq.png)

Notice the React console above. Once we fixed the form we tested it in the browser.   The `state` of the field is now being correctly identified and populated as was always intended.  

The lesson here is to remain consistent throughout your application with your naming conventions.  Because I had used snake case in the development of my API the keys in my `json body` request had to reflect that reality.  However, because I had declared the `state` differently, I had to make sure that my user interface was consistent in its request and handling of information. 

In a nutshell, we have to be extra vigilant when dealing with applications that are making use of all kinds of data and moving pieces.  It is good practice to double-check and proactively investigate the seemingly minor problems that can plague our code and that eat away at hours of our time. Moral of the story: stay consistent.


