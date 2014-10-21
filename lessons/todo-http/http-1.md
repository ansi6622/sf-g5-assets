# HTTP (Knowledge/Comprehension)

## Goal

Students get a basic idea of how a webpage is rendered in a browser

## Objectives

* students understand the lifecycle of an HTTP request/response cycle
* students can list the main HTTP verbs
  * GET
  * PUT
  * DELETE
  * POST
  * PATCH
* students can list some of the main status codes
  * 200 OK
  * 404 Not found
  * 403 Forbidden
  * 500 Generic server error
  * 302 redirect
* students understand that a HTTP response is comprised of:
 * status line 
 * header
 * body

stretch objectives:
* students know how DNS fits in to the picture
* students understand that only GET and POST are 'real'

## Prerequisites

N/A

## Materials

* notecards for documents (as described in stimulus section)
* [status cats](https://www.flickr.com/photos/girliemac/sets/72157628409467125)
* sequence diagram for HTTP
* slides that:
  * give an overview of HTTP verbs
  * give an overview of HTTP status codes
  * show the basic structure of a request and response

## Gain Attention

How does a web page get rendered in a browser?
What is actually happening behind the scenes?
As web programmers, we need to be intimately familiar with how this works.

## Inform learner of objective

Although a little abstract, the underpinnings of HTTP are important for web programmers

## Stimulate recall of prior information

Get a volunteer from class to draw on white board - mob effort to draw an HTTP request and response.

## Present the stimulus (I do)

Have a few volunteers come to the front of the class.
The instructor tells each student that they are either:
* the client
* the server

The instructor then hands the 'server' a couple of notecards labeled '/', '/blog', '/blog/new', and '/blog/1'.
Next, the instructor has the 'client' ask the 'server' to GET '/'- the server then reads the back of the notecard to the
class. (something like an about page)

The instructor then gives EXPLICIT instructions of who does what during an HTTP request/response:
* The client requests the server to GET '/blog'. The server reads back the headlines of some blog posts.

* The client requests the server to POST a new blog post to '/blog/new' - they hand the server a notecard with the content
of a blog post on it. (Call out that this is form submission) The server then writes on the back of the notecard the new
post's URL.

* The client requests the server PUT an updated blog post at '/blog/1'. They give the server a fresh notecard with the 
updated content and the server throws away the old one.

* The client requests the server to DELETE '/blog/1'. The server throws away the notecard.

## Provide learner guidance

What rules should they follow?  Any mnemonics or learning guides?
How should they approach the topic?

## Eliciting performance / Giving Feedback (We do)

Have different set of volunteers to play act as clients/servers but the instructor does not give
instructions on who does what, only provides the prompt of a request and response.

## Assessing performance

??

## Enhance retention and transfer - apply learning to real life

??
