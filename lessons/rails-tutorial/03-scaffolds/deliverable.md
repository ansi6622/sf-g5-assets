# Goal: Rails Scaffolding

## Objectives:

* Learn about the quick and dirty of scaffolds
* Overview of CRUD on resources
    * Create
    * Read
    * Update
    * Delete
* Introduction to
    * Models
    * Databases & Migrations

-----------

## Creating, Reading, Updating & Deleting: What Rails Does Easily

If your server is still running, shut it down: `ctrl-C`.

Let's review our working app. Check out all that CRUD. We get it with just a few
drops of water with scaffolding.

Let's try working with scaffolding:

```bash
  rails generate scaffold projects name:string
```

#### Run the Server

If you stopped your server, start it up again with `rails server`.

Go to the browser, same great home page.

What went wrong?

#### Migrations & Databases

Part of what scaffold built for us was a database migration. Let's go check out
that migration file. It is located at 'db/migrate/XXXXXXXXXX\_create\_projects.rb',
where all those Xs are actually a timestamp in numbers.

Inside the file you should see this:

```ruby
  create_table :projects do |t|
    t.string :name

    t.timestamps
  end
```

Ruby is very English-y. What it is trying to tell us is that it is creating a
database table named 'projects'. It has a column in that table named 'name' that
is a string. It also added something called timestamps, that we don't need to worry
about right now.

Let's run the migration, just like it told us to:

```bash
  rake db:migrate
```

#### Models

Scaffold also created a model named 'Project'. The file is located in the 'app/models'
directory. Models are like the connective tissue between your Rails code and the
database. There isn't any code in the model right now. It is just connective tissue right now.


#### Routing Changes

Scaffold also changed our routes. If you open that file again, you should see at the very top a
new line:

```ruby
  resources :projects
```

What's this about? This is the part of the cake mix that maps URLs to controller actions.
That's a little abstract. Why don't we check out what all the routes look like now? There is a
command line utility that comes with Rails that prints out all the routes.

```bash
  rake routes
```

Notice how there are a ton of paths now that go to the projects controller. Plus we still have that
one route we made to the welcome controller.

#### A New Controller

Scaffold generated a new controller for us 'app/controllers/projects_controller.rb'. It is HUGE!
Do not get intimidated. One day soon you will understand all of it.

Notice that on top of each method there is a comment noting the path that the route uses. Also, the
name of each method is what we saw listed in `rake routes`.

Notice that some of the methods are empty, which means all the interesting stuff is in the view. In some,
there is lots of code and we are doing lots of work.

#### Views Galore

Go to the views directory: 'app/views'. You will see a new directory in there called 'projects'. Inside that
directory, you will see a whole bunch of new views in 'html.erb' format.

Check out a couple of these before running the server to see it all in action. The '_form.html.erb' has some
interesting stuff.

#### See it in action

Run the server if you stopped it: `rails server`. Now that we have migrated. Everything should be working.
You can see your projects in all their CRUD glory at '/projects'.

## Now let's do it together
