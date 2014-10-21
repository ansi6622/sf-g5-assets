---
title: Rails - More View Work
bloom: application
---

# Goal: Make the App more useful with more informative views

## Objectives:
* Craft your own ERB
* Work with associations to present related data in the view

## Now that the App looks better, we want to make the view match what we expect from our data

Even though we allegedly have a to-do app, we don't have any to-do lists.
Wouldn't it be great if we could see all the tasks on the project when we looked
at the project? Let's do that.

Let's go to our GUI and see what we're working with. Go to your projects index
page: '/projects'. Next click on any project. This is the 'show' page which has
a path '/projects/:id'. That is the 'Read' part of CRUD. This is where we would like
to see our tasks.

### Making the Project detail better

The view related to this is 'app/views/projects/show.html.erb'

Find the ERB tag that has the project name. Right under that we would want to add a list
of tasks for that project.

Recalling from our lesson on the console, we can get to our project's tasks by calling `project.tasks`.

Also, we want to iterate through each task and make some HTML for the task.

Type this code, don't copy, underneath the 'p' tag that wraps the project name.

```html
  <% @project.tasks.each do |task| %>
    <%= task.name %>
  <% end %>
```

Go check it out. This kind of worked, but we didn't add enough tags around each task to
separate it from other areas of the page. The links got all glommed on to the back :(

Take 2:

```html
  <% @project.tasks.each do |task| %>
    <%= task.name %><br>
  <% end %>
```

Ok, not bad. But we can do better.  Remember the navigation links from our application layout? Those were
wrapped in `<li>` tags. HTML gives us all sorts of handy tags for organizing our documents, and `<li>` is super handy
for lists.  But you can't just through `<li>` tags out there on their own. We need to put our `<li>` tags inside
`<ul>` parent tags.  Let's do it.

```html
<ul>
<% @project.tasks.each do |task| %>
  <li><%= task.name %></li>
<% end %>
</ul>
```

Hey look at that! That is so much better than using the `<br>` tag. With the `<li>` tag we got a little bit of indentation,
as well as a little bullet mark.

It turns out that Bootstrap, our CSS upgrade library, comes with some great list formatting. Adding
a few classes will give us totally different styles.

Check it out in your browser. It looks great!

We can make this page just a little bit better. What if we were a little less wordy with the name
of the project. I think we could just have the name as the headline, bigger!

Find the tags that wrap the project name. Notice how they are `<p>` tags. Let's change them to `<h2>` tags instead.
That is pretty big, but still very wordy and confusing. Find the section that has the 'Name:' labeling,
and delete it.

### Upgrading the Task Area

We did a pretty good job of showing off our projects with tasks, but the task area is not very
intuitive. When we click on the 'Tasks' link in our Navigation sidebar, it brings us to a pretty
useless list. It turns out that when you just add water with our scaffold cake mix, you get lots
of useless stuff. In reality our problems don't map so easily to index, show, edit and delete. In
our case, we would like to use that link to go straight to the task creation form.

We can do that pretty easily by changing the navigation link. Do you remember where that is?

Let's change this list item link:

```html
  <li><%= link_to "Tasks", "/tasks/new"  %></li>
```

Woot! Getting better every change. We are almost getting paid!

### Back to Projects; This time the project list.

The headline is kind of lame. We can see it is a list, but it doesn't yet look like a list. I bet
we could use the same styling that worked so great in tasks. Let's try it.

Where is the view located?

Let's change the headline first, since it is easy to find on the top. We will remove 'Listing'.

```html
  <h1>Projects</h1>
```

Now we have a bigger problem. If you look down the page, we can't find our list tags at all. There
is a table. It turns out tables as a way of presenting lists went out of style in 1996. Look, scaffolds
gave us a time machine!

We are going to scrap the whole table and write our own list out of `<ul>` and `<li>`
tags.

```html
  <ul class='list-group'>
    <% @projects.each do |project| %>
    <li class='list-group-item'><%= project.name %></li>
    <% end %>
  </ul>
```

This is so much prettier, except that we can't use it anymore, because there are no links to
edit, show, and destroy. Beauty can't trump that functionality. Let's get those functions back in
but prettified!

First we will make the project name into a link:

```html
  <li class='list-group-item'>
    <%= link_to(project.name, project) %>
  </li>
```

Notice how the `<li>` can become multiple lines in HTML without changing the way it is rendered
in the browser. And it gives us more room to write the content in a readable way. Instead of
just the project name. We are using a Rails helper `link_to`, which auto creates a link to that
show page. The first argument is the display text of the link. The next element is the resource
we are linking to.

Next, let's add a button for editing our project. Put it right after the `link_to` tag.

```html
  <button type="button" class="btn btn-default btn-xs pull-right">
    Edit
  </button>
```

Let's talk about those crazy classes. What bootstrap does is provide a bunch of classes that
add one little bit of CSS functionality to your element. `btn` makes it a button style. `btn-default`
specifies the coloring style should be default, hover state too. `btn-xs` makes the button very
tiny. `pull-right` makes the button hug the right hand side of its container.

The funny thing is it looks right, but goes nowhere :( We need to switch it to a `link_to` tag:

```html
  <%= link_to('Edit', edit_project_path(project),
        class: "btn btn-default btn-xs pull-right") %>
```

This `link_to` has text 'Edit' and uses a path helper that Rails provides for getting to the edit
path of our project. It allows us to add all those classes as one big string in a hash.

Let's add another link right under the last.

```html
  <%= link_to('Delete', project_path(project),
        method: :delete,
        class: "btn btn-default btn-xs pull-right") %>
```

Rails is a little funky about linking to a delete path. We have to pass in another option into it.
Don't worry, just type.

Go to your browser and check it out. Is it the way you expected? Notice how the first link shows
up in the browser _after_ the last link. That is weird. But it is the way CSS works when you are
forcing things to the right.

### Going back home

Now that we have such a great projects page, the home page we created
isn't so useful. We don't know what to put there that hasn't already
been covered in the app. Let's get rid of it. (This happens all the
time in real development. We are deletionists.)

We need to do this by changing our routes.rb file in the config directory.

Find the line that maps 'root' to "welcome#home". Change it to go
to "projects#index". What does that do, when you reload the application
home page?

### Deletionism

Now that we have built a better navigation system, there is a lot of code and
files that we should delete. Can you come up with a list of things we no longer need?
