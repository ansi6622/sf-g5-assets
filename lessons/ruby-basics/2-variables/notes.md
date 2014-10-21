---
blooms: knowledge
---

# Variables


## Goal

Students understand local and instance variables

## Objectives
* Conceptualize assignment of an object into a variable
* Understand legal and idiomatic variable names
* Comprehend that variables act like the object they hold
* Understand that variables are reusable with any other type of object
* Introduce best practices for variable usage and naming
* Introduce instance level variables

## Prerequisites
* Reading and exercises in [Learn to Program](https://pine.fm/LearnToProgram/)

## Gain Attention

How do you store things in Ruby?
What are the different types of storage that exist?

## Inform learner of objective

We are going to cover local variables and instance variables.
There are others that will come up, but for now, we are focusing on these.

## Stimulate recall of prior information

Who can explain what a variable is?
Does anyone know the different types of variables?

## Present the stimulus (I do)

### Assigning to Variables

```ruby
  people_currently_in_class = 27
  # => 27

  people_currently_in_class
  # => 27

  # uh, oh! Flu outbreak

  people_currently_in_class = 18 # :(
```

### Legal variable names

```ruby
  12foo = 12
  #  SyntaxError: (irb):2: syntax error, unexpected tIDENTIFIER, expecting end-of-input
  #  12foo = 12
  #       ^
```

### Variables Act Like the Thing They Hold

```ruby
  number_of_students = 26
  # => 26
  number_of_students.to_s
  # => '26'
  sick_students = 5
  # => 5

  students_in_class = number_of_students - sick_students
  # => 21

  ratio_present = students_in_class.to_f / number_of_students
  # => 0.8076923076923077
```

### Variables Are Flexible

```ruby
  students = 26
  # => 26

  students = true
  # => true

  students - sick_students
  # => NoMethodError: undefined method '-' for true:TrueClass
  #      from (irb):2
  #      from /Users/baccigalupi/.rvm/rubies/ruby-2.0.0-p481/bin/irb:12:in '<main>'
```

### Instance Variables

```ruby
  @number_of_students = 26
  # => 26
  @sick_students = 5
  # => 5

  @students_in_class = @number_of_students - @sick_students
  # => 21

  @ratio_present = @students_in_class.to_f / @number_of_students
  # => 0.8076923076923077
```

## Provide learner guidance

Naming is hard. That being said, pick good variable names.
You will spend more time reading code than writing it, so be nice to the people
that come after you (and future you!) and pick good names.
Variables have a lifetime in your code. Keep that lifetime as short as you
possibly can.

## Eliciting performance / Giving Feedback (We do)

Come up with scenarios for variables and practice good naming.
Throw out variable names ('foo') thumbs up or thumbs down?
Guess what's in my variable based on its name?
