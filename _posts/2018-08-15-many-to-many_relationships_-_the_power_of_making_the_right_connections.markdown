---
layout: post
title:      "Many-to-Many Relationships - The Power of Making the Right Connections"
date:       2018-08-15 01:55:00 -0400
permalink:  many-to-many_relationships_-_the_power_of_making_the_right_connections
---


Of all the options Rails gives us to make associations between models, the ones that have intrigued me the most in recent weeks have been many-to-many relationships.  There are two ways to declare many-to-many relationships - `has_and_belongs_to_many` and `has_many :through`.  So, what’s the difference between the two methods?  How do we choose one method over another?

# `has_and_belongs_to_many`

According to the [Rails Guides](https://guides.rubyonrails.org/association_basics.html#choosing-between-has-many-through-and-has-and-belongs-to-many), the `has_and_belongs_to_many` association is the simpler of the two methods and allows for associations to be declared directly.  A third table, designed to be the join table that will connect our associating tables, must be included.  It will usually only contain the foreign keys of the connecting tables. 

To help me demonstrate how our structure would work, below are the migrations and models we used in our simple application for a cars collection - `cars`, `drivers` and  `cars_drivers`. 

```
class CreateCars < ActiveRecord::Migration[5.2]
 def change
   create_table :cars do |t|
     t.string :make
     t.string :model
     t.integer :year
     t.timestamps
   end
 end
end
```

```
class CreateDrivers < ActiveRecord::Migration[5.2]
 def change
   create_table :drivers do |t|
     t.string :name
     t.timestamps
   end
 end
end 
```

```
class CreateJoinTableCarsDrivers < ActiveRecord::Migration[5.2]
 def change
   create_join_table :cars, :drivers do |t|
     t.index [:car_id, :driver_id]
     t.index [:driver_id, :car_id]
   end
 end
end
```

The migrations for the `cars` and `drivers` tables are simple and straightforward.  They don’t contain any foreign keys.  The migration for the join table, `cars_drivers`, uses the `create_join_table` method to set up this type of join table.  Following the `create_join_table` method are the individual names of each of the tables we want to connect.  By setting up the migration this way, and without much more interference, Rails will automatically connect our tables, and our associations will be properly declared. Awesome!

Not so fast, though.  We have to set up our models so that the `has_and_belongs_to_many` method can be used in our application.  See our models below.  The declarations are made directly without the use of the third model because of the simplicity that this method offers. 

```
class Car < ApplicationRecord
   has_and_belongs_to_many :drivers
end
```

```
class Driver < ApplicationRecord
   has_and_belongs_to_many :cars
end
```

# `has_many :through`

The second method for declaring a many-to-many relationship is the `has_many :through` method, which could be more complex in structure.  However, complexity is not necessarily a bad thing.  

Very much like the `has_and_belongs_to_many` method, the `has_many :through` method will require the use of a third table that will hold the foreign keys.  However, unlike the `has_and_belongs_to_many` method, the `has_many :through` association will require a third model.  The third table will probably also be used to hold other relevant information pertinent to the application. 

Using our previous example, let’s change our structure a bit.  Rather than use the `cars_drivers` table (which doesn’t tell us anything significant about the application we are trying to build), we want to include a new table that gives our application a better flow.  Let’s add a `parking_spaces` table.  Cars, drivers, parking spaces - these things make sense together. 

Our migrations now look something like this…

```
class CreateCars < ActiveRecord::Migration[5.2]
 def change
   create_table :cars do |t|
     t.string :make
     t.string :model
     t.integer :year
     t.integer :parking_space_id
     t.integer :driver_id
     t.timestamps
   end
 end
end
```

```
class CreateDrivers < ActiveRecord::Migration[5.2]
 def change
   create_table :drivers do |t|
     t.string :name
     t.timestamps
   end
 end
end
```

```
class CreateParkingSpaces < ActiveRecord::Migration[5.2]
 def change
   create_table :parking_spaces do |t|
     t.integer :space_number
     t.timestamps
   end
 end
end
```

… and we want our models to show the following associations.

```
class Car < ApplicationRecord
   belongs_to :driver
   belongs_to :parking_space
end
```

```
class Driver < ApplicationRecord
   has_many :cars
   has_many :parking_spaces, through: :cars
end
```

```
class ParkingSpace < ApplicationRecord
   has_many :cars
   has_many :drivers, through: :cars
end
```

In this structure, we are using the `cars` table as our join table.  Since we want to show that a driver has many parking spaces through cars, then our `cars` table will hold the foreign key for parking space (`parking_space_id`).  In addition, we also want to show that a parking space has many drivers through cars.  Once again, our `cars` table will hold the foreign key for driver (`driver_id`).  Finally, in order to complete our associations and make the full connections, the `car` model will need to show that it belongs to a parking space and that it belongs to a driver.  The `has_many :through` association allows for our connections to be made indirectly through the third model, which allows for a more complete use of all tables and models we are creating in our application.  

## Which is the best option?

Ultimately we (the programmers) would have to decide which approach works best for our application.  In an effort to keep our code clean, DRY and skinny, we should only use what we need.  Neither option is wrong, but there is a clear favorite.  My own personal preference is the `has_many :through` association because it gives us the best option for developing dynamic code for ever-changing applications.  The majority of applications today are constantly growing and innovating based on the needs of their users.  I think the `has_many :through` method offers more flexibility, while a `has_and_belongs_to_many` method might assume a more static structure.  We live in a world full of connections and overlaps.  The least we could do is design our code to reflect life itself.
