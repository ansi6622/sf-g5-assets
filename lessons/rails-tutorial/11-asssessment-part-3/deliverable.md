---
title: Rails - Assessment, Part 2
blooms: assess
---

# Goal: Pretty up your App with Bootstrap

## Objectives:
* Add a gem to your project
* Use bootstrap to pretty up your app

-------

## Well it works, but it's kind of ugly!

Remember the last assessment we did. The CRUD was all in place; there
are relationships between our two models. We even are displaying the
employees in a list when we look at the project. But it's ugly, and
we learned about Bootstrap which we can use to quickly pretty it up.

## Bootstrap your app
1. Change your Gemfile to include the right gem, and bundle.
2. Do all those magic commands with rails generate to
    * install static content from the gem
    * generate a new application layout
3. Fix the generated layout to:
    * Top nav should only have that one link to the home page
    * Change the sidebar content to link to our two resources: Contacts and Companies.
4. Pretty up each of the indexes to have nice list styles.
5. Also, make the indexes have links 'edit' and 'delete' that look like buttons
6. Also, also, make the name of the resource a link to the 'show' view

That's it. When you are done. Grab your friendly TA, and get it confirmed.

#### Extra Credit

What other things can you do to pretty up the app? Check out the Bootstrap CSS
pages on the internet. Add some color, icons, whatever. Also is there a better
UI flow? How could you dot that?

Also, go teach your neighbor. It really helps.
