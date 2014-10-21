# Databases with Sequel

## Goal

Understanding database basics.

## Objectives

* students can define what a database is.
* students can define a schema.
* students can recognize that a database has tables, those tables have columns
and those columns have types.
* students can list the main datatypes supported by a database.

## Prerequisites

Having an understanding of files and persistence.

## Materials

* gdoc spreadsheet with 'sheets' for tables.
* diagram of a database with tables, columns and rows.

## Remember when we had you delete todos from a CSV file? Remember how that sucked?
Databases take a lot of that pain away from you.
They also are good for:
* concurrent access
* enforcing data constraints
* not dealing with the minutia of keeping data in a efficient format

## Databases are ubiquitous in web applications

Databases are kind of like an excel document - each sheet is a table,
and each table has rows and columns.

Think about old spy organizations from the 60's - they collect all kinds of data
about their citizens and then put them in paper documents and folders.
Those are all kept in a room called the archives. Databases are like archives.
They are where the data goes. When you want to know something about someone,
you send a request for the documents to the archives and then some clerk finds
them for you and sends the documents to your office.

## A simple Sequel program

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

## Helpful hints

S-Q-L is often pronounced like 'sequel'. This is a library on top of S-Q-L
pronounced 'sequel'. They are related, but NOT the same thing.

ALWAYS use a primary key. ALWAYS call it id.

Sequel is what we are using for now, but when we get to rails, we will use
something else that is similar. Don't get attached.

Think about the data that you are storing for your domain and how that gets
modeled with tables.

## Do the exercise above except with Movies (or some other interesting domain).

## Test yourself

Refactor away from CSV files in your todo app and use sequel instead.

## Further reading

* go read the [sequel documentation](https://github.com/jeremyevans/sequel/)
and see if you can figure out how to use another table.
