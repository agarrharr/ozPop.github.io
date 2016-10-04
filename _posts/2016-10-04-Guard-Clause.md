---
layout: post
title: Guard Clause Pattern
header-img: ""
---

### How I came across Guard Clause Pattern

I recently installed a plugin for Sublime Text called [Rubocop](https://github.com/bbatsov/rubocop).

![Rubocop img](https://raw.githubusercontent.com/bbatsov/rubocop/master/logo/rubo-logo-horizontal.png)

Rubocop is a static code analyzer that will enforce many of the guidelines outlined in the community driven [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide).

Soon after setting up Rubocop and seeing my editor light up in ways I have not yet seen, I noticed one particular error that kept coming up quite frequently when I used conditional statements inside methods.

```ruby
def method_zero
    if something
        this
        that
    end
end
```

**The Error:**

    Use a guard clause instead of wrapping the code inside a conditional expression

At the time, having no clue as to what this meant I decided to do some digging. To my surprise, I learned that not only have I already been using the guard clause, but that there are a couple of different ways it is used.

### Definition

_Note: Guard Clause Pattern is also known as Bouncer Pattern._

A guard clause is a conditional statement at the top of a function/method that is used as a check to avoid errors during execution, getting rid of bad cases before they slip in. Another common use case for a guard clause is to check if an entity that is about to be processed is not `nil`.

Guard Clause Pattern provides an early exit from a method, and is a commonly used to simplify and flatten the code removing one level of nesting and in some cases making debugging easier.

It typically does one of the following:

* checks the passed-in parameters, and returns with an error if they're not suitable.
* checks the state of the object, and bails out if the function call is inappropriate.
* checks for trivial cases, and gets rid of them quickly.

### A Note on the past

Before modern programming languages [Edsger Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra) coined the term _"structured programming"_. This type of programming enforced structure in a program to promote maintainability and ease of understanding. These concepts relied on a single entry concept which usually included a single exit, to ease the delineation of a function/method.

Single entry and exit point was original concept of structured programming to combat spaghetti coding as it allowed a clean analysis. It is worth mentioning that it is, at least in certain cases, still considered good practice when a method/function has only one exit point. This still is especially true for languages that require decent memory management such as C. 

It seems for more modern programming languages such as Ruby, where you have a garbage collection happening in the background, that is no longer applicable and the benefits of Guard Clause Pattern are now considered good practice.

### Examples

### 1.
----

Typical nesting

```ruby
def require_vip
    if current_user.vip?
        this
        that
    end
end
```

Guard Clause

```ruby
    def require_vip
        return unless current_user.vip? # <-- Guard Clause
        this
        that
    end
```

### 2.
----

Checking passed in parameter using nesting

```ruby
def method_one(variable)
  if variable == 'something'
    # do something
  else
    return nil
  end
end
```

Guard Clause

```ruby
def method_one(variable)
    return nil unless variable == 'something' # <-- Guard Clause
    # do something
end
```

### 3.
----

Multi nested example

```ruby
def method_two(variable)
    if variable.a?
        return false
    else
        if variable.b?
            variable.do_this
        elsif variable.c?
            variable.do_that
        else
            variable.do_everything_else
        end
    end
end
```

Guard Clause

```ruby
    def method_two(variable)
        return false if variable.a? # <-- Guard Clause 1
        return variable.do_this if variable.b? # <-- Guard Clause 2
        return variable.do_that if variable.c? # <-- Guard Clause 3
        variable.do_everything_else
    end
```

In conclusion I would like to say that like with most things in programming, Guard Clause can help when used in appropriate circumstances. Do not shy away from a nested conditional if it better suits your needs but do consider using a Gaurd Clause if it makes sense in that particular scenario.


Source:

* [Wikipage](https://en.wikipedia.org/wiki/Guard_(computer_science))
* [Rubocop docs](http://www.rubydoc.info/gems/rubocop/RuboCop/Cop/Style/GuardClause)
* [What are Guard Clauses](https://samurails.com/refactoring/what-are-guard-clauses/)
* [Prefer Guard Clauses Over Nested Conditionals](http://www.thechrisoshow.com/2009/02/16/using-guard-clauses-in-your-ruby-code/)
* [The Guard Clause Pattern](http://www.chrisrolle.com/blog/the-guard-clause-pattern)
* [Structured Programming](https://en.wikipedia.org/wiki/Structured_programming)
* [Single Function Exit Point](http://c2.com/cgi/wiki?SingleFunctionExitPoint)
* [Single-Entry, Single-Exit](http://blogs.msmvps.com/peterritchie/2008/03/07/single-entry-single-exit-should-it-still-be-applicable-in-object-oriented-languages/)