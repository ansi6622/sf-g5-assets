---
bloom: Memorization of refactoring with classes; application of class construction
publish:
----

[deliverable](deliverable)

## Goal
Learn about refactoring big classes into separate classes. Introduce single responsibility.

## Objectives
* Be able to aggregate method names together
* Evaluate method names that don't group well
* Determine method dependencies
* Extract methods without dependencies into separate classes
* Understand extraction of methods with dependencies
* Be able to build objects from extracted classes

## Prerequisites
* Completed exercise on CLI refactor into methods
* Understanding of Ruby classes

## Materials
* git repository: git@github.com:gschool-g5/todo-cli.git
* starting place for we do: git@github.com:baccigalupi/todo-cli.git, master branch

## Gain Attention
Now that we have extracted methods. We have a
How will you convince the students that this is a worthy problem straightaway?

Examples are: asking questions, showing mockups or real sites, pointing out features or problems

## Inform learner of objective
Remember/recognize extraction of classes. Apply creation of classes, and use of
custom objects:
* Recognize method name similarities as an indication of separate responsibilities
* Practice moving groups of methods into separate objects
* Practice creating and using extracted objects

## Stimulate recall of prior information
The big `run` method in our CLI app, got quite a bit easier to understand when
we extracted methods. Did you notice that the class got much bigger?

## Present the stimulus (I do)
Smaller is still better.
What can we do to improve this? Wait for lots of answers, shine no lights.

* Show three different projects to the class.
* Mob evaluate the names of methods
* Start to group methods together according to name
* Question the name of anything that does not group well

There are:
  * flow related methods
  * project related methods
  * task related issues

This makes sense since we have 2 menus in our product.

Let's look at the big `if` statement in the middle of the `run` method.
Symmetry!

Also, there is a lot of printing that happens. Let's start by building a printer
object.

```ruby
  class Printer
  end
```

Brainstorm what methods and data needs to move in order to transfer `puts`, and `gets`

Extract the printer class one method at a time.

## Provide learner guidance
* As we group methods, we should think about any method that does not aggregate
* Shapes of methods also can help us determine grouping

* Sandi Metz rules:
  * No method more than 5 lines
  * No class more than 100 lines

* When the code reflect the product, you are probably getting to the right abstractions

* Tests should always be passing as you refactor

## We do
Everyone should download a version of the application ready for refactor and
together we will do the following:

Extract user input object. Brainstorm what to call it.

Brainstorm what other objects we see lurking in the methods.

Separate the big if statement, into a something with two branches:
* project being edited
* or no current project

Build once separated build two different menu classes objects.

## Exercises (You do)
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
