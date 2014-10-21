---
title: Blocks, Methods, Functions, oh my!
blooms: understanding
---

# Goal: Understand Functions, Methods and Blocks: Compare & Contrast

## Objectives:
* Be able to create our own methods
* Understand all that is possible with arguments
  * default values
  * splatted args
* Explore return values
* Understand Functions vs Methods
* Introduce scope

## Prerequisites
* Reading and exercises in [Learn to Code](https://pine.fm/LearnToProgram/)

-----

## Using other people's methods is easy, but we need to make our own

Let's revisit some stuff we said before ... everything in Ruby is an object. Even
though have not yet built any custom objects ourselves, hashes, arrays, strings and everything
else is an object. That means they operate as a tiny package containing both data
and methods.

Methods are little procedures and usually they are focused in some
way on the object they live in. For example, `#upcase` on strings will take the
underlying string of characters, and use it to construct a new string that is uppercase.
If there were a method on string that dealt only with array data, it would be in
the wrong place. The goal of objects is that they are small and self-centered.

Let's check out how methods are made:

```ruby
  def greet_class
    puts "Hello, I am Kane"
  end
```  

We use the `def` keyword followed by the method name. It turns out that you can
specify arguments that should be passed into methods. These become variables that
are available in the method.

```ruby
  def greet_student(student_name)
    puts "Hello #{student_name}, I am Kane"
  end
```

Parenthesis in Ruby are usually optional, so it is just as valid to write that method this way:

```ruby
  def greet_student student_name
    puts "Hello #{student_name}, I am Kane"
  end
```

For multiple arguments, we separate each one with a comma.

```ruby
  def greet greeter, greetee
    puts "Hello #{greetee}, I am #{greeter}"
  end
```

Sometimes we want the option of passing in an argument, but we would like a default value.
That is possible!

```ruby
  def greet greeter, greetee = "friend"
    puts "Hello #{greetee}, I am #{greeter}"
  end
```

In this case, we have to provide the first argument, but the second we can provide or leave off.

What happens if you don't provide the right number of arguments?

```ruby
  greet "me", "you", "someone else"
  # ArgumentError: wrong number of arguments (3 for 1..2)
	#    from (irb):1:in `greet'
	#    from (irb):4
	#    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

Don't worry this happens all the time. And when Ruby raises an error, it is always
trying to tell you what is going wrong. In this case it is telling us that it
received three arguments for this method, but was expecting between one or two. The
ambiguity around what it expects is because of that default value we added.

Of course, Ruby is flexible, so you can do something totally crazy and just mush
arguments into a single variable.

```ruby
  def greet_all greeter, *greetees
    puts "Hello #{greetees.join(", ")}, I am #{greeter}"
  end

  greet_all "the computer", "John", "Martha", "students"
  # "Hello John, Martha, students, I am the computer"
  # => nil
```

The `*` in front of the argument is called a splat operator. It will convert all the
remaning passed arguments into an array of the values passed in.

### Return values

Everything returns something, even if that something is nothingness, on `nil`.

That means an empty method will return something ... `nil`. Let's experiment with that:

```ruby
  def the_void
  end

  the_void
  # => nil
```

In Ruby, it is pretty rare to see an explicit call to `return`, but it is possible.
One of the places we frequently see this is with something called a guard clause:

```ruby
  def invite friend
    return unless friend.member?
    send_invitation(friend)
  end
```

This is some hypothetical code. It invites a friend. But if the friend is already
a member, we would rather not.

In most other cases, it is a bad idea to use an explicit return. People will assume
you don't understand Ruby always returns something.

### Functions

That is all fine and well, but we have just created a whole bunch of methods not related
to any objects! That is pretty much what other languages call functions. They are little
procedures wrapped in names that we can call later.

And if you remember, what we said about blocks in the iteration section is that they are
little procedures that you can call later. So, let's look into blocks and see what else
there is to know.

Shortly, we will get into making our own custom objects, and then all our methods will have a home.

### Scope?

Until now we have only looked at scripts, which is to say procedures in code that are pretty flat.
Everything can see everything else.

With the introduction of methods now create local variables that aren't available globally. Let's
take a look at what I mean:

```ruby
  def do_something
    done = true
  end

  done
  # NameError: undefined local variable or method `done' for main:Object
	#    from (irb):5
	#    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

As you can see, the local variable that was defined inside the method is not available
outside that method.

This is why Ruby has instance variables, to span scope.

```ruby
  def do_something
    @done = true
  end

  @done
  # => true
```

It turns out this is true of arguments too.

```ruby
  def set_done(doneness)
    done = doneness
  end

  doneness
  # NameError: undefined local variable or method `doneness' for main:Object
  #    from (irb):5
  #    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

Blocks have scope issues both with the arguments inside of pipes, and local variables
defined within blocks.

```ruby
  (1..10).each do |n|
    local = n
  end

  n
  # NameError: undefined local variable or method `n' for main:Object
  #    from (irb):5
  #    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'

  local
  # NameError: undefined local variable or method `local' for main:Object
  #    from (irb):5
  #    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

Scoping behavior changes when a local variable is defined outside of the method,
before use.

```ruby
  done = false

  def do_something
    puts "Something is currently done? #{done}"
    done = true
  end
  # Something is currently done? false
  # => true

  done
  # => true
```

What is happening in this example is that a local variable is defined outside the method.
When we get into the method and set the variable, we are setting the existing variable,
not creating a new one. Then when we leave the method, and look at what it is in the
variable, it has been changed permanently by the method.

It seems tedious, but is pretty important to think about scope.

## Group Exercise
* First spec file in [collection-method-exercises](https://github.com/gSchool/collection-method-exercise)

## Solo Exercise
* Second spec file in [collection-method-exercises](https://github.com/gSchool/collection-method-exercise)

## Group Exercise
* Go over second exercise as a group

## Assessment
```gherkin
  Given an array of hashes of student names (built in the array assement)
  When I run my ruby file
  Then I should see a headline printed: "All"
  And I should see printed list of students in this format "{{last name}}, {{first_name}}: {{email}}"
  And I should see a headline printed: "Some"
  And I should see the same formatting for the students that have a 't' upper or lower case in their last names
```
