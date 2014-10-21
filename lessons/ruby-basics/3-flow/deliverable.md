---
title: In the Flow
blooms: understanding
---
# Goal: Understanding if-else-elsif blocks, and other branching logic

## Objectives
* Understand if statements in all their incarnations
* Comparison operators in Ruby

## Prerequisites
* Reading and exercises in [Learn to Program](https://pine.fm/LearnToProgram/)

-------

## Programs need to do different things depending on their environment

Ok, remember when we talked about how variables contain unknowns because when we
write our code we can't predict what will happen when the application is run?
We used the number of students that might be sick on a given day as our example.

It could be that we want to cancel class if greater than 90% of our students are
sick.

That kind of choice between two (or more options) is what flow control is for:

```ruby
  if sick_students > 0.9 * total_students
    class_cancellation.notify!
  end
```

This variability in the procedure is called 'control flow'. Related to this is
'conditionals'. We will cover both in this section.

### Getting Ify with `if` statements

You're already familiar with some common ways of controlling the flow using `if`
statements.

```ruby
  if rand(10) > 5
    puts "I am biggish"
  else
    puts "I am smallish"
  end

  # I am smallish
  # => nil
```

If you run that script several times, the if statement will puts out different
things because `rand(10)` generates a random number between 0 and 9. Sometimes
that number is greater than 5, sometimes it is not. The code runs different
parts of the procedure depending on randomness.

Here is a useful thing you may not know:
`if` statements return something. The `if` statement is not just a fork in
the procedural road, it actually returns whatever the last statement in the chosen
branch returns.

```ruby
  description = if rand(10) > 5
    "I am biggish"
  else
    "I am smallish"
  end

  description
  # => "I am biggish"
```

That brings us to another important Rubyism, _everything_ in Ruby returns something,
even if that something is nothingness ... or `nil`.

```ruby
  puts "Hi"
  # "Hi"
  # => nil
```

The return value of `puts` is always `nil`, which leads to some confusing looking
output.

### Truthiness, Equality & Nots

You can think of truthiness as anything that will make an `if` statement fall into
the first branch of the statement.

In order to really explore that we should know more about comparison operators in Ruby.

To test equality you use two equal signs: `==`.

```ruby
  1 == 1
  # => true

  1 == 2
  # => false
```

And of course because everything in Ruby is an object, this `==` operator is really
a method on objects.

You can also check for the inverse of equality with `!=`

```ruby
  1 != 1
  # => false

  1 != 2
  # => true
```

It is pretty common to not compare things but just ask whether they are truthy or
not. A great way to check if something is not truthy is with the not operator `!`.
You sometimes see `!!` before a thing to convert it into it's `true` of `false` equivalent.

```ruby
  !true
  # => false

  !!true
  # => true

  !'foo'
  # => false

  !!'foo'
  # => true

  !!nil
  # => false
```

Rubyists are lazy though (in a good way), and it is just as easy to throw something
into an if statement
and see if it succeeds. And because everything returns something, even assignment will
return the thing that was assigned.

These two if statements work the same, except that we also get an assignment with
our if statement.

```ruby
  if 'foo'
    puts 'foo'
  end

  if string = 'foo'
    puts string
  end
```

#### Mixing our truths

Most programming languages acknowledge that one truth is not enough. Sometimes
we want to know that someone is younger than me, but older than my daughter.

_Demanding all conditions with `&&`_

```ruby
  # assuming some people objects with #age methods, and
  # an event with an #invite method ...

  # using nested if statements
  if elisa.age < me.age
    if elisa.age > daughter.age
      event.invite(elisa)
    end
  end
```

Instead of nesting if statements we can combine them together with `&&` the logical
'and' operator.

```ruby
  # combining conditions with `&&` makes it a little cleaner
  if elisa.age < me.age && elisa.age > daughter.age
    event.invite(elisa)
  end
```

We can also sometimes want to go forward if only one of the conditions is true.

_Demanding some truthiness with `||`_

```ruby
  # assuming more people with a #like? method, and that same event object
  if me.like?(elisa) || you.like?(elisa)
    event.invite(elisa)
  end
```

#### Else if ...

So far we have been building conditional flows with only one or two branches. Often we
need more than that. For those cases we have `elsif`. It is a weird non-English
word which is pretty unusual for Ruby. So, pay close attention. Ruby will throw
an error if you try to correct the spelling.

```ruby
  # assuming a gerbil object that responds to #fuzzy? and #bald?
  if gerbil.fuzzy?
    puts 'pet the gerbil'
  elsif gerbil.bald?
    puts 'maybe its a rat'
  else
    puts 'gerbil is odd'
  end
```

#### Tail Conditions

Ruby has an awesome syntax that allows you put an `if` or `unless` statement as
a tail condition. Huh? Let's just look at it in action:

```ruby
  puts "Hello World" if chatty?
  # "Hello World"
  # => nil

  puts "Hello World" unless grumpy?
  # => nil
```

So, in those cases where you have only one branch. The branch goes
first and the conditional statement at the end, a tail condition.


This is a pretty handy shorthand for a branch of code that fits on a line. Also,
while it is possible to use `unless` the same way as `if` with `else` and `elseif`,
please don't. The only justice if you do something like this is having to maintain
your own code.

#### Ternary If Statements

`if`s can get so brief that they don't even look like `if` statements. This is the
case of a ternary statement. It is just a question mark and a colon, all in a very exact order.
Most languages have this kind of syntax, and it makes sense so long as the statement
is very brief:

```ruby
  description = number > 1000 ? "that is big" : "that is small"
```

In this case we are setting `description` to a string depending on whether `number > 1000`
is `true` or `false`. If it is `true`, it goes into the part between the `?` and the `:`.
Otherwise it will go into the part after the `:`.

#### Memoization

No, I didn't mean memorization. I meant memoization. It means store a value if it is not
already stored. Typically you see this with instance variables, but it works with declared
local variables too.

But, wait, why is this weird storage thing in this section? Well, it is really just shorthand
for a particular kind of `if` statement.

```ruby
  @foo ||= 'foo'
```

What we are saying here with an `||` combined with an `=` is, if this `@foo` is falsey, set
it to this other thing on the right side. We could rewrite it like this with a ternary.

```ruby
  @foo = @foo ? @foo : 'foo'
```

Or we could rewrite it with some larger full if statement:

```ruby
  if !@foo
    @foo = 'foo'
  end
```

Why is memoization useful? Sometimes we want to have a variable that we can set manually,
but otherwise it gets set to a default value.

#### Other uses for && and ||

Mostly in other languages, but sometimes in Ruby, you will see `&&` and `||` used as if statements.
This is a little exotic and you should just try to use any of the other syntaxes instead. Let's look
at an example anyway. You might run into in in other people's confusing code.

```ruby
  # assuming people objects with the method #like? and the event object with #invite
  me.like?(elisa) && event.invite(elisa)

  # equivalent if statement
  event.invite(elisa) if me.like?(elisa)
```

### Other flows

In other languages it is common to see `while` and `for` loops. Ruby is forgiving and
allows programmers to use these constructs too. It is much more common to use built in
iterators. We will cover those in a whole section on its own.

Ruby also has case statements, which are mostly unused. We will cover them in the exercises
and assessments.

------

## Group Exercises
Go over all the code above as a group.

## Solo Exercises
* What is the difference between `==` and `===`, between `!=` and `!==`? Go look it up on the internets!
* By exploring truthiness, figure out all the values in Ruby that are falsey.
* Ruby also comes with `and` and `or`. What is the main difference between `&&` and `||`
and how can you get into trouble with these?
* Case statements are like if-else statements. Research them; what are the
advantages and disadvantages?
* Use a `while` and `until` loop. What is the main difference? What about a `for` loop.

## Group Exercise
* Review above
* Together, do the clone and repurpose flow in part two

## Assessment
* Do the following story using if statements

```gherkin
  Given I run the my script with 'ruby ageist.rb'
  Then I will see the statement 'Age is _' where _ is a random number between 0 and 110
  When the age is 1 or less it will report the age range is a          'baby'
  When the age is less than 10 it will report the age range is a       'child'
  When the age is between 10 and 12 it will report the age range is a  'tween'
  When the age is between 13 and 19 it will report the age range is a  'teenager'
  When the age is between 20 and 40 it will report the age range is a  'adult'
  When the age is between 40 and 65 it will report the age range is a  'middle age'
  When the age is between 66 and 100 it will report the age range is a 'senior'
  When the age is over 100 it will report the age range is a           'record breaking'
```

* Ruby also has case statements, which act very similar to big if-else statement. Write
another script for the story above that uses a case statement instead of an if-else
statement.
