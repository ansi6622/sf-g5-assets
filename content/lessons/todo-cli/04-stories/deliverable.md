# Goal: Understand Stories

## Objectives
* Understanding how gherkin stories are written
* Construct stories from existing tests

### User stories
One thing that can really help when building software is thinking about it in
terms of stories or flows that a user will do. In this class we will use a story
syntax called 'gherkin' that came from a Ruby testing framework called 'cucumber'.
Gherkin is a tiny language that computers can understand, but reads very nicely
for humans as well (just like Ruby!)

A user story is typically a short sentence or two that describes what
a user can do or is trying to do with some software in plain english.
For example, a user of our todo command wants to be able to list all of the
things that are on the todo list. Or, the user wants to be able to add a new
todo item.

In order to help capture all of the relevant information (and leave out
irrelevant information!) stories in 'gherkin' are written like this:

```gherkin
  Given *some condition*
  When *some action*
  Then *some event occurs*
```

Let's convert the first set of tests for our CLI todo app into
stories:

```gherkin
  Given I run the cli todo app
  Then I will see a menu
```

```gherkin
  Given I run the cli todo app
  When I type 'continue'
  Then I will the application will continue to wait for input
```

```gherkin
  Given I run the cli todo app
  When I type 'quit'
  Then the application will stop
```

Together let's convert the rest of the stories ...


### Exercises
* Write stories for a rock, paper, scissors game
* Continue with the exercises for the Todo cli if you haven't finished

## Stretch Exercises
* Implement the rock, paper, scissors game in Ruby with tests
* Change the stories, the tests and then the implementation to include [lizard and spock](http://en.wikipedia.org/wiki/Rock-paper-scissors-lizard-Spock)
* Write stories for a small [text adventure game](http://en.wikipedia.org/wiki/Interactive_fiction)
* Write tests and implement that text adventure game!
* Write stories for a command line application that organizes hospitals and their staff
with the following data relationships:
  * Hospitals have names
  * Hospitals have many doctors and many nurses
  * Doctors have names and annual salaries
  * Nurses have names and hourly wages
* Write specs and implement a series of CLI menus to edit this kind of data
