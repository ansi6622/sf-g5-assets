# Databases with Sequel (Knowledge/Understanding)

## Goal
[deliverable](deliverable)

Students should understand database basics.

## Objectives

Concrete objectives that are phrased according to [verbs that relate to the Bloom's level](blooms-taxonomy.md) above:

* students can define what a database is.
* students can define a schema.
* students can recognize that a database has tables, those tables have columns
and those columns have types.
* students can list the main datatypes supported by a database.

## Prerequisites

Students have an understanding of files and persistence.

## Materials

* gdoc spreadsheet with 'sheets' for tables.
* diagram of a database with tables, columns and rows.

## Gain Attention

Remember when we had you delete todos from a CSV file? Remember how that sucked?
Databases take a lot of that pain away from you.
They also are good for:
* concurrent access
* enforcing data constraints
* not dealing with the minutia of keeping data in a efficient format

## Inform learner of objective

Databases are ubiquitous in web applications, so we want to introduce them to you.

## Stimulate recall of prior information

Databases are kind of like an excel document - each sheet is a table,
and each table has rows and columns.

Think about old spy organizations from the 60's - they collect all kinds of data
about their citizens and then put them in paper documents and folders.
Those are all kept in a room called the archives. Databases are like archives.
They are where the data goes. When you want to know something about someone,
you send a request for the documents to the archives and then some clerk finds
them for you and sends the documents to your office.

## Present the stimulus (I do)

```ruby
require 'sequel'

DB = Sequel.connect("sqlite://citizens.db")

DB.create_table :citizens do
  primary_key :id
  String :name
  Boolean :is_radical
end

citizens = DB[:citizens] # Create a dataset

# Populate the table
citizens.insert(:name => 'Martha Berner', :is_radical => false)
citizens.insert(:name => 'John Foley', :is_radical => true)
citizens.insert(:name => 'Kane Baccigalupi', :is_radical => false)

# Print out the number of records
puts "Citizen count: #{citizens.count}"

# Print out the number of shifty characters
puts "Their are: #{citizens.where(:is_radical => true).count} shifty characters"

# Print out the number of upstanding citizens
puts "Their are: #{citizens.where(:is_radical => false).count} upstanding citizens"

# Martha has fallen victim to John's propoganda...
citizens.where(:name => "Martha Berner").update(:is_radical => true)

# Print out the number of shifty characters
puts "Their are: #{citizens.where(:is_radical => true).count} shifty characters"

# Print out the number of upstanding citizens
puts "Their are: #{citizens.where(:is_radical => false).count} upstanding citizens"

# oh dear! The cops showed up and 'disappeared' John
citizens.where(:name => "John Foley").delete

# Print out the number of shifty characters
puts "Their are: #{citizens.where(:is_radical => true).count} shifty characters"

# Print out the number of upstanding citizens
puts "Their are: #{citizens.where(:is_radical => false).count} upstanding citizens"
```

## Provide learner guidance

ALWAYS use a primary key. ALWAYS call it id.
Sequel is what we are using for now, but when we get to rails, we will use
something else that is similar. Don't get attached.
Think about the data that you are storing for your domain and how that gets
modeled with tables.

## Eliciting performance / Giving Feedback (We do)

Do the exercise above except with Movies (or something). Guide students through
creating the table with the proper schema. Think of some interesting (but simple)
queries to do.

## Assessing performance

Have students refactor away from CSV files in their todo and use sequel instead.

## Enhance retention and transfer - apply learning to real life

* go read the sequel documentation and see if you can figure out how to use
another table.
