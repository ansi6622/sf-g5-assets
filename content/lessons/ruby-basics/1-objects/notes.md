---
blooms: knowledge / understanding
published:
---

# Everything is an object
[deliverable](deliverable)

## Goal

Understand the implications of everything being an object!

## Objectives

* Learn to call methods on numbers and other 'primitives'
* Understand operators and method calls
* Introduce Ruby introspection, by asking objects for their methods

## Prerequisites

* Reading and exercises in [Learn to Program](https://pine.fm/LearnToProgram/)

## Gain Attention
Who can name me an object in Ruby?
How many objects are there in Ruby?

Ruby is an object-oriented language. But what does that really mean?
Let's dig in to how Ruby thinks about the world.

## Inform learner of objective

Probably something like: Draw a mind-map of the topic, with a branch for Objectives listed above

## Stimulate recall of prior information

What is an object oriented language?
Who can name other OO languages?
What is an object?

## Present the stimulus (I do)

### Objects have methods

#### Asking an object for information
```ruby
4.even?
# => true
```

#### Asking an object to do something

```ruby
  3.2.round
  # => 3

```

### Calling Methods
#### Use the dot operator
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

#### Send a message

```ruby
  3.send :to_s
  # => "3"

  1.25.send :round
  # => 1

  4.send :zero?
  # => false
```

which is equivalent to:

```ruby
  3.to_s
  # => "3"

  1.25.round
  # => 1

  4.zero?
  # => false
```

### Operators are methods too

```ruby
  3 + 1
  # => 4
```
is equivalent to:

```ruby
  3.+(1)
  # => 4
```

### Finding Methods

#### Listing all the methods of an object

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

#### Trying out a method (with error)

```ruby
  3.quo

  # ArgumentError: wrong number of arguments (0 for 1)
  #   from (irb):1:in 'quo'
  #   from (irb):1
  #   from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in '&lt;main>'
```

#### Trying out a method

```ruby
  3.quo(4)
  # => (3/4)
```

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

## Provide learner guidance

Emphasize that send is a bad idea and students shouldn't really use it.

## Eliciting performance / Giving Feedback (We do)

Have the students open up IRB.
Ask students for some methods from the list above to try out.
Have students form a hypothesis about what the result will be.
Then everyone call the method on the object.

Pick a different type of object and repeat.
