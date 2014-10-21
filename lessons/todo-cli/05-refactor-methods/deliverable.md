# Goal: Refactor and re-organize our code

The command line application works, but it is pretty messy! Nested if statements
are not just frowned upon but are an area where bugs ofter arise.

We are going to start by organizing chunks of code into methods. It is a way of
naming the logic so it is easier to understand.

## Writing code is about maintainability

It may seem hard to believe right now, but writing code that works is the easier
part of a software developer's job. Writing code that is easy to work with in
the future is the harder part.

While you know exactly what you wrote yesterday. If we all rotated code by one seat,
you would find that the stuff that was obvious to your neighbor is hard to understand
for you. It isn't your fault that you can't understand your neighbors code, but
it is your responsibility to leave behind code that is easy to understand.

## Smaller is better

It turns out that whatever language you write in smaller chunks of code are easier
to understand that big complicated chunks of code.

In Ruby one approach to breaking up code is to just break it into smaller pieces
in the form of methods. For example, in several places we show the user the same
project menu. We might be tempted to show them that menu everytime they completed
a project command. If we just had that code repeated over and over again, changing
it to print in many places would get much, much easier.

Let's write a method to extract the project menu instructions:

```ruby
  def print_project_menu
    puts "
      your instructions here
    "
  end
```

This is a really small change, but now in our logic, we see `print_project_menu`
instead of a puts statement that spans many lines. Right away it is easier for
your neighbor to understand what is happening.

In this case we were prompted to do this extraction because we saw some repetition
in the code. In fact, some of you probably already did this extraction. It turns
out that it is useful to extract methods just for the benefit of having a good name.
When we see that well chosen method name, it takes the place of a comment we would otherwise
need to put in our complicated code.

You can think of method extraction as a way of hiding complications under a well-chosen
name. That means that you need to choose your names well, which is one of the hardest
things in computer science ... really ask your local experts.

In this lesson, we are going to be extracting almost everything into methods.

## Code Show and Tell

Let's pop up three different examples from the class, and look for ways to extract methods.

Now, we are going to do a mob refactor.

## Solo Exercise
* Refactor your own code for this projects into methods

## Stretch Exercise
* Fork or clone other people's projects. Refactor! As a developer you will spend more time
working with other people's code than you will creating your own code. 
