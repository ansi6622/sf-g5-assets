# Goal: Write programs that respond to user input

## Prerequisites
* Ruby basics - while loops

## Objectives

* `while` loops for command line applications

### Looping for input

It's cool that our program can print output to the user and get user input,
but we want to start doing different things depending on different input.
It would also be nice if we could keep the program running until the user
decides to quit.

That is a pretty common need when it comes to command line applications. They
print information and then wait for input. When they get the input, they process
it in some way and wait for more input.

It is pretty rare in Ruby to need a while loop, but this is just one of those
cases. While we are not at some ending condition we want our app to keep getting
input from the user and responding.

What if we added this to our program?

```ruby
  while true
    # get some input
    # do something with that input
  end
```

In this case, we will just loop forever. Maybe we want that, but it is much
more likely that we want to stop and exit when the user tells us they are done.

Let's write some code stop when a user types 'quit'.

```ruby
  while (user_input = gets) != 'quit'
    puts user_input.inspect
    # just keep going
  end
```

Did that work? Why not?

```ruby
  while (user_input = gets.chomp) != 'quit'
    puts user_input.inspect
  end
```

Success. Now let's change it a little. Let's imagine a menu where we have numbers
for commands instead of having to type full words:

```plain
Welcome to our command line app.
Type a number to do the corresponding action:
1. Keep looping
2. Quit
```

Let's try coding that ...

```ruby
  while (user_input = gets.chomp) != 2
    puts user_input.inspect
  end
```

Did that work? Why not?

Let's try again:

```ruby
  while (user_input = gets.chomp) != '2'
    puts user_input.inspect
  end
```

We could also have written as our while conditional `(user_input = gets.chomp).to_i != 2`. It
depends on whether you want to use the number as a number, or if a string is good enough.


## Group Exercise

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

## Solo Exercise
* Work on the next set of tests that quitting and looping

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
