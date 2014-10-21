---
title: Ruby Basics - Everything is an Object
blooms: understanding
---
# Goal: Understand the implications of _everything_ being an object!

## Objectives
* Learn to call methods on numbers and other 'primitives'
* Understand operators and method calls
* Introduce Ruby introspection, by asking objects for their methods

## Prerequisites
* Reading and exercises in [Learn to Program](https://pine.fm/LearnToProgram/)

-------

## No, really. _Everything_ is an object!

Let's imagine adding two numbers together with a calculator. It is the operators,
'+', 'x', etc., that do all the work. Those just keep being the numbers they always were.
They are bald data, and most languages have this bald data. This bald data is also
called a 'primitive'.

Ruby is not most languages, and it has _no_ primitives. All data, like numbers, are
wrapped up in a little package with methods.

### Objects have methods

Methods are a way of asking an object for information or
asking an object to do something for you.

```ruby
4.even?
# => true
```

Here, we ask the object for some information- in this case, a question about
itself, and it returns an answer.

```ruby
  3.2.round
  # => 3

```

Here we are asking a decimal, or floating point number as it is
sometimes called in programming, to do something. We want it to round itself.
It returns another number object that is an integer.

### Primitives have no methods

In JavaScript or other languages, numbers are just bald data.
That is what a primitive is.
In Ruby there is no bald data; everything has methods.

### Calling Methods

Let's call some methods on the simplest possible object, a number. To call a method
on an object, we use the `.` operator.

```ruby
  3.even?
  # => false

  3.odd?
  # => true

  3.next
  # => 4

  3.between?(0, 4)
  # => true
```

### Sending Messages

Another way of thinking about this whole process is that objects receive messages
from the world. An alternative way to call any method is with the `send` method, which sends
that method name and arguments. The method gets called, and the result is
returned.

```ruby
  3.send :to_s
  # => "3"

  1.25.send :round
  # => 1

  4.send :zero?
  # => false
```

We just sent three different messages to number objects, and they responded with
a method call specific to that object each time.

These are equivalent to just using the `.` notation below:

```ruby
  3.to_s
  # => "3"

  1.25.round
  # => 1

  4.zero?
  # => false
```

So what is the point in having this middle man `send` in our way confusing our
brains with an extra step? Under the covers ruby is always sending messages to
objects with method calls, and exposing a mechanism to do this ourselves is very
powerful. You can send messages that you don't yet know to an object.

More importantly, the concept of sending messages leads to thinking of objects in
a better way. Instead of thinking of them as the data they contain. We start
thinking of them as the things we can talk to respectfully.

#### Caution!
Send is good for illustrating how Ruby works under the covers, but seriously.
Don't use it, unless you have a spectacularly good reason to. Which you probably
don't.

### Operators are methods too

In a calculator, the operator is doing the work. But in Ruby objects do the work
and even things that look like operators are actually methods.

```ruby
  3 + 1
  # => 4
```

That is a shorthand for doing this:

```ruby
  3.+(1)
  # => 4
```

These method calls look really different, but when you put a `+` after a number, Ruby
is calling a `+` method on the object.

One thing to try to think about is this: `3.+(1)` calls the method `+` on the object
`3`. The method can use the underlying data to figure out what to do with the argument that is
passed in `1`. And out pops a `4`, which is another object that we can call things on.

One other thing to note. It is a common paradigm in Ruby to end a method in a ? when it
will return either `true` or `false`.

By the way `true` and `false` are also objects.



### Finding Methods

As practical as that was supposed to be, it got very theoretical. So, back to the practical.

The basic building blocks of Ruby come with fine documentation that you can find on the web.
But as we grow up as developers, we run into situations where there isn't documentation. Sometimes
we even run into situations where we are programming without WiFi access, and can't get to the
web for documents.

It is often much more fun and expedient to ask objects what they can do. There is a
handy method called `methods` that will tell us just what you can ask of an object.

```ruby
  3.methods

  => [:to_s, :inspect, :-@, :+, :-, :*, :/, :div, :%, :modulo, :divmod, :fdiv,
  :**, :abs, :magnitude, :==, :===, :<=>, :>, :>=, :<, :<=, :~, :&, :|, :^, :[],
  :<<, :>>, :to_f, :size, :bit_length, :zero?, :odd?, :even?, :succ, :integer?,
  :upto, :downto, :times, :next, :pred, :chr, :ord, :to_i, :to_int, :floor, :ceil,
  :truncate, :round, :gcd, :lcm, :gcdlcm, :numerator, :denominator, :to_r,
  :rationalize, :singleton_method_added, :coerce, :i, :+@, :eql?, :remainder,
  :real?, :nonzero?, :step, :quo, :to_c, :real, :imaginary, :imag, :abs2, :arg,
  :angle, :phase, :rectangular, :rect, :polar, :conjugate, :conj, :between?,
  :nil?, :=~, :!~, :hash, :class, :singleton_class, :clone, :dup, :taint, :tainted?,
  :untaint, :untrust, :untrusted?, :trust, :freeze, :frozen?, :methods,
  :singleton_methods, :protected_methods, :private_methods, :public_methods,
  :instance_variables, :instance_variable_get, :instance_variable_set,
  :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?,
  :is_a?, :tap, :send, :public_send, :respond_to?, :extend, :display, :method,
  :public_method, :singleton_method, :define_singleton_method, :object_id, :to_enum,
  :enum_for, :equal?, :!, :!=, :instance_eval, :instance_exec, :__send__, :__id__]

```

Wow. That was verbose, but don't be afraid. The call to `methods`
just returned a collection of method names. Each of these is a message we can send.
They start with a `:` and are separated by a commas in a list.

So, any of these methods can be called on our number `3`, at least in theory. The
thing we don't know from this list is whether they need arguments or not. Let's try a
few.

What about `quo`, maybe it quotes things.

```ruby
  3.quo

  # ArgumentError: wrong number of arguments (0 for 1)
	#   from (irb):1:in 'quo'
	#   from (irb):1
	#   from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in '&lt;main>'
```

So, we are getting feedback that we didn't provide the right number of arguments.
We can see we passed no arguments, or 0 arguments, and instead 1 was required.
Since we are working with numbers and don't know yet what `quo` does, I want to
try passing it another number to see it will be happy and do something magical.

```ruby
  3.quo(4)
  # => (3/4)
```

It returns a ratio, and since Ruby tries to make intuitive method names, I
will infer that `quo` means quotient not quote like I originally imagined.

Let's try a few more where we can make some guesses:

```ruby
  # `next` method ... anticipating next number
  3.next
  # => 4
  # cool it worked like I thought

  # `prev` method ... anticipating the previous number
  3.prev
  # => 2
  # woot!
```

## Solo Exercises
* Numbers in Ruby are weird sometimes. What happens when you do division like this: `1 / 3`? Is it what
you expected? Are there methods on these numbers you can use to get the number you would expect
from this kind of division?
* What is `gcd` on our integer numbers. Experiment with different numbers first to try to figure it out.
When you have a guess, check the docs to see if your guess is correct.
* Figure out what methods `true` and `false` respond to. What methods do they have in common with numbers,
and what do those methods do?

## Group Exercises
* Review above
