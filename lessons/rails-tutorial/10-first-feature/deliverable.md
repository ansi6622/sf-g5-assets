---
title: Rails - Our first feature
bloom: application
---

# Goal: Write some code without so much cake mix

## Objectives:
* Create a migration from scratch
* Working with the controller to change model data
* Change views in response to different model data
* Introduction to helpers

-------

## All that was fun. But still we can't complete a task.

Task lists are only useful if you they give you some sense of where you are in
them. Our whole system is pretty faulty because we can't complete tasks. Doing
this is going to involve doing all things you have already done.
Now we just need to do them all in a more directly related way.

### Making a migration

Before we got our migration through the scaffold command. Now we are going to use
`rails generate` to write our own custom migration.

```bash
  rails generate migration add_completed_to_tasks
```

Let's open that file and add some code to add our new column.

'db/migrations/XXXXXX\_add\_completed\_to\_tasks.rb'

```ruby
  def change
    add_column :tasks, :completed, :boolean, default: false
  end
```

We don't have to dive too deep right now, but this code adds
a column to the tasks table (first argument). The name of the
column is 'completed'. The type is a boolean meaning it is true or
false. Finally, we gave it a default value of false, so that existing
records would have that.

```bash
  rake db:migrate
```

### Preparing the controller to update the completed field

We haven't done much work in a controller yet. Everything was generated
by our scaffold. And there is a lot of code. When we want to edit
a resource, the form data is submitted to the `update` action. But
in Rails we need to allow the params through so that they actually
get to the model and get updated. This happens in one of the last lines of
the TasksController.

Go find the method named: `task_params`. Notice how the code inside
indicates that it is requiring some stuff and also that it is permitting
some stuff from the params. Params are the bits of data that come
from the form, packaged so that we can ask and demand information.

The require method demands that that attribute is there. The permit
allows those parameters to pass through. So we need to add 'completed'
to the attributes that can be passed down to the model.

```ruby
  def task_params
    params.require(:task).permit(:name, :project_id, :completed)
  end
```

### Making the view work

We have been using the project 'show' view as the place where all our our tasks
can be seen. It would be great to also be able to complete these task right in
place. In order to do that we are going to need to put a form into our view.

The form will be updating an individual task, so even though the view is over
in the projects area, we are going to be building a talk related form.

The view is at: '/app/views/projects/show'. Right now the task name is in an `<li>`
element all on its own. We want to put the form into that list element!

```html
  <li class='list-group-item'>
    <%= form_for(task) do |f| %>
      <%= f.check_box(:completed) %>
      <%= task.name %>
      <%= f.submit("Save", class: 'btn btn-xs btn-default pull-right') %>
    <% end %>
  </li>
```

We added a `form_for` tag, a Rails helper that builds forms based on what model you provide it.
Inside of that we have a checkbox. The `form_for` knows what model we are dealing with, so the
`check_box` method on that form just needs to know which field it is representing. In this case,
we want it to be checked or unchecked based on our new 'completed' field. The `task.name` is now right
in the middle of everything. And we conclude the form with a submit button. It has the classes that
we previously used on our project index page. It makes the button look like our other similar buttons.

Run the server; complete a task. Notice how we end up in a weird place in the app, the task edit form.
What we would really like it to go back to our project show view ... and we will work on that later.
For right now try checking tasks, saving and reloading the page. Notice anything else that is going wrong?
On the other hand when we reload the page, the check boxes that were checked stay checked. That gives
us some confidence that our data is being saved.

Go to the console and confirm that the data you are seeing in the GUI is the same data in the models.

### Giving Completed Tasks a Different Look & Feel

We would really like to see finished tasks looking different than unfinished tasks. While the checkbox
is handy, I would like them to look more different than they currently do so I can find out more at
a glance.

Let's set a css class based on whether or not the task is completed:

```html
  <li class="list-group-item <%= task.completed ? 'completed' : '' %>">
```

Visit your browser and convince yourself that this is working right. Great!

The thing is, it is really poor form to put this kind of logic in your views ... it will
get you fired. It turns out that Rails has helpers for containing our view logic. We have
been using many of these: `link_to`, `form_for`, but now we are going to create our own.

Open up '/app/helpers/projects_helper.rb'. It just contains an empty module. We are going
to add this method:

```ruby
  def completed_class(task)
    task.completed ? 'completed' : ''
  end
```

Next we are going to replace our ternary if statement with just a call to this method:

```html
  <li class='list-group-item <%= completed_class(task) %>'>
```

Go back to the browser and confirm it is still working in just the way it was.

Now let's add some styling. This is going to be the first CSS we have written, and it will
be really simple. Open the '/app/assets/stylesheets/projects.css.scss' file and add this:

```css
  .completed {
    text-decoration: line-through;
    color: gray;
  }
```

Reload your browser page and check out the magic!

As an aside, we have just performed a refactoring.

### Redirection

Remember before when we were annoyed by what happened after we saved the completed (or un-completed)
task? Let's look at the TasksController. The method `update` is what our form is hitting.

You can see in the middle of that `if` statement that when the task is succesfully updated, it redirects
back to the task's show page. We never use that page though. So, let's change where it redirects to.

```ruby
  format.html { redirect_to @task.project, notice: 'Task was successfully updated.' }
```

Now try checking, unchecking and saving in the browser. Better experience? We think so!

### What else?

There are a lot more improvements that we could do, and we aren't going to do them today.
Let's brainstorm about what they are right now, though. That way you will get in the mindset
of thinking about edge cases, and unexplored options ... they bite every time.
