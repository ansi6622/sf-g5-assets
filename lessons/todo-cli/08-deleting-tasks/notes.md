---
Blooms: application
published: 
---

# Deleting from files (Application)

[deliverable](deliverable)

## Goal

Students can delete things from the middle of a file.

## Objectives

* Demonstrate the tediousness of traversing file content when not using a database
  or library.
* Students can write a ruby script that deletes an item from a file.
* Students understand the importance of an id field.

## Prerequisites

* Persistence lesson

## Materials

* preloaded CSV file for students

## Gain Attention / Inform Learner of Objective

Write a todo list on the whiteboard. Erase one from the middle and demonstrate
the tedious process of having to individually move each one below up to its
new spot.

What if todo lists in real life never got any smaller, but just got added to?
That would suuuck! We need to be able to delete our todos!

## Stimulate recall of prior information

Recall deleting todos from our rails todo app from the console.

## Present the stimulus (I do)

See the whiteboard note in Gain attention section. Now have class
brainstorm solutions to this problem.

## Provide learner guidance

Moderate the brainstorming session.

Guide students towards the concept of a primary key.

## Eliciting performance / Giving Feedback (We do)

Follow up with class about their efforts / how things went.

## Assessing performance

__Story 1:__

```gherkin
Given I have file with some todos already saved
When I select one todo to delete
Then that todo is removed from the file
```

__Story 2:__
*stretch*

```gherkin
Given I have some todo items
When I delete a todo item
Then the remaining todo items are in the proper order
And the CSV file does not have an extra line
```

## Enhance retention and transfer - apply learning to real life

N/A
