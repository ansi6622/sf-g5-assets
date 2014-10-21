---
blooms: application
---

# Http-2

## Goal

Students can write a rack server

## Objectives

  * Students can make connection between (input -> function -> output) and
    (request -> rack function -> response)
  * Students can write a router in the jank
  * Students understand URL structure
  * Students understand that a rack application always boils down to a function
    that takes input as a hash and returns an array of three elements.

## Prerequisites

HTTP-1 Basic HTTP

## Materials

How the Internet Works diagram

## Gain Attention

We are web developers! We must understand how the web works on a fundamental
level. Also, Rails has a lot of bells and whistles and does a lot for us. We
want to strip that down so we can truly appreciate what rails gives us.

## Inform learner of objective

See objectives

## Stimulate recall of prior information

Functions take what and return what? (input, output)
All Http transactions are made of what? (request, response)

## Present the stimulus (I do)

```bash
gem install rack
atom server.rb
```

```ruby
require 'rack'

app = Proc.new do |env|
  ['200', {'Content-Type' => 'text/html'}, ['A barebones rack app.']]
end
```
## Provide learner guidance

All rack apps have a function. In our case, think of this new Proc as a function.
This function takes one argument - traditionally called env. We'll look at that
later.

### Our function returns an array of three elements:

  * Http status code
  * Hash of http headers
  * body of the response

## Have students write different paths in the url (i.e. http://localhost:8080/bananas)

  * This is to demonstrate to students that nothing happens because we have not
    yet given our server instructions to do anything with these requests.
  * Show 'puts env' and demonstrate how the URI changes

## Recall our CLI and liken routes to using a case statement to tell the server
## how to respond to different client behavior

  * when /hello do this
  * when /bananas do this

## Eliciting performance / Giving Feedback (We do)

As a class, write a case statement to hand different server requests.

## Assessing performance

* Students can write a server that returns 'Hello world' literal
* Students can return 'Hello world' HTML (<html></html)
* Students can write a server that says 'Hello' with GET /hello and
  "Goodbye" with GET /goodbye

## Enhance retention and transfer - apply learning to real life

?
