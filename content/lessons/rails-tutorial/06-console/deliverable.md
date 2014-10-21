---
title: Rails - Models in the Console
blooms: understanding
---

# Goal: Understand What the Model Does

## Objectives:

* Learn about Rails Console
* Try all the Model CRUD methods on the command line
* Hand make some associations models on the command line

------

## All That is Pretty, But You Are A DEVELOPER! What's Under the Hood?

Let's create a few projects and tasks via your GUI (Graphical User Interface).

Let's go check out what these look like via a command line app that Rails provides.
It is called the console. Let's start the console.

```bash
  rails console
```

Now, let's take a look under the hood and see all the projects we just created.

```ruby
Project.all
```

At first glance, all this output is probably really confusing. But take a closer look. What we're
getting here is the name of each project, a project id, and what appears some dates and times. Remember
timestamps from our migration? Well, that's what it gave us.

Let's do some more. Remember how we just created three new projects using our GUI? Let's do that
very same thing, but from the console.

First, let's ask the console how many projects we currently have.

```ruby
Project.count
```
Ok, now, let's add to that.

```ruby
Project.new()
```
Sweet. Let's check out that number again.

```ruby
Project.count
```

WAIT! WHAT? Why is that number the same? We just added a new project? Why didn't that save?!

```ruby
project = Project.new()
project.save
Project.count
```
Phew! That was a close one.

Let's go back to our GUI and do some more!  

This time, let's update an existing project. Let's change the name of one of our projects.

Now, let's go back to the console and do the same thing but from under the hood.

In fact, remember the last project we created from the console? Guess what? We didn't really
give it a name.  So let's do that.

```ruby
project.update(name: "Console Project")
```
Ok, let's see that one in action. Let's go back to our GUI. See our Console Project?  Nice!

Let's go see it in our console too.  

```ruby
Project.last
```

What do ya know, there it is.  But you know what? I don't like any of these projects
anymore.  Let's get rid of them all!!

```ruby
Project.destroy_all
```

Let's make sure they're all gone.

```ruby
Project.count
```

Woo hoo! No work to do!

But wait, we still have all these tasks. What's going on in the GUI?

Phew, good thing we wrote that method earlier to handle a situation like this.  Instead
of blowing up, our app simply lists projects as __none__.

But you know what, a task with no project is sort of useless.  Let's go back to the console
and take care of some business.

```ruby
project = Project.create(name: "Console Project")
task = Task.first
task.project = project
task.save
```
Ok, great. But why did we have to save the task and not the project that time?  

Right. Great question. That's because we used 'create' this time when creating our project,
instead of 'new' and 'save'. It turns out, when you use 'create' it also saves the new object
for you.  Later, we'll talk more about how to make decisions about when to use 'create' and
when to use 'new' and 'save'.

Let's keep going!

Similar to how we assigned a project name to a task, can we can get information on all of
our project tasks from the command line.

```ruby
project.tasks
```
Ok, it looks like we have one task assigned to this. But it's not actually just a task, it's actually
a collection of tasks with just one tasks in that collection.  In fact, it's an array of tasks.  So
let's see that in action.

```ruby
project.tasks.create(name: "foo")
project.tasks
```

Now that's a collection!

How much does your brain hurt right now? Let's go back to the GUI.
