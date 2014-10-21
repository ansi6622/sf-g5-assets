---
title: Everything Else
blooms: understanding
---

# Goal: Recognize the other Ruby objects in common play

## Objectives:
* Learn about `nil`
* Revisit symbols
* Recognize regexes and their uses
* Time and Date

## Prerequisites
* Reading and exercises in [Learn to Code](https://pine.fm/LearnToProgram/)

-----

## There are a wealth of objects ready to use in Ruby

In this section we are going to look at the most basic ones that you should be
familiar with before we start crafting our own objects and procedures.

### `nil`

There is a concept in most programming languages of nothingness. It is not the same
thing as 0, which is a number, or false which is a boolean. In Ruby that concept
is available an `nil`. Like everything else in Ruby, nil is an object.

In order to see what it can do, we can introspect with `nil.methods`. That prints
out a whole bunch of methods, but we can understand more about what make nil different
from other objects with this command:

```ruby
  nil.methods - Object.methods
  # => [:to_i, :to_f, :to_a, :to_h, :&, :|, :^, :to_r, :rationalize, :to_c]
```

As you can see there are only a few things you can do with it, and many of those
are about converting it to other types of objects.

Still, nil is a really important object in Ruby that just keeps showing up.

### Symbols

As mentioned in the lesson on [hashes](/lessons/ruby-basics/5-collections), symbols
in many ways look like strings, but are not the same as their string counterparts.

They are most commonly used as keys in hashes and method names. See above
Ruby output for an array of methods names, all of which are symbols.

The reason that they exist in the world is because they convert to integers under
the Ruby covers. Comparing integers is math, which computers do very quickly and well.
Comparing string is actually pretty computationally expensive, so it is slow.

### Regexes

Comparing strings is computationally expensive, but when comparing strings a character
by character match is often more an ideal than a reality. Usually what we want is a
fuzzy match. For example, what if we wanted to check that an email, coming in through
a form was a real email, as opposed to a gibberish. There is a pattern that emails
have:
  * They start with a bunch of characters with no spaces. There can be a variety
    of letters in there, but not an '@' sign. Mostly we see a-z, 0-9, and maybe periods '.'
  * Next they have that '@' sign
  * After that there is a domain name which has similar requirements to the first part of
    our email matcher, except that it definitely includes at least one '.'

We can build out that kind of pattern in a regex.

Regexes look like this: `/foo/`. They are bounded by slashes. Except that sometimes
they end in modifiers like this `/foo/i`.

A not very good regex for emails could look like this:

```ruby
  /[a-z0-9.]+@[a-z0-9.]+/i
```

This regex will have a starting section with a-z, 0-9, '.'. That is what we see
inside that first section with square brackets. The plus sign after those square
brackets indicates that we must have at least one character of that type. The '@'
is just a plain text match. We are demanding that this character be there between
those two sections. And the last section of square brackets is the same as the first
section. The ending modifier 'i' indicates that it is case-insensitive. So really
each of those sections matches capital letters too. If we didn't want that everywhere
we could change our bracketed section to look like this: `[a-zA-Z0-9]`.

There are whole books written on regexes!

There is too much to learn, and it will come to you with time. The good news is
that regexes look and act similar across actions.

Let's look at how we use regexes in Ruby:

```ruby
  "hello@gmail.com".match(/[a-z0-9.]+@[a-z0-9.]+/i)
  # => #<MatchData "hello@gmail.com">

  "hello+totally-legal@gmail.com".match(/[a-z0-9.]+@[a-z0-9.]+/i)
  # => #<MatchData "legal@gmail.com">

  "gerbil".match(/[a-z0-9.]+@[a-z0-9.]+/i)
  # => nil
```

In the first example, we got the match we expected, but how do we get to it?

```ruby
  match_data = "hello@gmail.com".match(/[a-z0-9.]+@[a-z0-9.]+/i)
  match_data[0]
  # => "hello@gmail.com"
  match_data[1]
  # => nil
```

Match data acts like an array, which is pretty bad when you get `nil` back.

```ruby
  match_data = "gerbil".match(/[a-z0-9.]+@[a-z0-9.]+/i)
  match_data[0]
  # NoMethodError: undefined method `[]' for nil:NilClass
	#    from (irb):10
	#    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

That's it for now.

## Group Exercises
* Let's brainstorm what we could do with those nil methods. What do they do?
* How could we make the regex work for our totally legal example email above?

## Resources
[Rubular - the Ruby web regex experimenter](http://rubular.com)
