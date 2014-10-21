---
title: Collections
blooms: understanding
---

# Goal: Understanding Collections

## Objectives
* Know the difference between arrays and hashes
* Understand common array methods and where to find documentation
* Recognize multi-dimenisional arrays
* Recognize and use ranges
* Recognize and use both methods of hash declaration
* Understand common hash methods
* Be aware of common pitfalls of using multi-dimensional arrays and nested hashes

## Prerequisites
* Reading and exercises in [Learn to Code](https://pine.fm/LearnToProgram/)
* Lesson on basic Ruby: [everything is an object](/lessons/ruby-basics/1-objects)
* Lesson on basic Ruby: [string](/lessons/ruby-basics/4-strings)

-------

## Collections are important for grouping things

Our Rails to-do app would not have been that useful if we had only been able to
work with a single task. In the world we work with groups of things: a bunch of bananas,
a team of workers, a forrest of trees.

Sometimes the order of collections is important. For example, imagine a list of students
in this class. What if we ordered that list by what date the student was accepted. If we
printed out that list of students in order, we could know at a glance whether one student
was enrolled before or after another student.

Ordered lists are know in Ruby as Arrays.

There are other types of collections though. Imagine that you wanted to organize some data about
a person. For any given person, the collection of data will include their first name, their last name,
an email and maybe a phone number. You want all this information grouped together, but you need to
easily grab the email and know that you are not getting the phone number instead.

In Ruby, the Hash collection type allow programmers to associate keys with values.
It is very similar to JSON, if you have seen that beast. Other languages call this
construct a dictionary because labels are defined by their values, or an associative array
because the value is associated with the label or key.

It is really rare to do any work in Ruby that does not involve both Arrays and Hashes. We
need to learn both very well.

### Arrays

Arrays are ordered lists, and in Ruby they are syntactically bound by square brackets: `[1, 2, 3]`.
You also use square brackets to access members by index. __Indexes start at zero.__

```ruby
  student_names = ["Jane", "Jeff", "Jan"]
  # => ["Jane", "Jeff", "Jan"]

  student_names[0]
  # => "Jane"

  student_names[2]
  # => "Jan"
```

Like strings, arrays come prepackaged with all kinds of
[magic methods](http://www.ruby-doc.org/core-2.1.2/Array.html).
All the array index magic with negative numbers that we saw with strings also work with arrays.
It turns out strings are collections too.

You can see that the method `#at` will also work for accessing elements by index:

```ruby
  student_names.at(0)
  # => "Jane"
```

It's nice that this `#at` method is here, but you don't typically see this done.
Other methods are much more useful and frequently used.

```ruby
  student_names.length
  # => 3

  student_names.count
  # => 3

  student_names.size
  # => 3
```

Ruby aliases lots of method names to get the most intuitive fit for engineers. You don't have to
know all these methods, but you need to have a sense that they exist so you can look them up.

Collections in many languages use methods for adding and removing items in different ways to
an array.

`#push` will add an element to the back of an array.
`#unshift` adds an element to the front of the array:

```ruby
  student_names.push("John")
  # => ["Jane", "Jeff", "Jan", "John"]

  student_names.unshift("Adam")
  # => ["Adam", "Jane", "Jeff", "Jan", "John"]
```

`#unshift` is a pretty weird method name. The 'un' part pairs it with another method `#shift` that takes things
off the top of the array.

```ruby
  student_names.shift
  # => "Adam"

  student_names
  # => ["Jane", "Jeff", "Jan", "John"]

  student_names.unshift("Alice")
  # => ["Alice", "Jane", "Jeff", "Jan", "John"]
```

So what is the opposite of push then? `#pop`.

```ruby
  student_names.pop
  # => "John"

  student_names
  # => ["Alice", "Jane", "Jeff", "Jan"]
```

You can also insert and remove things in the middle of an array.

```ruby
  student_names.insert(2, 'Annabelle')
  # => ["Alice", "Jane", "Jeff", "Annabelle", "Jan"]
```

You can remove objects either by index or by value. In both cases the thing
being deleted is returned.

```ruby
  student_names.delete("Annabelle")
  # => "Annabelle"
  student_names
  # => ["Alice", "Jane", "Jeff", "Jan"]

  student_names.delete_at(0)
  # => "Alice"
  student_names
  # => ["Jane", "Jeff", "Jan"]
```

We can even delete items if they meet a certain criteria:

```ruby
  student_names.delete_if {|name| name.start_with?("J") }
  # => []

  student_names
  # => []
```

We have been constructing arrays that hold just one type of thing. But Ruby allows
arrays of many different types of things:

```ruby
  ['gerbil', 3.14, Time.now]
```

Because you can store anything in an array, you can even store an array inside.
This leads to something called nested arrays or multi-dimensional arrays.

```ruby
  weird_collection = [nil, 2, [1,2,3]]

  weird_collection[2][2]
  # => 2
```

But watch out! Trying to access things that aren't there may throw an error.

```ruby
  weird_collection[0]
  # => nil

  weird_collection[0][1]
  # NoMethodError: undefined method `[]' for nil:NilClass
	#    from (irb):7
	#    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

On a software design level, when you mix types of objects in an array you have
to remember lots of details about how that data is organized. When that memory fails
or isn't transfered to other developers, bugs proliferate. If you find yourself
needing an array within an array, you probably need to build a custom object or
two instead.

### Ranges

Ranges are like arrays except a little less useful, and a little more conceptual.
They define a range of values. It is most common to see these used with numbers and times.
Here is what they look like:

```ruby
  # given a variable my_number containing, a number
  (1..5).include?(my_number)
  # => true

  (1..5).to_a
  # => [1, 2, 3, 4, 5]

  (-1..-10).to_a
  # => []

  # given variables start_time and end_time which both contain times
  (start_time..end_time).include?(Time.now)
```

You can even use variables in the scope of a the start and end points.

```ruby
  # given an x and guess that are both numbers
  (0..x).include?(guess)
  # => false
```

### Hashes

Hashes are super useful utility packs for collecting associated data.

```ruby
  {
    first_name: 'Kane',
    last_name: 'Baccigalupi',
    email: 'kane@galvanize.it'
  }
```

It turns out that these things can get very deeply nested:

```ruby
  class_info = {
    instructor: {
      first_name: 'Kane',
      last_name: 'Baccigalupi',
      email: 'kane@galvanize.it'
    }
  }
```

Getting data back out of these things looks very similar to accessing arrays by index.
We use the square brackets:

```ruby
  class_info[:instructor]
  # => {:first_name=>"Kane", :last_name=>"Baccigalupi", :email=>"kane@galvanize.it"}
```

Notice how we used `:instructor` as the key to access the data. `:instructor` is a
symbol, which in Ruby is like a string with some important differences. Symbols
don't have many methods. They work mostly as labels and names. Because they are
used as labels comparing them is much, much faster. That is their main reason for
existing.

The 'class_info' hash that we built uses the newer, JSON-style, syntax.
Let's look at what hashes looked like before Ruby 1.9. Hint, it is what we saw
returned on the command line above.

```ruby
  {
    :instructor => {
      :first_name => 'Kane',
      :last_name => 'Baccigalupi',
      :email => 'kane@galvanize.it'
    }
  }
```

There is a lot more syntax in that definition, but it churns out the same thing.
We are mapping keys that are Symbols to values on the other side of a hash-rocket `=>`.

When we used the shorter syntax with the key separated from the value by just `:`, it
was using a shorthand to make symbol keys for us.

It turns out symbols are not the same as strings; let's check:

```ruby
  "kane" == :kane
  # => false
```

Why does this matter? Well any kind of an object can be a key.

```ruby
  confusing_hash = {
    'kane' => 'no one home',
    :kane => "Baccigalupi"
  }

  key = 'kane'

  confusing_hash[key]
  # => "no one home"

  key = :kane

  confusing_hash[key]
  # => "Baccigalupi"
```

That kind of confusion between strings and symbols when accessing a hash is so
common that Rails built a class `HashWithIndifferentAccess` that takes
away this problem. We will work with that much later in the class.  

Anything can be a key in a hash. Let's look at other objects as keys:

```ruby
  weird_hash = {
    1 => 'one',
    [1,2,3] => [4,5,6]
  }

  weird_hash[1]
  # => 'one'

  weird_hash[[1,2,3]]
  # => [4, 5, 6]

  weird_hash[[1,2,3]][1]
  # => 5

  just_a_bad_idea = {
    {mind: "blown"} => "is it a key? is it a value?"
  }

  just_a_bad_idea[{mind: "blown"}]
  # => "is it a key? is it a value?"
```

While many things are possible, most are not advisable. This weird hash is pretty
confusing. Most developers would curse you to your face if you made something like
this and they had to maintain it.

There are some instances where we might want to use an object as a key. Let's imagine
that we have a collection of students and we want to access them quickly by their student
id. The collection could be a hash where the key is a number, and the value would be the student
data.

One thing to note here, in our weird hash example, is that we are accessing nested data,
similar to how we were accessing multi-dimensional arrays. We use nested square brackets:

```ruby
  class_info[:instructor][:first_name]
  # => "Kane"
```

Access goes both ways. You can set hash values with square brackets too:

```ruby
  class_info[:instructor][:pet] = "cat"
  # => "cat"
```

When we try to set stuff that isn't yet there, things go wrong:

```ruby
  class_info[:ta][:first_name] = "Martha"
  # NoMethodError: undefined method `[]=' for nil:NilClass
	#    from (irb):21
	#    from /Users/baccigalupi/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

Hashes like all other Ruby constructs come action packed with many great methods.
Documentation will give you a sense of what is possible, but you should always experiment!

## Solo Exercises
* Experiment in IRB to figure out what you can do with `+`, `*`, `-`, `&`,
and `<<` on an array. PS: `<<` is really commonly used!
* What is the difference in range operators `..` and `...`?
* Build a nested hash, 3 layers deep. When you try to read information that
you have not yet set, what happens? Is it similar to multi-dimensional arrays? How
is it different?
* Experiment with the methods `#keys` and `#values`. What do they do? How would
this be useful?

## Group Exercises
* Review solo exercises

## Assessment
In a ruby file construct an array of student data hashes.
Each student hash should contain:
* first name
* last name
* email
* class

for each student in the class.

Data:
```plain
  First Name    | Last Name     |   Email                 | Class
  ------------------------------------------------------------------------------
  John            Foley             john@gschool.it         Beginning snark
  Sylwester       Kelsey            sellie@gmail.com        Ruby Immersive
  Timothy         Rama              tim.rama@gmail.com      Ruby Immersive
  Kane            Baccigalupi       kane@gschool.it         C for dummies
  Nikita          Theodosius        nikita.theo@gmail.com   Ruby Immersive
  Roddy           Eldred            roddy.el@gmail.com      Ruby Immersive
  Martha          Berner            martha@gschool.it       Time travel for beginners
  Kofi            Thomas            k.thomas@hotmail.com    Ruby Immersive
```

You can copy and paste text values from the file,
but are not allowed to copy and paste hashes or other syntax elements.

We will use this for the next section on iteration!

## Resources
* Array Docs: [http://www.ruby-doc.org/core-2.1.3/Array.html](http://www.ruby-doc.org/core-2.1.3/Array.html)
* Hash Docs: [http://www.ruby-doc.org/core-2.1.3/Hash.html](http://www.ruby-doc.org/core-2.1.3/Hash.html)
* Range Docs: [http://www.ruby-doc.org/core-2.1.3/Range.html](http://www.ruby-doc.org/core-2.1.3/Range.html)

## Extra Credit
* Go grok why hashes are called hashes. [Hint](http://c.learncodethehardway.org/book/ex37.html)
