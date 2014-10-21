---
blooms: knowledge
published:
---

[deliverable](deliverable)

# HTTP (Knowledge/Comprehension)

## Goal
Students work with HTTP verbs in association with CRUD operations

## Objectives
* Introduce HTTP verbs: GET, POST, PUT, DELETE
* Be able to associated HTTP verbs with CRUD actions
* Introduce REST as the conventions for making this map with paths

## Prerequisites
* Rails tutorial (with CRUD)
* Completed Todo CLI app

## Materials
* github repo:

## Gain Attention
Now that we have gotten a chance to work deeply with Ruby on our Todo CLI app,
we want to go back to the web. Only instead of jumping strait into Rails, we
are going to start with a much more basic web server.

## Inform learner of objective
* Know main four HTTP verbs: GET, POST, PUT, DELETE
* Be able to associate HTTP verbs with CRUD actions
* Experiment with connecting HTTP verbs to CRUD actions in a simple rack server
* Understand REST is the translation of CRUD actions to paths + HTTP verbs

## Stimulate recall of prior information
Remember when we used Rails to build our Todo tutorial.
We talked about CRUD operations. Let's use projects as an example:

* index: list projects
* new: show form for creating a new project
* create: create a new project
* edit: show a form to edit a project
* update: update an existing project
* destroy: delete a project

## Present the stimulus (I do)

It turns out that Rails is using a convention called REST to convert paths, with
the right HTTP verb into CRUD actions. This is a powerful convention that goes
beyond Rails.

### HTTP Verbs
HTTP has two categories of verbs:
* idempotent - data is guaranteed not to change, a read only operation
* destructive -  data can change in some way

Idempotent: GET

Destructive: POST, PUT, PATCH, DELETE (describe each)

## Provide learner guidance

What rules should they follow?  Any mnemonics or learning guides?
How should they approach the topic?

## We do

Rest is a combination of the right verbs and the right paths

Go through each of the CRUD methods and have class work out
* which are GET requests
* which are about a singular thing
* extrapolate paths

## Assessing performance
* Write the paths and verbs for a todo app with:
  * projects
  * tasks
* Write the paths and verbs for an app with:
  * articles
  * comments
  * authors
