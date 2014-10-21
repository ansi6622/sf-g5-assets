# Goal: Apply what you learned so far about rails by building a contacts app

## Objectives:
* User `rails new` to create an empty app
* Build basic CRUD with scaffold

-------

## Let's apply what we learned about tasks, to people

We learned a lot in a short period of time about CRUD, scaffolding,
controllers, models, styling, Gemfiles ... Oh, so much!

Now we want you to try it on your own.

## Build a Contacts App for holding all your people
Having trouble remembering this stuff? When developers
get stuck, the first thing they do is look on google, really!
We want to build that practice in here too. So, get stuck,
look for answers on the internet. Then ask for help.

1. Build a new rails app with `rails new`. Don't bother to add any gems this time.
2. Use Rails scaffold to build a Contact. The Contact should have these attributes:
    * first name
    * last name
    * phone number
    * email

That's it. When you are done. Grab your friendly TA, and get it confirmed.

#### Extra Credit
Some of you are going to finish faster and be eager to try more stuff.

* Help your neighbor! It turns out that talking through what you know by teaching
enforces what you know and sets it in stone it your brain. It is also much more
challenging than coding.
* What other fields could you add to a user?
* Can you make a method on the model for full name? What about a method that puts
last name first with a comma between the name parts?
* In the contacts show view, try to figure out how to make the email into something
that you can click, that opens in your mail editor. This will involve looking up in
Google-land how HTML handles a special `<a>` tag that links to emails.
