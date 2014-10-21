
# Deleting from files

## Goal

Delete things from files.

## Objectives

* Demonstrate the tediousness of traversing file content when not using a database
  or library.
* Students can write a ruby script that deletes an item from a file.
* Students understand the importance of an id field.

## Prerequisites

* Persistence lesson

## Materials

* preloaded CSV file for students

## Test yourself

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
