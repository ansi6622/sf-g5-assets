# Command line interfaces

## Goal: Learn to get user input and print to the screen.

## Objectives
* Learn about command line programs
* Deeper usage of `puts` and `gets`
* Introduce streams/IO

## Remember when we made that Rails todo list application? Let's do that again, but this time a lot simpler!

The first time around, you did a bunch of stuff without really knowing how it all worked.
We want you to really understand what's going on, so lets build the same thing, except this time,
there won't be a web interface, no database, no models, no migrations,
views, controllers, etc.

Just Ruby, in your terminal

### Command Line Programs

First, we need to understand what command line programs are.

Unlike a web application which you interact with in a web browser,
command line applications interact with a user via the terminal.

Web pages can be quite fancy with colors, text, images, videos, etc. while
command line apps are much simpler - you only get text.

Because of that, we need to figure out how to interact with a command line
program. Let's start simple, with `puts`.

### Printing to the command line with `puts`

`puts` is one of the basic methods in Ruby that seems to be available anywhere and
everywhere. And it is. To get to know it better, lets experiment!

Write a simple script in ruby file. We are going to use the file name `puts-and-gets.rb`

```ruby
  puts "Enter your name: "
```
Let's run our file and see how we did.

```bash
  ruby puts-and-gets.rb
```

What happened? It looks like `puts` simply writes onto our screen whatever we tell it to.
Wow, that was simple! Let's do more.


### Getting input from users using the method `gets`

In order for people to be able to use a command line app, it needs to get user input.
It turns out we can do this by using a ruby method `gets`. Nice and intuitive.

Let's change our simple script to get your name from the command line:

```ruby
  puts "Enter your name: "

  name = gets

  puts "Hello #{name}"
```

What do you think is going to happen? Let's run our file and find out. It looks like now, the
program puts out whatever input the user gave us. And that's exactly what we told it to do.

### Diving a bit deeper: streams of information

Prerequisites to the course included many exercises with `puts` and `gets`. What else can
you learn about them in class.

Probably the way you are thinking about these methods is that they print stuff, and magically
get stuff. The computer and Ruby think about these things very differently. They think about
this in terms of streams of information called IO.

In this case we are writing messages to a stream known as standard output, or stdout for short.
We are pulling information in from an input stream known as standard input, or stdin for short.

The thing that makes these streams of information different from a simple string is that
there is a position in the stream, known as a cursor. The cursor is your current position in the
stream.

Files are another type of IO, and we can rewind a file to put the cursor at the beginning of the file.

In the next couple of days we are going to get into files, and you will have to know a little more
about how these streams behave. For right now, this is just a scary intro.

## Exercises
1. Write a program that asks your name, and then prints out a greeting.

```bash
What is your name?
> John
Hi John!
```

2. Write a program that asks what your favorite color is. When you type your
favorite color the program tells you 'that's my favorite color too!''.

```bash
What is your favorite color?
> Red
Thats my favorite color too!
```

3. Write a program that asks what your favorite color is. When you type your
favorite color the program says "<whatever the color> is my fovorite!"

```bash
What is your favorite color?
> Green
Green is my favorite!
```

## Solo Exercise

1. Write a program that asks your name, and then prints out a greeting.

```bash
What is your name?
> John
Hi John!
```

2. Write a program that asks what your favorite color is. When you type your
favorite color the program tells you 'that's my favorite color too!''.

```bash
What is your favorite color?
> Red
Thats my favorite color too!
```

3. [Command Line Todo app](https://github.com/gschool-g5/todo-cli)
This link is to a repository that we will use for the next several lessons. For
this lesson only worry about the first describe block that prints out instructions. In
the next lesson, we will go over making a loop to get input from the user.
