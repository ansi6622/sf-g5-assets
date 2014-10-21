# Goal: Understanding Routing

## Objectives:
* Route home page to new content
* Learn to build a static HTML page
* Introduction to ERB, an HTML templating language
* Recognize a controller
* Introduce server errors, and info that we can glean from it

-----------

## No one is going to pay for the Rails welcome. What can we do?

<img src="http://www.cheznadia.com/wp-content/2010/04/switchboard.jpg">

You know those old fashioned notions of switchboards, connecting an
incoming call to a phone somewhere. In our case we are connecting incoming
requests to a controller and view.

#### Change your routes!

* Go to atom and find a file routes.rb. It is in the directory called 'config'.
* Change line 6, which is commented and says: `# root 'welcome#index'`
  * uncomment it!
  * change the word 'index' to 'home'
* Start the server and check it out

What happened? What is the server trying to tell you?

#### Create a controller

* In the 'controllers' directory, create a new file called 'welcome_controller.rb'
* Don't restart the server, it's fine.
* Reload the page. What is the message now?
* Autoload errors mean that Rails found your file, but can't find the expected class.
* Add this code:

```ruby
  class WelcomeController < ApplicationController
  end
```

* Reload the page. Now what???

#### Write an action

The 'home' in routes is the name of an action, or controller method. Let's build an empty one,
and see what happens.

```ruby
  def home
  end
```

Reload the page. What is the error message telling us now? It looks like it is time to finally write some
HTML.

#### Make a view

* In the 'views' directory. Add a 'welcome' directory.
* In that new 'welcome' directory, make a new file called 'home.html.erb'
* Open it and add `<h1>Hello World</h1>`
* Reload the page and check out your new home page

## Now let's do it together
