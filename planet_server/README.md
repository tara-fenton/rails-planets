# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...


# Rails Planet Server
_Introduction_

In this exercise we will practice defining routes and controller actions in Rails

#### Deliverable
The "finished" state of this lab should be a rails app for creating and viewing planets
	- The `Planet` resource should have a `name` field, a `num_moons` field, and a `color` field
	- There should be working routes for viewing all planets, creating a planet, and viewing one planet

## Setup

- in terminal, navigate to the directory where you store projects
- run `rails new planet_server --api -d postgresql -T`
- `cd` into the directory
- run `rails db:setup` and `rails db:migrate`
- Finally, spin up the server with `rails s`

## The Routes + Controller

Inside `config/routes.rb` use `resources` to declare RESTful routes for `planets`.  Verify that the routes have been created using `rails routes`

Either by hand or using the generator, create the boilerplate for a `PlanetsController`.

Go ahead and write actions for `index` and `create` that return dummy responses.  Verify that at least `index` works, e.g., using the browser, curl or insomnia.

## The Model

- Generate a Rails model for `Planet` and fill out the migration file.
- run `rails db:migrate`
- open up the rails console with `rails c` and create a few planets from the console using `Planet.create!`

## The `index` Route

Now head back over the `PlanetsController` and properly implement the `index` route.  Remember, you can just use the `Planet` model directly in the controller without having to import or `require` anything.

You can render a json response with `render json: <data>`.

## The `create` Route

- First, write a `planet_params` helper method that calls `require` and `permit` appropriately on the params hash
- In the `create` method, use `planet_params` to gather the form data from the request and pass it to `Planet.create!`
- Return the newly created planet resource

Try to write a scratch axios script to test out the `create` action.  If that feels like overkill, test the `create` action using insomnia

## The `show` Route
  Implement `show` by extracting the `id` for the planet to be shown from the `params` hash, fetch the correct Planet from the db and then return it to the client using json.

## Bonus

- Implement the `destroy` and `update` actions
- Write a simple React front end for the app that can list and create new planets.

To enable `cors` in the Rails server, use the [rack-cors gem](https://github.com/cyu/rack-cors).

And include the following in `config/application.rb`

```ruby
config.middleware.insert_before 0, Rack::Cors do
      allow do
        origins '*'
        resource '*', headers: :any, methods: [:get, :post, :options]
      end
    end
```
