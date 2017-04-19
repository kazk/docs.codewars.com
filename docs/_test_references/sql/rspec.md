---
title: RSpec Testing Framework for SQL
language: sql
---

# RSpec Testing Framework for SQL

Codewars supports the RSpec behavior-driven testing framework, which uses Ruby.

These notes are adopted from [rspec-core](http://rspec.info/documentation/3.3/rspec-core/).

## Why Ruby/RSpec?

Since SQL is a query language it cannot be used to write unit tests.
Ruby was choosen instead to execute the unit tests.
Ruby and RSpec are both very easy to learn.
Our usage of Ruby also allows you to setup any initial data within the database, support special visualizations and advanced output, etc.

## RSpec SQL custom utilities

A small set of utility methods and classes have been provided to make testing and displaying SQL queries easier within Ruby.
These utility methods are available both within the Preloaded Code (data setup) and Test Cases.

* `$sql` is a global variable which contains the user's SQL solution
* `run_sql` is a method that will run the user's query,
  execute any non-SELECT statements and print and return any result sets from SELECT statements.
* `compare_to` is a method which can be used to compare the candidate's submitted query to your own,
  which will then auto generate a bunch of specs for you based off of the expected query results.

### [Sequel](http://sequel.jeremyevans.net)

We utilize the [Sequel](http://sequel.jeremyevans.net) gem to communicate with the database driver.

## Basic Example

RSpec uses the words "describe" and "it" so we can express concepts like a conversation:

```
"Describe a query"
"It should return 5 rows"
```

```ruby
# prints the user's query to the UI and returns the results as a Sequel dataset.
results = run_sql

describe "Query" do
  it "should return 5 rows" do
    expect(results.size).to eq 5
  end
end
```

The describe method creates an `ExampleGroup`.
Within the block passed to describe you can declare examples using the `it` method.

Under the hood, an example group is a class in which the block passed to describe is evaluated.
The blocks passed to it are evaluated in the context of an instance of that class.

## compare_to(expected)

The `compare_to` method takes an `expected` param, which is your own query.
You can embed your own query within the preloaded code like so:

```ruby
def expected
  DB[%q(
    PLACE YOUR QUERY HERE
  )].to_a
end
```

> **Note:** Make sure to always return an array by having `to_a` at the end. Otherwise it's possible to expose the query's SQL string.

Then within your Test cases section you can simply add this:

```
compare_to expected
```

What this will do is compare the expected query results to the results of the candidate's query. It will also print out both the actual results as well as the expected, making it much easier for a candidate to see what is expected of them.

When the results are compared, `describe/it` RSpec blocks will automatically be generated for you based off of the expected data, allowing you to provide meaningful feedback to the candidate telling them where their query went wrong. Specs will be auto-generated for each data column returned, as well as a set of specs related to rows (such as row count).

You can also extend the generated specs. For example:

```ruby
compare_to expected do
  rows do
    it "should have movie titles ordered alphabetically" do
      expect(actual.first[:title]).to be < actual.last[:title]
    end
  end
end
```

## Learn More

You can learn how to use it on the [RSpec website](http://rspec.info/).

{% comment %}

- <https://www.qualified.io/kb/languages/sql/rspec>

- Should substitute Qualified terms with Codewars terms, e.g, candidates.

{% endcomment %}
