# Goal: New up a Rails app. Add some gems.

## Objectives:
* Learn about `rails new`
* Learn about Gemfiles and using bundler to install those gems.
* Understand localhost, servers and where to see your app.

-----------

## Rails is big. How do we start? What's the first step?

Rails can be compared to a cake mix. You can get a lot by just adding water.
We don't have to grow wheat and then mill it. We are just going to pull a
box of cake mix off the shelf, buy some frosting and paper plates to eat
a great dessert.

* Think of your Gemfile as a shopping list.
* Bundler does your shopping for you.

## Let's See How That Works

#### Make a new rails app

```bash
  rails new todo
```

#### Open the app in atom, your editor

Let's look at that in atom:

```bash
  cd todo
  atom .
```

There are lots of files! Let's not get overwhelmed.

#### The Gemfile!

We will just look at the Gemfile.

Add this line ... all the way at the bottom:

```ruby
  gem "bootstrap-sass"
```

What is Bootstrap? [Bootstrap](http://getbootstrap.com) is like the icing on the cake. It gives CSS styling
defaults that look good. It also gives some JavaScript niceties (that we won't use).

#### Bundling

```bash
  bundle
```

What just happened? Bundler did your shopping. It went to rubygems.org
and downloaded the latest version of the library so you can start using it
in your application locally.

#### Fire up the application server

We built an app with `rails new todo`. We can see the code using atom. We
can get libraries with bundler. But what we really want is to see our web server running!

You can do that on the command line:

```bash
  rails server
```

Go to [localhost:3000](localhost:3000). This is the out of the box welcome
screen that Rails gives you.

## Now let's do it together

Everyone get to the point where you can see the Rails welcome screen. Once we are all there, we can move along-
have an instructor or TA help if you get stuck.
