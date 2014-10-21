---
title: Objects Again
blooms: understanding
---

# Goal: Understand How Classes Create Objects

## Objectives:
* Recognize class construction
* Learn how to make new objects from a class
* Build a basic class
* Understand scope within a class
* Understand self
* Be able to use inheritance
* Recognize and build a module
* Be able to mixin modules via `extend` and `include`
* Recognize and create class methods

## Prerequisites
* Reading and exercises in [Learn to Code](https://pine.fm/LearnToProgram/)
* Basic Ruby, Basic Objects [lesson](/lessons/ruby-basics/objects)

-----

## Let's start packaging our logic in classes!

So far we have been writing lots of procedural code. We did introduce methods,
but they weren't encapsulated in a class.

Object oriented code comes from writing classes and turning them into objects.
And Ruby does scripting fine, but it is really for making object oriented code.

### Why Objects?

Imagine every book in the world were copied, page by page into a single book. It
would be really hard to read. Just the weight of it would be huge. And then when
we wanted to find a particular subject, or worse a particular page in that book,
our lives would be pretty sad.

It turns out we group knowledge into books so that we can focus.

Object try to focus our logic in one place. Instead of putting all our application
into a single script, we break it into little packets containing data and methods
for that data.

The typical way to create objects is with the `.new` method on the class. Let's
create an object:

```ruby
  Object.new
  # => #<Object:0x007fe8c2096098>
```

We have already used a lot of objects, and we didn't have to use the `.new` method.
It turns out that we can use that class method too.

```ruby
  Array.new
  # => []

  Hash.new
  # => {}
```

Array and Hash are easy in that they don't take arguments. But some classes require
one or more arguments.

```ruby
  Range.new
  #

  Range.new(1, 3)
  # => 1..3
```

### Classes

If you have every made clothing from scratch, there is typically a pattern. You
use the pattern to cuto out the clothe and sew the clothing together in the right
way. It is very effective.

Classes are the patterns for making objects.

Let's create a class, and then make an object from that class:

```ruby
  class Printer
  end

  printer = Printer.new
  # => #<Printer:0x007fe8c2058568>
```

Notice that our class name is capitalized. It is a convention to capitalize classes
and you will typically not see underscores in class names. Instead you will see
capitalized words smashed together.

Alas, that is not very useful. What about adding some logic and data to our class.

```ruby
  class Printer
    def initialize
      @output = []
    end

    def print
      @output.join(" ")
    end

    def add(string)
      @output << string
    end
  end

  printer = Printer.new
  printer.print
  # => ""
  printer.add("Dear friend")
  printer.add("I love you!")
  printer.print
  # => "Dear friend I love you!"
```

That is a little more interesting. We have just build something like a parrot. We
feed it things to say, and it stores them and saves them.

Did you notice that instance variable `@output`. We set it up in the initialize method, which
gets called when you make a new object of this class. It is an array where we can store
strings. Then we add to it in the `add` method.
Finally we read from it in the `print` method by joining all the strings with a space.

We used an instance variable instead of a local variable because instance variables are
available throughout the entire object. Every method can access that instance variable.
Local variable go out of scope as soon as the method is left. So if we set a local variable
in `initialize`, it would not be available in the `print` or `add` methods.

### Self

One other Ruby concept that hasn't come up is the notion of `self`. `self` is a keyword
in Ruby that refers to the object that you are inside of. That is a weird concept so let's
look at it is action:

```ruby
  class Printer
    def print_from_self
      # put a message in front of the current array of messages:
      @output.unshift("#{self} says:")
      print
    end
  end

  printer = Printer.new
  printer.print
  # => ""
  printer.add("Dear friend")
  printer.add("I love you!")
  printer.print_from_self
  # => "#<Printer:0x007fef41819ba0> says: Dear friend I love you!"
```

You can call methods on self in the context of an object. So in the print_from_self
method, we could have done this:

```ruby
  class Printer
    def print_from_self
      # put a message in front of the current array of messages:
      @output.unshift("#{self} says:")
      self.print
    end
  end
```

Typically, Rubyists don't use explicitly use self to call a method on itself.

### Subclasses

Getting back to our Printer class functionality:
We could probably come up with lots of ways to print an array of strings. Let's say
that we wanted to format our strings by wrapping them in HTML instead of just adding
a space between them.

It would suck to just copy and paste that class into a new area of the code. It turns out
that we can just make a subclass that inherits all that behavior, and writes the stuff that
we need that is new. Let's try it:

```ruby
  class HtmlPrinter < Printer
    def print
      "<p>#{@output.join("</p><p>")}</p>"
    end
  end

  printer = HtmlPrinter.new
  printer.add("Dear friend")
  printer.add("I love you!")
  printer.print
  # => "<p>Dear friend</p><p>I love you!</p>"
```
In this case, we used all of the original printer class, and rewrote the `print`
method. Everything else acts the same, but when we call `print` instead of looking
at the original definition, it uses the new method. That method is a little
dense: it makes a string that starts and ends with `p` tags. In the center of
those tags in puts the joined array. The array is being joined by an ending and
then a beginning `p` tag. And most important, it all works.


### Mixins

It turns out subclassing is just a way of sharing code between classes. Ruby provides
other ways to do similar things.

Let's imaging another code universe where you have a weird social network. There
are events and topics. People run around commenting on them. And you have crazy
product managers who are adding things that need comments all the time!

In Rails you might handle this with a module.

A module, just like a class, is a collection of methods. Let's build a module:

```ruby
  module Commentable
    def comment(message)
      puts "comment: #{message}"
    end
  end

  Commentable.comment("hello?")
  # "comment: hello?"
```

In Rails you would probably want this to do more that just puts a string. But
let's just mix it into some classes anyways.

To share this module code with a class you would use the `include` keyword.

```ruby
  class Event
    # ... lots of methods
    include Commentable
  end
```

Since we could call `comment` on the `Commentable` module, you might assume that
this method would also be available on the `Event` class:

```ruby
  Event.comment("hello?")

  # NoMethodError: undefined method `comment' for Event:Class
  # 	from (irb):51
  # 	from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

Because we used the `include` keyword with our module, methods will be injected
into the instance or object:

```ruby
  event = Event.new
  event.comment("Hi!")
  # "comment: Hi!"
```

Ok. There it is!

What if we did want the event class to respond to `comment`? There is another keyword
`extend` that is used for adding methods to the class:

```ruby
  class Topic
    extend Commentable
  end

  Topic.comment("whatever ...")
  # "comment: whatever ..."

  topic = Topic.new
  topic.comment
  # NoMethodError: undefined method `comment' for #<Topic:0x007fef418f97c8>
  # 	from (irb):55
  # 	from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

And as you can see it only adds those methods to the class not the instance.

### Class Methods

Did we mention that everything in Ruby is a object?

It turns out even classes are objects, and because of that we can put methods
on them, and they can even have data.

You can use the `extend` keyword with a module to create these methods, but
sometimes you want to write them into classes directly.

Let's go back to our printer class and make a class method for faster printing:

```ruby
  class Printer
    def self.print messages
      printer = new
      messages.each do |string|
        printer.add( string )
      end
      printer.print
    end
  end

  Printer.print(["hello", "world"])
  # => "hello world"
```

Notice that we have `self.` in the method declaration. What we are doing is defining
a method on the object self. In this case we are inside the class definition, and therefore
self is the class itself.

We get all the benefits of inheritance with class methods too. So after adding this class
method to our base printer class, the subclasses will be able to use it too.

```ruby
  HtmlPrinter.print(["hello", "world"])
  # => "<p>hello</p><p>world</p>"
```

## Group Exercises
* Brainstorm about what other kinds of printers you could make as subclasses


## Extra Credit
* Some other exercises that are thematically related, but hard or time consuming
* Or maybe just more of them

## Other Resources
* Other loosely related links

## Assessment
* A link to an assessment to test whether the student knows the material
