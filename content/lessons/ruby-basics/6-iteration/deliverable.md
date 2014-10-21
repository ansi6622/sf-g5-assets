---
title: Iteration
blooms: understanding
---

# Goal: Get comfortable with collection iterations

## Objectives
* Use `each` on collections
* Know which Ruby objects are enumerable
* Use other collection iteration methods
* Recognize other less used types of language level iterations

## Prerequisites
* Reading and exercises in [Learn to Code](https://pine.fm/LearnToProgram/)
* Ruby Basics lesson on [Collections](/lessons/ruby-basics/5-collections)

-------

## Collections get much more useful when we can loop through each item

Remember in the last lesson we had collections, but we really only adding
and removing things from them. A more typical workflow has us going through
each one and doing something with each one.

Back in our Rails to-do app, we had Rails go through each project on the projects
page and print out its name and links. Then when looking at a project details,
we iterated through each task in the project and rendered some information per
task.

Humans are't really good at repetitive tasks. But computers are! Lets learn
how to get them to do things over and over for us.

### each-ing

Iterating at its heart is going over _each_ item, so it make a lot of sense that
`each` is an important method for doing this in Ruby.

Let's look at a simple case:

```ruby
  (1..100).each {|num| puts num }
```

Do you recognize the thing we are iterating over? It is a Range in this case.

Let's take apart this code. We have a range inside parens followed by a method
call `each`. We add the parens so that each is called on the range, and not
the number `100`.

Next we have a block. We saw blocks in the last lesson, but we didn't talk about them.
It's time to dig deeper; blocks are important.

### Blocks
Blocks are tiny procedures that we can run later. Blocks can take arguments, and those
blocks will show up in pipes `|num|`. In the example above there was only one argument.
This is what a block looks like with two arguments:

```ruby
  {hello: 'world'}.each {|key, value| puts "#{key}, #{value}"}
```

Similar to arguments in a method, block arguments are separated by commas. Also, an
interesting thing to note, is that Hashes allow `each` iteration, and pass in
the key and the value as arguments to the block.

That gets to a really interesting point, these blocks need to conform to what the method
`each` will give to them. When we work with other methods that use blocks, the blocks
have to work closely with the methods.

#### Alternative Block Syntax
Ruby is flexible and has many different syntaxes for creating blocks. Let's look
at a few more so you recognize them, and can use them:

```ruby
  ["fish", "gerbil", "dog"].each do |animal_name|
    puts "#{animal_name} is cute!"
  end
```

In this case we are iterating over an Array. The different block syntax uses `do`
and `end` to mark the ends of the block instead of curly braces, `{` and `}`.

#### Convention around block syntax usage
Ruby has some informal conventions around when to use `do end` blocks, and when to use `{ }` blocks.

The most common convention is that multi-line blocks use `do end`, where as blocks that
fit easily in a single line use curly braces `{ }`.

You can research other conventions, but this is the one we will be using going forward.

### Enumerables
In the above examples, we called `each` on three different objects: Range, Hash and Array.
It turns out  that each of these are considered 'Enumerables' in Ruby, and they share
code that is well documented: [Enumerable Docs](http://ruby-doc.org/core-2.1.3/Enumerable.html).

It turns out that any object in Ruby that implements an `each` method can drop
in Enumerable and get all these other methods for free. Let's play with a few of these:

```ruby
  hash = {one: 1, two: 2}
  array = ["fish", "gerbil", "dog"]
  range = (1..1_000)

  hash.first
  # => [:one, 1]

  array.first
  # => "fish"

  range.first
  # => 1

  hash.max
  # => [:two, 2]

  array.max
  # => "gerbil"

  range.max
  # => 1000
```

It looks like Hashes act pretty different as enumerables than Arrays and Ranges, because
they have a key and a value. When we use them as enumerables, that array including the key
and value will show up. In the case of our `each` call with hashes, we used a block with
two arguments. If we had used a block with only one, we would have seen this same kind of
an array containing the key and value.

### Mutating collections
In previous sections we talked about 'mutating' objects. Sometimes we want not
just to iterate over a collection, but also *permanently change the original object*.
We are going to dig deeper into what mutation really means, while building towards
some handy collection methods.

Lets say we
have an array of names and we want to make all of them uppercase. Lets try it
with each:

```ruby
  names = ["Kane", "John", "Bru", "Lauren", "Martha", "Kat"]
  names.each {|name| name.uppercase }

  puts names # => ["Kane", "John", "Bru", "Lauren", "Martha", "Kat"]
```

Wait a minute, it didn't work! Why not? The reason is somewhat subtle. When we
call each, Ruby is actually making a copy of each item when it is passed in to
the block, so the thing that is being uppercased is actually the copy. At the
end of the block the copy is just thrown away, so our change never makes it back
to the original array.

So what can we do? What if we just build another array with the changes that we
want? That looks something like this:

```ruby
  names = ["Kane", "John", "Bru", "Lauren", "Martha", "Kat"]
  uppercased_names = []

  names.each {|name| uppercased_names << name.upcase }
  puts uppercased_names # => ["KANE", "JOHN", "BRU", "LAUREN", "MARTHA", "KAT"]
```

Yay it worked! But its a little ugly still- we have to create an empty array
and then push things on to it ourselves. Its not the worst, but Ruby has a
shortcut for doing this for us. We can use the `map` method.

```ruby
  names = ["Kane", "John", "Bru", "Lauren", "Martha", "Kat"]
  uppercased_names = names.map {|name| name.upcase }
  puts uppercased_names # => ["KANE", "JOHN", "BRU", "LAUREN", "MARTHA", "KAT"]
```

Just like the each method, map will call our block for each item in the array.
The crucial difference is that each will throw away the return value of the
block, but map will use that return value to create a new array.

It turns out that you can do it with even less code with another method called `map!`.

```ruby
  names = ["Kane", "John", "Bru", "Lauren", "Martha", "Kat"]
  names.map! {|name| name.upcase }
  puts names
  # => ["KANE", "JOHN", "BRU", "LAUREN", "MARTHA", "KAT"]
```

Notice the '!' at the end of the method. This is a convention in Ruby. When something
will change the original value, or is in some other way destructive, we will see it
ends in an exclamation mark. We will even do that for methods that we write ourselves.

There are many other things that you can do with collections, so this is just
the start. All of these methods are in a Ruby module called Enumerable, so go
take a look at the documentation and see what else you can do with collections.

### Language iterators

Most languages, Ruby included, come with a variety of ways to iterate independent of
collections. In Ruby it is pretty rare to actually use these language constructs, but
let's look at them so you are familiar

#### While

```ruby
  while true
    puts "hello!"
  end
```

This will loop forever, not a typical need! Let's fix that with some logic to
change the conditions for the while loop:

```ruby
  keep_running = true
  while keep_running
    puts "hello!"
    puts "keep going?"
    input = gets.chomp

    if input == "no"
      puts "ok..."
      keep_running = false
    end
  end
```

### Until
Ruby has another loop that is a mirror image of a while loop- it will keep
looping until some condition is met. It's called an until loop.
Lets rewrite our greeter program using an until loop:

```ruby
  done = false
  until done
    puts "hello!"
    puts "keep going?"
    input = gets.chomp

    if input == "no"
      puts "ok..."
      done = false
    end
  end
```

#### Loop
The last looping construct that we should talk about is just...a loop. You give
it a block and it loops forever. You can break out of the loop with the `break`
keyword.
Our greeter again:

```ruby
  loop do
    puts "hello!"
    puts "keep going?"
    input = gets.chomp

    if input == "no"
      puts "ok..."
      break
    end
  end
```

#### For
Another type of loop in Ruby is called a for loop. It actually looks pretty
close to the first loop above:

```ruby
  for num in (1..10_000_000) do
    puts num
  end
```

There is _no_ good reason to use this instead of `each` on a Range. No one does
this in Ruby.

--------

## Group Activity
* [Array exercises](https://github.com/gSchool/array-exercises)

## Solo Exercises
* Finish the array exercises above.
* Write code that prints out all of the multiples of 17 between 1 and 10 million.

## Group Activity
* [Hash exercises](https://github.com/gSchool/hash-exercises)

# Solo Exercises
* Finish the hash exercises above.
* [Hash/Array Collection Exercises](http://github.com/gSchool/collection-exercises)

--------

## Assessment
```gherkin
  Given an array of hashes of student names (built in the array assement)
  When I run my ruby file
  Then I should see a headline printed: "All"
  And I should see printed list of students in this format "{{last name}}, {{first_name}}: {{email}}"
  And I should see a headline printed: "Some"
  And I should see the same formatting for the students that have a 't' upper or lower case in their last names
```

## Resources
* [Array Docs](http://www.ruby-doc.org/core-2.1.2/Array.html)
* [Enumerable](http://www.ruby-doc.org/core-2.1.2/Enumerable.html)
* [Loops and Arrays](http://ruby.learncodethehardway.org/book/ex32.html)
* [Treehouse Arrays](http://blog.teamtreehouse.com/ruby-arrays)

<!-- ## Extra Credit -->
<!-- * [Reducing and detecting](https://github.com/gSchool/reducing_and_detecting_arrays) -->
<!-- * [Filtering and transforming](https://github.com/gSchool/filtering_and_transforming_arrays) -->
<!-- * [Milestone Assessment Week 4](https://github.com/gSchool/denver-assessment-week-4) // text collection -->
<!-- * [Hamming Exercism](https://github.com/gSchool/hamming) // text collection -->
