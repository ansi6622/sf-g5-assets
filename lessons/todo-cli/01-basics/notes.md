---
blooms: knowledge
published:
---
# I/O
[deliverable](deliverable)

## Goal
Learn to get user input and print to the screen

## Objectives:
* Learn about command line programs
* Deeper usage of `puts` and `gets`
* Introduce streams/IO

## Prerequisites
* Ruby basics

## Material
* git repository: git@github.com:gschool-g5/todo-cli.git

## Next in the series:
[02-cli](/lessons/todo-cli/02-cli/deliverable)

## Gain Attention
Rails has lots of bells and whistles that can distract.
We are going to start with just Ruby building something simple you can interact with.

## Inform learner of objective
* Learn more about `puts` and `gets`
* Introduce deeper topic: streams and IO

## Stimulate recall of prior information
Remember using `bundle`? It turns out that `bundle` is a command line application
written in Ruby. `rails` is too. Lot's of basic Ruby libraries include a CLI.

## I do

#### `puts`

* Who can tell me about `puts`?
* Talk about what it does basically

-----

Make project:

```bash
  mkdir basic-cli
  cd basic-cli
  touch cli.rb
  atom .
```

-----

```ruby
 puts "What is your name?"
```

```bash
  ruby cli.rb
```

#### `gets`

* Flip side of `puts`
* Basic usage

```ruby
  name = gets.chomp
  puts "Hello #{name}"
```

#### IO Streams

* Where does `puts`, `gets` come from
* What other things have these methods

### Provide learner guidance

* Also, `gets` is only used in these interactive applications, which is rare


## We do

*Class discusses:*

1. In ruby, how do you print things out to the terminal?
1. What about getting input from the terminal?
1. What are other types of input and output? Brainstorm a few. Maybe in a group.

## You do
* Testing puts and gets is hard! Why fuzzy hand waving
* Clone/fork the exercise
* Run through first few tests

### Provide learner guidance
* Work on this one test at a time
* Write new tests when done with existing ones
* Make it pass and move on
