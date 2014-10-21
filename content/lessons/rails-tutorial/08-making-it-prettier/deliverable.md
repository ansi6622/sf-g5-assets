---
title: Rails - The Prettier Edition
bloom: remembering
---

# Goal: Make it Prettier

## Objectives:
* Learn about layouts
* Learn a little about Bootstrap
* Experiment with ERB and Layouts
* Create links to other pages in the app

------

## The App is UGLY. There are easy gems to make things a little better.

Remember at the very beginning of this project when we added an extra gem to our Gemfile?
It turns out, that it wasn't just to educate you about Gemfiles, we can use it
to quickly add some default styling.

Let's start by finishing the installation of the gem. While it comes out of the box
with code, many gems will also plug into Rails to add even more code to you app.
We want to install the static content (CSS & JS).

```bash
  rails generate bootstrap:install static
```

Also, before you start mucking around with CSS, let's delete the scaffold.css that Rails provides.
It will complicate our life in unexpected ways.

### Let's talk layouts

Layouts are the HTML containers for the more dynamic content that exists at each
path/route. The Rails default is at 'app/views/layouts/application.html.erb'. Let's go
look at it.

HTML pages have two big containers. One is the `<head>`. The content there is more meta.
It affects the way content looks, sometimes. But it is pretty rare to see content
embedded in the head tag. The one common exception is the `<title>`.

Let's experiment with changing the title:

```html
  <title>Todo - For Me!</title>
```

Now reload the page. Can you find that content?

The `<body>` is the other high level tag. It contains all the things
we typically see as content in a page.

In our case it only has some mystery tag: `<%= yield %>`.

We haven't talked about ERB, yet. Now is the time!

### Let's talk ERB

ERB is just HTML with Ruby embedded in it. You can tell which tags
have Ruby because they start weird, with a '%':

```html
  <% @collection.each do |n| %>
    <%= n + 1 %>
  <% end %>
```

All these tags contain ruby. The outer tags just have a '%', whereas the
inner tag also has an '='. That '=' is important. It means we will see the
printed out Ruby, not just do it.

So the outer tags are a loop that goes through each element in a
collection. The inner tag will print out a number that is the sum of
the item and 1.

### Back to Layout

But we haven't learned what this `<%= yield %>` tag is. Well, it is complicated
Ruby that has to do with blocks. It doesn't make much sense now, but what you should
know is that it is where the content from each dynamic page ends up!

To prove it, let's add some static text on either side of the `<%= yield %>`
tag.

```html
  <h1>Hello Page!</h1>
  <%= yield %>
  <h4>and Goodbye!</h4>
```

Go to different areas in the CRUD. Notice how the main content changes, but those
statements stay the same.

# Rebuilding that Layout

Getting back to our fancy, pretty making gem, let's use it to replace the
existing layout.

```bash
  rails generate bootstrap:layout application
```

It is going to ask if you want to overwrite the existing application.html.erb layout. Say yes, or 'Y'.

Check out the joy! Click around your CRUD.

### What just happened?

Let's checkout the 'app/views/layouts/application.html.erb' file.
A lot has changed. Now there is a lot more content in both the head and the body tags.

Take a tour of the new body content.

* Where is the tag responsible for that 'Todo' link in the top bar?
* Where are the links in the Sidebar?

### Making it our own

1. Find that Todo link and change the href to '/'. In that way, no
matter where we are, when we click on it we will go back to the home page.
2. Let's remove the other top navigation links. Our app isn't that complicated,
and we just don't need the clutter.
3. Next we need a way to get to our projects and our tasks to do CRUD. Let's
change the Sidebar to contain that data:
    1. Change the h3 content 'Sidebar' to 'Navigation'
    2. Remove the li tag, with the content 'Navigation'. Our life just isn't that complicated.
    3. Change 'Link1' to be 'Projects'
    4. Change 'Link2' to be 'Tasks'
    5. Change the "/path1", to be "/projects"
    6. Change the "/path2", to be "/tasks"
    7. Remove the tag for 'Link3'
4. Let's change the company name to 'gSchool, Cohort 5'

### One last thing

Go check out your task form via the sidebar 'Tasks' link. It got messed up when we removed
the scaffold.css file. The project form has the same issues.

What can we do to make it better? Currently in forms, the `<div>` wrapping
each set of label and input has a 'field' class. The scaffolding provided that.
We can change it to use the Bootstrap equivalent 'form-group'.
Then things are spaced better again.
