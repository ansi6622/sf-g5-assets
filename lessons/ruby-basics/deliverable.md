---
title: Ruby Basics
blooms: understanding, generally. Other blooms for subsections
---

# Goal: Learn Ruby Syntax

# Objectives
* Understand everything in Ruby is an object, with methods and a class
* Recognize and understand different variables types
* Understand common control flow patterns
* Get comfortable with common Ruby objects: Strings and Collections
* Understand iteration over collections, and iteration more generally
* Recognize symbols, regexes, nil and other Ruby objects
* Understand scopes, methods and classes

----------

## Ruby is your tool for the next 3 months, intensively
#### You need to know how it works in detail

Remember your assigned prerequisite to work through Chris Pine's Learn to Program?
That should have taught you about basic programming and Ruby ideas.

Every programming language is made up of basic building blocks that can be used
to assemble bigger and more complex stuff. This is the section where we cover
Ruby concepts again. Getting these right will save an amazing amount of
pain down the line, and ultimately determine how well you do in the course.

Before we dive into a bunch of sub-lessons. Let's look at two ways to run your
Ruby code.

#### IRB - An Experimentation Playground

Ruby comes with a playground for trying out code without having to go through the
bother of saving it in a file.

Once you have installed ruby on your system, IRB is a freebee.

Type 'irb' in your terminal. You should see a number that follows the pattern 2.X.X.
This is the version of ruby that you are running.

```bash
  $ irb

  2.1.2 :001 > 1 + 1
   => 2
  2.1.2 :002 >
```

In my case, I am running Ruby 2.1.2. The number after the Ruby version number is the
line number.

After the '>' prompt, you can write Ruby code.

If the code isn't legal, IRB will sometimes throw an error. Don't panic!

```bash
  2.1.2 :002 > 1 + gerbil

  # NameError: undefined local variable or method 'gerbil' for main:Object
	#         from (irb):2
	#         from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in '&lt;main>'

  2.1.2 :003 >
```

Experimenting with what will work and what won't is part of programming.

Sometimes things go very bad in IRB, and the console stops responding or is in
weird state where code behaves very un-Ruby like.

Don't panic! This happens all the time and there is a magic escape hatch

`ctrl-c` or if that doesn't work `ctrl-d`

If all else fails, close your terminal. You didn't break your computer. Everything
is fine.


#### Ruby in the file

It is much more common to write your Ruby in a file and then run that file as Ruby.

We will be writing our Ruby in a code editor called 'Atom'. You already downloaded
it, and now you can, from the command line open any directory by typing this in the
terminal:

```bash
  atom ./
  #  - or -
  atom .
  #  or even just
  atom
```

Right now we are going to go to our gSchool directory and open it in atom:

```bash
  cd ~/Projects/gSchool
  atom .
```

Let's make a new file called 'ruby/_in/_the/_file.rb'. Do you remember from the
command line how to create that file?

```bash
  touch ruby_in_the_file.rb
```

The `.rb` at the end of the file let's you and your code editor know that this
file is written in Ruby. It doesn't however make Ruby just run the file automatically
when you call it on the command line. So to run the file, you need to ask ruby to
do it:

```bash
  ruby ruby_in_the_file.rb
```

Now, let's look at that file in Atom. Nothing is there. Let's put a little Ruby
into the file and re run it from the command line:

```ruby
  puts "Hello gSchool!"
```

#### Ruby in bigger projects

Rails and other bigger projects will need to require a number of files in order
to accomplish their big goals. These bigger projects have special starting scripts.
For example Rails is a command line application that responds to several commands
in order to run its code. Here are some examples: `rails server`, `rails console`.

For these bigger projects, you have to know that tool in addition to pure Ruby.

You have to learn those tools in addition to Ruby to know what to do. Our class
is going to focus a lot on Ruby, but we'll try some other big Ruby systems too.

## Lessons
1. [Everything is an object  ](/lessons/ruby-basics/1-objects/deliverable)
1. [Varying with Variables   ](/lessons/ruby-basics/2-variables/deliverable)
1. [In the Flow              ](/lessons/ruby-basics/3-flow/deliverable)
1. [Strings                  ](/lessons/ruby-basics/4-strings/deliverable)
1. [Collections              ](/lessons/ruby-basics/5-collections/deliverable)
1. [Iterating                ](/lessons/ruby-basics/6-iteration/deliverable)
1. [Methods & Functions      ](/lessons/ruby-basics/7-methods-functions/deliverable)
1. [Objects Again            ](/lessons/ruby-basics/9-objects-redux/deliverable)

## Resources
* [Command Line & IRB](http://tutorials.jumpstartlab.com/projects/ruby_in_100_minutes.html#1.-instructions-&-interpreters)

Sometimes it takes many different ways of seeing something to really understand it.
Here are a lot of learn Ruby resources. Be mindful though that in programming, reading
is _not_ learning. Experimenting, trying and often failing is learning.

* [Learn To Program](https://pine.fm/LearnToProgram) by Chris Pine
* [Ruby Pickaxe Book (online)](http://ruby-doc.com/docs/ProgrammingRuby/)
* [Ruby in Twenty Minutes](https://www.ruby-lang.org/en/documentation/quickstart/)
* [Ruby Learning](http://rubylearning.com/satishtalim/first_ruby_program.html)
* [Railsbridge](http://curriculum.railsbridge.org/ruby/)
* [Learn Ruby The Hard Way](http://ruby.learncodethehardway.org/)
* [Try Ruby](http://tryruby.org/levels/1/challenges/0)
* [Simple Ruby Exercises](http://www.techotopia.com/index.php/Simple_Ruby_Examples)
* [Ruby Kickstart](https://github.com/JoshCheek/ruby-kickstart)

------
## Exercises

* [Grading](https://github.com/gSchool/grading-ruby)
* [Practice Assessment](https://github.com/gSchool/denver-practice-assessment-week-3)
* [Iterating through dogs ( and owners )](https://github.com/gSchool/iterating-arrays-of-hashes)
* [Assessment Week 4](https://github.com/gSchool/denver-assessment-week-4)

* [Ruby basics](http://tutorials.gschool.it/ruby_basics) :: includes high level acceptance tests
* [Ruby Monk](https://rubymonk.com/)

* [Ruby Kickstart](https://github.com/JoshCheek/ruby-kickstart) ??

## Assessment

* script that does line breaks
* class that does line breaks
