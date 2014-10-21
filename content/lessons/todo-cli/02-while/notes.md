---
blooms: understanding IO, applying basic ruby
publish:
---

## Goal:
Write programs that respond to user input

## Objectives
* While loops for command line applications
* Input and Output (I/O)

## Prerequisite
* [Basic Ruby lessons](/lessons/basic-ruby/deliverable) - or equivalent
* [CLI- basic lesson](/lessons/todo-cli/02-cli)

## Materials
* git repository: git@github.com:gschool-g5/todo-cli.git

----------

## Gain Attention
We want to keep getting user input until the user is ready to quit.
Therefore we need a loop that just keeps asking

## Inform learner of objective
* `while` loops for command line applications
* More about input and output (I/O)

## Stimulate recall of prior information
Remember using `bundle`? It turns out that `bundle` is a command line application
written in Ruby. `rails` is too. Lot's of basic Ruby libraries include a CLI.

## I do
As you write code, prompt class to hypothesize what will happen next

```ruby
while true
  # get some input
  # do something with that input
end
```

Will fail:

```ruby
while (user_input = gets) != 'quit'
  puts user_input.inspect
  # just keep going
end
```

Should work:

```ruby
  while (user_input = gets.chomp) != 'quit'
    puts user_input.inspect
  end
```

Responding to a menu of number inputs:

```plain
Welcome to our command line app.
Type a number to do the corresponding action:
1. Keep looping
2. Quit
```

Will fail:

```ruby
  while (user_input = gets.chomp) != 2
    puts user_input.inspect
  end
```

Should work:

```ruby
  while (user_input = gets.chomp) != '2'
    puts user_input.inspect
  end
```

Talk about using number vs string. When is it good

### Provide learner guidance
* `while` loops are almost never used in Ruby. CLIs is about the only real use case

## We do

```gherkin
  Given I run my app with `ruby guess-me.rb`
  And the application picks a hidden number between 1 and 100
  Then I will be prompted to guess a number between 1 and 100
  When my number is higher than the game's number
  Then I will see a message that my guess was too high, and be prompted to guess again
  When my number is lower that the game's number
  Then I will see a message that my guess was too low, and be prompted to guess again
  When my number matches the game's number
  Then I will see a a message that I won
  And the game will end
```

## You do

* Work on the next set of tests that quitting and looping

### Provide learner guidance
* Work on this one test at a time
* Write new tests when done with existing ones
* Make it pass and move on

## Solo Stretch Exercises
1. Reverse the guessing game. Have the computer guess the number in your head:
```gherkin
  Given I run my app with `ruby computer-guesser.rb`
  Then the computer will volunteer a number between 1 and 100
  And the computer will offer a list of options:
    1. too high
    2. too low
    3. correct!
  When I enter too high
  Then the computer will make a new guess that is lower
  When I enter too low
  Then the computer will make a new guess that is higher
  When I enter correct
  Then the computer will report how many quesses it took
```
2. Test it by copying the design patterns in the project in the solo exercises
3. Detect obvious cheating: A person running the application could change their
number mid game. If they keep doing it, they will eventually get caught. How could
you hold state about the numbers guessed in order to see if a person was trying
to game the system
4. Find a way to separate the code that runs the game from the actual command line
inputs. (See the exercise about testing the code.) Now that it is separated. Run
the code 100 times with a randomly generated guess to see what the average guess
is.
