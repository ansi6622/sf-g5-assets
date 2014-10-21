---
title: Rails - Assessment, Part 2
blooms: assess
---

# Goal: Add to the Contacts app, relationships and another layer of CRUD

## Objectives:
* Do more scaffolding
* Build associations

-------

## Now that we have people, we want to associate them with companies

Remember the last assessment we did? We created a Rails app that held
 contact info. Now we want to store more information about people.

We want to know what companies they are part of, and instead of making
that company just a name, we want it to be real data. Why? Because then
we can show a company, and list all the employees.

## Add companies to your Rails contacts app
0. Make the contacts index/list the home page. Do this in the routes.rb file.
1. Use rails scaffolding again to create companies. We should only need a
name for these companies.
2. Create a migration to add 'company_id' to contacts.
3. Make a relationship from Company to Contact.
4. Make a relationship from Contact to Company.
5. Change the Contact form to have a select drop down for companies.
5. In the Company 'show' view, list all the employees.

That's it. When you are done. Grab your friendly TA, and get it confirmed.

#### Extra credit
* Help your neighbor. Teaching makes you learn better, faster.
* It turns out people have many emails and many phone numbers ... not just one.
How many columns would we have to add to the contacts to make it practical? What
are the implications of having to add a column to the database every time someone
exceeds your limit? How much down time will the app have for these deploys? How
frustrated will your users be, waiting for a deploy to add another email to the system?
* Read this article: [Design pattern: repeated attributes (the phone book)](http://www.tomjewett.com/dbdesign/dbdesign.php?page=phone.php)
* How would this work in our Rails app? Add those models to make this work everywhere!
