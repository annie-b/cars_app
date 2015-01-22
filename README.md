# cars_app
Create the infrastructure for your rails app by typing:

rails new cars_app --database=postgresql

cd cars_app
bundle install

Database creation and population:

The first thing we need to do is create a database of cars - Make, Model, and Year. To do this, type this at a command line:

rake db:create

(This will create an empty database)

ROUTER:

To get the “ROUTER” portion of the MVC working:

Open the file config/routes.rb and add:

get ‘cars’, to: ‘cars#index'

AFTER the Rails.application.routes.draw do line

CONTROLLER:

First, you need to create a file in app/controllers to hold the Cars class:

touch app/controllers/cars_controller.rb

Inside the cars_controller.rb file, type:

     class CarsController < ApplicationController

     # The index action (or method). This will be invoked to view all the products
     def index
          # This pulls the cars from the database and puts them into the @cars variable
          @cars = Car.all
     end

     end


This will create the CONTROLLER

Then you will need to create the VIEW. This is the file that translates Ruby language and sends it back to the client’s browser in HTML format.

mkdir app/views/cars
touch app/views/cars/index.html.erb


Then, we need to create the MODEL, which accesses the data in the cars table

touch apps/models/car.rb

(NOTE: This is a singular instance of cars)

Then, in the car.rb file, type:

     class Car < ActiveRecord::Base
     end

Once we have created the Car class in apps/models/car.db, we can populate the database with some car instances:

First, we need to create a Rails migration for cars:

rails generate migration CreateCars make model year
rake db:migrate

Then, we need to add some records into the database:

In db/seeds.db:

     Car.create(make: ‘Honda’, model: ‘Accord’, year: ‘2014')
     Car.create(make: ‘Mazda’, model: ‘Miata’, year: ‘1999')
     Car.create(make: ‘Volkswagen’, model: ‘Passat’, year: ‘2002')
     Car.create(make: ’Toyota’, model: ’Sienna’, year: ‘2012')

To create these records in the database:

rake db:seed

Change the VIEW to show the list of cars in ERB format:

Then, in the app/views/cars/index.html.erb file, type:

<h2>Cars</h2>
     <ul>
     <% @cars.each do |car| %>
     <li>Make: <%= car.make %>Model: <%= car.model %>Year: <%= car.year %></li>
     <% end %>
     </ul>


Launch rails:

rails server
