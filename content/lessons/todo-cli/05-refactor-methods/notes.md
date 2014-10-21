---
blooms: understanding refactoring, applying method ruby basics
publish:
---

[deliverable](deliverable)

## Goal:
Clean up the code in the todo cli

## Objectives
* Extract methods from our command line application
* Work at finding the right name for methods

## Prerequisite
* Completed command line application from previous lessons

## Materials
* git repository: git@github.com:gschool-g5/todo-cli.git

## Gain Attention
Our CLI todo app works, but it is quite messy.
Let's take a look at 3 people's applications:
  * if you didn't write this how easy would it be to change
  * what if there was a bug? how long would it take to find it

## Inform learner of objective
* Be able to extract methods from any messy code

## Stimulate recall of prior information
Remember when we studied methods in Ruby.

## Present the stimulus (I do)

Methods are ways of grouping logic and giving it a name.

Let's say that again. Methods
  * group logic
  * allow us to name the group

Breaking code into smaller parts in any language is a fundamental
part of cleaning up and keeping a code base clean.

This cleaning process is called *refactoring*

Naming things allows us to understand easier what the little module of code is for.

These are the steps I did for refactoring this:
* extract the input methods 'gets.chomp'
* extract the print methods, anything with a puts
* extract the end points of each if statements

## Provide learner guidance
* Look for repeating chunks of code and remove them into a methods
* Group complicated conditionals into method names ending in a question mark
* Look for appropriate names, and look hard. It is one of the hardest problems in CS

## Eliciting performance / Giving Feedback (We do)

* Clamshells down
* Grab the messiest of the three examples shown, and mob refactor

1. recognize the gets.chomp repetition
2. notice the other printing methods to pull out
3. break each of the if statements related to a command/section into own method

## Solo Exercise
* Refactor your own code for this projects into methods

## Stretch Exercise
* We will post other people's code, fork refactor and push those to your fork
