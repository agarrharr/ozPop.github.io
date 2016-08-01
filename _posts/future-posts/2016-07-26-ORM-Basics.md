---
layout: post
title: ORM Basics & More
---

#### Connecting to database

```ruby
database_connection = SQLite3::Database.new('db/my_database.db')
```

#### Executing statements

```ruby
database_connection.execute("Some SQL statement")
```

A convention we use when telling our program to talk to a database is:
* that classes are mapped to or equated with tables and instances of a class are equated to table rows

#### Setting Up the DB access class (FROM Dynamic ORMs Lab)

NOTE on _returning query results as Hash:_

```ruby
DB[:conn].results_as_hash = true
```

When SELECT statement is used return database row as `Hash` instead of `Array`

<p></p>

NOTE: use `pluralize` method to pluralize e.g.: class name 
    (dependency: `require 'active_support/inflector gem'`)

* [ActiveSupport::Inflector](http://api.rubyonrails.org/classes/ActiveSupport/Inflector.html)

<p></p>

NOTE: PRAGMA statement lets us query SQLite library for internal data
and in this case querying a table for all its values to only choose clumn names

`PRAGMA table_info(<table name>)`

##### ( The above returns an array of hashes and detailed information about all
column values )

* [SQL Pragma tut](http://www.tutorialspoint.com/sqlite/sqlite_pragma.htm)
* [SQLite doc](https://sqlite.org/pragma.html)

<p></p>


