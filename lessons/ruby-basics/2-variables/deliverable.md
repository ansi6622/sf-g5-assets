---
title: Varying with Variables
blooms: understanding
---

# Goal: Understanding local and instance variables

## Objectives
* Conceptualize assignment of an object into a variable
* Understand legal and idiomatic variable names
* Comprehend that variables act like the object they hold
* Understand that variables are reusable with any other type of object
* Introduce best practices for variable usage and naming
* Introduce instance level variables

## Prerequisites
* Reading and exercises in [Learn to Program](https://pine.fm/LearnToProgram/)

-------
# Variables are containers for things you have now and will need later

Imagine that you are working out a complex equation on a calculator.
Most calculators have a button, or two, that stores a number for later.
This is handy for breaking complex equations down into simpler, smaller steps.

Programming is all about those small steps and having easy places to store things
until you need them again. A variable is just like those buttons.

### Assigning to Variables

Variables are called variables because they _can_ change, and we know they
 _will_ change. But we rarely know ahead of time _what_ they will become.

Take for example the number of people in our class on a daily basis. We know how many
people are enrolled in the class. We are much less secure about how many people
will survive MUNI and flu season to arrive in our humble abode. This quantity,
people currently in class, could be stored in a variable, since the value varies.

We use the equal sign to assign values from the right side to variables on the left.

```ruby
  people_currently_in_class = 27
  # => 27

  people_currently_in_class
  # => 27

  # uh, oh! Flu outbreak

  people_currently_in_class = 18 # :(
```

### Legal Variable Names

Variables in Ruby have to follow some rules. They can contain any alphanumeric
character, plus an underscore `_`. The variable name has to start with either a letter
or an underscore. In other words, you can't start a variable name with a number.

Here are some legal names: `__tacos`, `bag_of_money`, `i`

By convention, these variables don't contain capital letters. Ruby variables are
usually what is called both snake-case, or underscored: `snake_with_a_snack`.

What happens if you try to assign something to an illegal variable name?
Let's experiment:

```ruby
  12foo = 12
  #  SyntaxError: (irb):2: syntax error, unexpected tIDENTIFIER, expecting end-of-input
  #  12foo = 12
  #       ^
```

Ruby just can't figure out what to do when it runs into an illegal variable name. The
error that you see above is the typical feedback you will get when the syntax of
the code does not make sense. Pay attention, it will come back over and over again.

### Variables Act Like the Thing They Hold

Variables are drawers where you can hold things. The funny thing is that the drawer
pretends to be the thing that it holds. That means that you can call methods on
variables as long as the thing inside them responds to that message.

```ruby
  number_of_students = 26
  # => 26
  number_of_students.to_s
  # => '26'
  sick_students = 5
  # => 5

  students_in_class = number_of_students - sick_students
  # => 21

  ratio_present = students_in_class.to_f / number_of_students
  # => 0.8076923076923077
```

### Variables Are Flexible

As we have seen, variables are reusable. We can put something inside it; use it
and then put something else in it.

It turns out that you can put any kind of an object into a variable. Some languages
don't allow this. They force programmers to choose up front what kinds of things
go inside the variable.

Ruby doesn't care. You can reuse a variable with anything.

```ruby
  students = 26
  # => 26

  students = true
  # => true

  students - sick_students
  # => NoMethodError: undefined method '-' for true:TrueClass
	#      from (irb):2
	#      from /Users/baccigalupi/.rvm/rubies/ruby-2.0.0-p481/bin/irb:12:in '<main>'
```

Of course, changing the type of thing in a variable is hard because then you might
try to use it like some other type of object. And that just won't work. Also, it is
pretty hard to name something which has the potential to be many different kinds
of things.

In this case, we used the variable name `students` which is very general. It holds
the number of students first, and then the fact that there are students. It could
also hold a collection of objects with student data. It would
be hard for other programmers to guess easily what might be in that container.
It would even be hard for the author to figure this out after a month
absence. Naming is one of the hardest things in programming, and putting all
different kinds of data into a variable makes that naming so much harder.

### Instance Variables

The variables that we have been talking about so far are all _local_ variables. Local
refers to the scope, or where these variables can be seen. Since we are dealing in
procedures right now, or scripts, our scope is global, or everywhere.

Another type of variables is an instance variable. By instance, we mean an instance
of an object. These are the variables that belong to an object, and can be seen
everywhere in that object. We will explore them more once we learn how to make our
own objects.

Instance variables use the same naming conventions as local variables, but always
start with a `@`. That they start with an `@` means that the next character can
be a number.

We could rewrite some of our scripts to use instance variables instead of local
variables and things just work.

```ruby
  @number_of_students = 26
  # => 26
  @sick_students = 5
  # => 5

  @students_in_class = @number_of_students - @sick_students
  # => 21

  @ratio_present = @students_in_class.to_f / @number_of_students
  # => 0.8076923076923077
```

Since instance variables are variables belonging to an object, in this kind of a
script, who do they belong to?

Ruby is flexible. It is object-oriented and it also allows scripting. In this kind
of a procedural script, the instance variable is just hanging out in the global
space.

One difference, even in this very object-free space between instance variables and
local variables is that you can just start using instance variables, even if they
don't exist yet. Local variables have to be set into being. Let's look at an example:

```ruby
  nothing_here
  # NameError: undefined local variable or method `nothing_here' for main:Object
	#         from (irb):36
	#         from /Users/baccigalupi/.rvm/rubies/ruby-2.0.0-p481/bin/irb:12:in `<main>'

  @nothing_here
  # => nil
```

When you try to call `nothing_here`, a local variable that has not yet been defined, Ruby
complains that you are doing something wrong. But when you call an instance variable that
has never been set up, it returns `nil` which is the Ruby idea of nothingness. It's almost
as if every possible instance variable is there waiting to be called into nothingness.

When we get deeper into scope and objects. These two kinds of variables will act
very different.

## Resources
* [Variables](http://tutorials.jumpstartlab.com/projects/ruby_in_100_minutes.html#2.-variables)

## Exercises
* Instance variables have similar naming conventions, but in reality have more flexibility
around naming. Experiment in IRB to figure out what the rules are for legal names in instance
variables.
