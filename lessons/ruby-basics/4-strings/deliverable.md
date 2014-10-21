---
title: Ruby Basics - Strings
blooms: understanding
---

# Goal: Understand Strings

## Objectives
* Know the difference between single and double quoted strings
* Methods on strings
* Strings as a collection of letters
* Evaluating Ruby inside strings

## Prerequisites
* Reading and exercises in [Learn to Code](https://pine.fm/LearnToProgram/)
* Lesson on basic ruby: [everything is an object](/lessons/ruby-basics/1-objects)

-------

## Text is an important part of programming

Remember back to the last time you used a website or an application. Unless you
were using a game or a very unusual, super-visual app, you were surrounded by
text in the form of:

* labels
* names
* descriptions of data
* data
* ... almost everything

We store text inside programming constructs called string. The reason they are
called strings is because they are consist of a string of letters:

<img src="http://i01.i.aliimg.com/wsphoto/v0/533098499/1-shining-noble-love-letters-flash-drill-necklace-fashion-jewelry-short-Women-necklace-new-product.jpg">

In Ruby strings are designated by quotes, which is easy to remember because English
works that way when we are trying to directly quote other people.

```ruby
  "I am a string"
  'I am also a string'
```

### Quote types

Strings can be in single quotes `'`:

```ruby
  'Hello world'
  # => "hello world"
  # whoa! it got converted to double quotes in IRB
```

Strings can be in double quotes `"`:

```ruby
  "Hello world"
  # => "Hello world"
```

So if you want to put a double quote into a string (maybe because you are
storing quoted text) you can use single quotes:

```ruby
  'I said, "Hello"'
  # => "I said, \"Hello\""
  # huh? is that a preview of what is to come?
```

But you could also escape the quotation marks inside double quotes,
so that Ruby knows not to end the string. You do that with a back-slash:

```ruby
  "I said, \"Hello\""
  # => "I said, \"Hello\""
```

You can escape single quotes within a single quoted string too:

```ruby
  'What\'s up?' == "What's up?"
  # => true
```

And it looks like you can compare strings with an equality statement.

### Methods on Strings

Even though strings are a very basic things provided by the language, they are
also objects ... like everything in Ruby. There are a whole bunch of methods
built into strings, making them useful without writing a single line of code:

```ruby
  "hello".upcase
  # => "HELLO"

  "hello".center(20)
  # => "       hello        "

  "       hello        ".strip
  # => "hello"

  "hello".center(20).strip
  # => "hello"
  # well that was pointless

  "hello".length
  # => 5

  "hello".size
  # => 5
  # that's the same as length!
  # sometimes Ruby aliases of methods so we can guess at the right method name
```

The resources section list the Ruby docs for String. There are lots of methods.
You don't have to memorize them. In fact, please don't, it will mostly be a
waste of time. The documentation just stays around waiting for
you. You do have to know what is possible so you can go to the docs and look it up.

### Math with Strings

Ruby is fun. It turns out you can do math on strings, even though you can't do math
in real life on text. Here are some examples:

```ruby
  "hello" * 3
  # => "hellohellohello"

  "hello" + " " + "world"
  # => "hello world"
```

After that things get a little more error prone and dissatisfying. That will be an
experiment for later.

### Indexes and Substrings

Strings are really justs lists of letters. You can
access individual characters of a string, with square bracket notation:

```ruby
  "hello"[0]
  # => "h"

  "hello"[1]
  # => "e"

  "hello"[2]
  # => "l"

  "hello"[3]
  # => "l"

  "hello"[4]
  # => "o"
```

The 'index' number in the square bracket always starts at 0 and increases with each
character by 1.

You can also count backwards from the end.
```ruby
  "hello"[-1]
  # => "o"

  "hello"[-2]
  # => "l"

  "hello"[-3]
  # => "l"

  "hello"[-4]
  # => "e"

  "hello"[-5]
  # => "h"
```

Getting a subset of the original string, or a substring, can be done with square
bracket notation too:

```ruby
  "hello"[0..3]
  # => "hell"
  # oops
```

Notice how Ruby lets you use elipses-like syntax to indicate a range of numbers
for the index.

Ranges can also use negative numbers:

```ruby
  "hello"[3..-1]
  # => "lo"
```

### Substitution in Strings

It is a pretty frequent programming practice to want to substitute one bit of text
for another bit of text. With more of our magical Ruby methods it is pretty easy:

```ruby
  "I don't know. I just don't understand. I don't get it".gsub("don't", "do")
  # => "I do know. I just do understand. I do get it"
```

The g in `gsub` stands for global. So the method does a global substitution of "don't"
for "do". There is a companion method `sub` that will just replace the first instance
of the match.

```ruby
  "I didn't believe. I didn't understand.".sub("didn't", "did")
  # => "I did believe. I didn't understand."
```

The funny thing about these string methods is that they don't change the original string.
Let's set a variable to a string, call methods on it and check what happened.

```ruby
  buffoonery = "bluster and blow"
  # => "bluster and blow"

  buffoonery.upcase
  # => "BLUSTER AND BLOW"

  buffoonery
  # => "bluster and blow"
```

There are methods on string that will change the string permanently, not just return
a changed string. These usually have a `!` in the name:

```ruby
  buffoonery = "bluster and blow"
  # => "bluster and blow"

  buffoonery.gsub!("b", "")
  # => "luster and low"

  buffoonery
  # => "luster and low"
```

You will probably also see this permanent change called 'mutation'.
Methods that end in a '!' mutate the string.

### Putting Ruby Inside Strings - String Interpolation

Remember how we can do some simple addition with strings?
For strings, addition just glues the strings together.

```ruby
  full_name = "John" + " " + "Doe"
  # => "John Doe"
```

Kind of ugly, but it works.
What if we wanted to glue a couple of variables together?

```ruby
  first_name = "John"
  last_name = "Doe"

  full_name = first_name + " " + last_name
  # => "John Doe"
```

Well, this is a bit of a bummer - we have to remember to put in that extra space,
and it doesn't read all that nicely.

Luckily, Ruby provides a nicer way to accomplish our goal called string
interpolation.

Observe:

```ruby
  first_name = "John"
  last_name = "Doe"

  full_name = "#{first_name} #{last_name}"
  # => "John Doe"
```

The really cool thing about string interpolation is that it will work with any
Ruby that we want:

```ruby
  "2 + 2 = #{2 + 2}"
  # => "2 + 2 = 4"
```

The syntax for evaluation within a string is `#{some ruby expression}`. It only
work inside double quoted strings. This is the first real difference we have seen
between using strings with a single and double quote.

Notice how in the example, the first part was a real string, but the part in the
`#{}` block was evaluated as Ruby and turned into the number 4.

We often get very convoluted and abstract, evaluating strings within strings:

```ruby
  "hello #{"world".upcase}"
  # => "hello WORLD"
```
## Group Exercise
* Play with strings and math: What happens when you ...
    * add a number to a string?
    * add a string to a number?
    * subtract one string from another?
    * use other math operations

## Solo Exercises
* Try all the examples yourself in IRB; experiment with small changes to see what happens
* Experiment with at least 5 other Ruby string methods and figure out what they do. Don't
read too much about them. Just experiment.
* Figure out a way to append a number to the end of a string. Can you find at least one other way to do it?
* What happens if you access a string by index of any number larger than the size of the string?
* Do you get the same result accessing a string by index that is a very large negative number?
* Why do you get no result when evaluating this Ruby: `"hello"[-1..-2]`
* What are some other methods with a '!' in their name that permanently change the string value?

## Group Exercises
* Review Solo Exercises

## Assessment

```gherkin
  Given the string "The quick brown fox jumps over the lazy dog."
  When your script is run
  Then I will see any character 'e' converted into a 3
  And  I will see all the other letters capitalized
```

## Resources

* [Ruby Documentation: String](http://www.ruby-doc.org/core-2.1.2/String.htm[]())
* [Wikipedia: Strings (Computer Science)](http://en.wikipedia.org/wiki/String_(computer_science))
* [JumpstartLabs: String Tutorial](http://tutorials.jumpstartlab.com/projects/ruby_in_100_minutes.html#3.-strings)
* [RubyLearning: More on Strings](http://rubylearning.com/satishtalim/more_on_strings.html)

## Extra Credit

* Research 'heredoc' in Ruby. What would this be good for? Does string interpolation work in heredocs?
* Character sets have an encoding. The original programing encoding is ASCII which encompassed 128 characters
in the Latin alphabet. Now we live in a world where the character sets in strings are very big. Research what are the
common encodings. What are some of the ways that encoding is handled in Ruby 2.0 and greater? (There are lots of
right answers!)
