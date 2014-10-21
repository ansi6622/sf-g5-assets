# Persistent Storage

## Goal

Understanding files.

## Objectives

* students can define a file.
  * files are durable.
  * files are available to be used by programs to store data.
* students should be able to recall the methods in Ruby for opening, reading,
writing and closing a file.
* students should understand that files are analogous to:
  * a cassette tape
  * a record (like vinyl)
  * an array/collection of bytes
* students understand that files (in a filesystem) are analogous to paper documents
and directories are similar to folders.

## Prerequisites

* Ruby basics - Arrays/Collections

## Materials

![](http://static.searchengineguide.com/images/directory-ideal.jpg)

## The Problem

Our todo app loses all of our todo's when we quit. How can we store these
between runs of our program? How can we store these between reboots?

Who knows what casette/VCR tapes are?
What about vinyl records?
What about filing cabinets and documents?

### Files in Ruby
Opening a file:

```ruby
my_file = File.open("todo.txt")
```

And remember to close it!

```ruby
my_file.close
```

Opening a file (block version):

```ruby
File.open("todo.txt") do |f|
  # we can do stuff with our file here!
end

# and our file is automatically closed at this point
```

Reading from a file:

```ruby
File.open("todo.txt") do |f|
  data = f.read
  puts data
end
```

Writing to a file:

```ruby
File.open("todo.txt", "w") do |f|
  f.write("hello! I'm a todo app!")
end
```

Writing a CSV file:

```ruby
File.open("todo.csv", "w") do |f|
  f.write("completed,task\n")
  f.write("false,take out the trash\n")
  f.write("false,do laundry\n")
  f.write("true,buy groceries\n")
end
```

### Directories, the filesystem and paths

```bash
mkdir fruits
touch fruits/apple.txt
touch fruits/banana.txt
touch fruits/orange.txt
```

```ruby
File.open('fruits/apple.txt', 'w') do |f|
  f.write("I'm an apple!")
end

File.open('fruits/banana.txt', 'w') do |f|
  f.write("I'm an banana!")
end

File.open('fruits/orange.txt', 'w') do |f|
  f.write("I'm an orange!")
end
```

### Writing a simple web page

```ruby
File.open("hello_world.html", "w") do |f|
  f.write("<!DOCTYPE html>\n")
  f.write("<body>\n")
  f.write("<h1>Hello world</h1>\n")
  f.write("</body>\n")
  f.write("</html>\n")
end
```

## Helpful hints

Always remember to close your files after opening them.
To that end, you should always use the block version of open.

## Test yourself

Create a ruby script that writes the names, ages and gender of these dogs in to
a file in CSV format:

* Tank - 2 years - Male
* Fido - 5 years - Male
* Trixie - 1 year - Female

Have a member of the instruction team check your work.

## Implement persistence into the todo app.

__Story 1:__

```gherkin
Given I enter a todo item
And I quit the todo app
And I re-run the todo app
When I list the todo items
Then I see my todo item
```

Extra credit:

* Go read about [JSON](http://en.wikipedia.org/wiki/JSON) and figure out how
you might use this format instead of CSV.
