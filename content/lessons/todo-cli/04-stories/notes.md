---
blooms: understanding
publish:
---

## Goal:
Understand the story writing conventions

## Objectives
* Be able to read gherkin stories and convert specs and working code
* Construct gherkin stories from specs

## Prerequisite
None

## Materials
* git repository: git@github.com:gschool-g5/todo-cli.git

----------

## Gain Attention
We have been seeing exercises and assessments written in this weird story format.
Let's

## Inform learner of objective
* Be able to read gherkin stories and convert specs and working code
* Construct gherkin stories from specs

## Stimulate recall of prior information
Remember in our lesson on cli `while` loops how our group exercise included a
story written in the Given-When-Then style?

## I do

It turns out this style of writing specifications is called gherkins.

```gherkin
  Given *some condition*
  When *some action*
  Then *some event occurs*
```

Go through a couple of the first specs in the cli project:

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

## We do
* Look at the cli project and come up with stories for each set of specs

## You Do
* Write stories for a rock, paper, scissors game
* Continue with the exercises for the Todo cli if you haven't finished

## Stretch exercises:
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
