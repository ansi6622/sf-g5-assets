# Lesson Title

## Goal
Write more maintainable code, by grouping logic into classes

## Objectives
Remember/recognize extraction of classes.
Apply creation of classes, and use of custom objects:
* Recognize method name similarities as an indication of separate responsibilities
* Practice moving groups of methods into separate objects
* Practice creating and using extracted objects

## Prerequisites
* Completed exercise on CLI refactor into methods
* Understanding of Ruby classes

## Materials
* git repository: git@github.com:gschool-g5/todo-cli.git
* starting place for group exercise: git@github.com:baccigalupi/todo-cli.git

## Writing more maintainable code with classes!
Remember in the last class when we showed different people's solutions.
What made sense to them was probably Greek to you.
And they probably feel the same way about your code.

Extracting methods gave the logic more names, but now the class is very large.
It is hard to page through everything to understand what is going on.

It's often really hard, even for experienced developers to figure out how to divide
classes into smaller classes. Let's look as some techniques.

### Technique: Organize and group methods by name
In our code we see:
* There are a lot of method names that have to do with printing, and most of these
actually print to the command line
* There are methods related to projects
* There are methods related to tasks
* There is a small set of methods related to getting input

### Our first class extraction
A printer class would provide a really simple way to
clean up some code. We are going to start by extracting that class first.

After grouping all the printing named methods together, we want to:
* Check to make sure each of them actually prints using puts, and is not just
  named with printing in mind
* Look at each method to see if we can pass in the data we need instead of grabbing
  it from the class in general. That is called identifying dependencies. In order
  to move this method somewhere else, we need to know everything that it depends on,
  and it is easier to see if we pass arguments in instead of grabbing them from scope.

Now let's write the base class for starting the extraction process:

```ruby
  class Printer
    attr_reader :io_output

    def initialize(io_output)
      @io_input = io_output
    end

    def puts message
      io_output.puts message
    end
  end
```

The Printer initializes with our io_input object. We need that to build our basic `puts`.

In our original class, we want to build a printer instance in the initializer:

```ruby
  @printer = Printer.new(io_output)
```

We should run our tests and make sure everything still works. We haven't yet changed
the logic in our class to use the printer, but running tests catches syntax errors
and any error we made when constructing the printer.

Next we want to switch our puts method to use the printer:

```ruby
  def puts message
    printer.puts message
  end
```

Run the tests again. You are now using your new printer object! We can prove that
we no longer need the `io_output` object by deleting code. We only need to pass
that object into the printer, so we can now remove the accessor/reader, run our tests
to confirm and move on.

Next we want to go through every method that uses puts and make sure it passes in
its dependencies as arguments. For example if you have a method called `print_current_project`
make sure it passes in the current project name as an argument! Changing the
method signature means changing its usage everywhere else.

Now we can copy that method over to our printer class. Just copy it, don't delete
the original. Run the tests ... nothing should have changed.

Now switch all the usages of that method to point to the one in the printer. Run
tests, everything should still pass.

Lather, rinse, repeat!

In the end, you should have extracted everything that uses `puts` into the printer
class.

## Technique: Brainstorming about nouns in the product
Based on our code and more importantly the product needs, we can
start to imagine what kind of objects would be in our system. Once
we think about these objects, we want to think about the data
they would hold and the methods they would have. Then we can
evaluate if it is a good object candidate. The things we usually
think of first are nouns. Let's explore some obvious nouns.

    Project
      data: name
      methods: --none--

Notice I didn't put 'create' or 'find' methods in this object.
That really belongs to a collection of projects. Also, 'edit' is something
you would do to the data object, except in our product case, editing a project
store in the application, data about which project tasks we are looking at.

Given that Project just has a name that is a string, it is not a great candidate
for extraction, at least initially. We should try other things.

So the next candidate we should look at is the collection Projects:

    Projects
      data: collection of projects with their tasks, current project
      methods: create, find, list

Now that we are holding state about the current project in the Projects object,
the 'edit' method is also appropriate. For a way of organizing our data, Projects
is a better candidate.

Do we need Tasks or Task? Those are the two other data components of our application.
The code is much more easy to manage when the data is in a single container. This
is a pretty simple application, and having two data containers means we have to find
a way to associate that data.

Depending on how the data is currently organized, this may be a harder problem.
What you want is that after each small change to the code, you can run your
tests and they all pass. In the case of rewriting the way our data is stored, we
may need to do major changes to our code.

We are going to try an alternate extraction technique:

### Extraction, via test driven parallel class development

Instead of moving methods over one by one, let's look at the kind of things we would like
to do with a Projects object. We already made a small list of fuzzy methods. We are going
to expand that list as we go along:

So let's build this class:
1. Write a test about the initial state of the object. State is the same as the
data we mentioned in our brainstorming.
2. Write a class that makes that code pass
3. Look at existing methods and how they work with project and task data to write:
  * first tests
  * then code
4. Keep writing methods until you have an object that you feel encapsulates the data

After building this class, you are going to need to switch it in, and it will be very
hard to switch it in gradually.

Now would be a good time to commit in git. That way you can roll back to this state
and try again and again. You don't have to get it right the first many times.

### Technique: Looking for More Abstract Concepts

It turns out that there are two significant objects that haven't been discovered in
other ways. They are the menus. Many of the methods in our cli app have to do with
responding to inputs depending on whether there is as current project or not. There
is a ProjectsMenu and a TasksMenu lurking in the app that are harder to see.

Why are they hard to see? Really these concepts are more abstract and about the UI.

We are used to thinking about things like projects and tasks. They are ordinary nouns.
Menus are not so typical, especially since these command line applications don't have
the same visual menu look that you see on your desktop computer applications.

In general you need to keep an eye out for objects that are more of programming
constructs. In the future we will see Validators, Observers and other helper objects
that don't set off the usual noun flags.

The menu extraction should allow a method by method extraction into classes, with
all tests passing.

## Exercises
* Repeat this exercise with your own code, doing these things first as neede:
  * rename methods
  * repackage data to be in one object
  * extract more or different methods

## Stretch Exercises
* Write tests for the extracted objects
* In the project we used for group work, extract a data object Projects
  * Write tests one at a time based on what we need our object to do
  * Fill in test code based on what it is doing in various classes
  * Move state about current projects from the Todos class into projects
  * Substitute the Projects object for the hash
  * Move the rest of the menu methods into their prospective classes
* Follow this exercise with someone else's code
