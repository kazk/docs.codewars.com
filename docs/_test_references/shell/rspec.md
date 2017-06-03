---
title: RSpec for Shell
language: shell
---

# RSpec Testing Framework for Shell

Codewars supports the RSpec behavior-driven testing framework.

These notes are adopted from [rspec-core](http://rspec.info/documentation/3.3/rspec-core/).

## Basic Example

RSpec uses the words "describe" and "it" so we can express concepts like a conversation:

```
"Describe the adder script."
"It adds two numbers."
```

```ruby
describe 'adder script' do
  it "adds two numbers" do
    test = run_shell args: [2, 3]
    expect(test).to eq('5')
  end
end
```

The describe method creates an `ExampleGroup`.
Within the block passed to describe you can declare examples using the `it` method.

Under the hood, an example group is a class in which the block passed to describe is evaluated.
The blocks passed to it are evaluated in the context of an instance of that class.

## Get Started

Start with a simple example of behavior you expect from your system:

```ruby
describe 'subtractor script' do
  it "subtracts two numbers" do
    test = run_shell args: [5, 2]
    expect(test).to eq('3')
  end
end
```

Run this by clicking the **VALIDATE TEST CASES** in the challenge creator,
or **RUN TESTS** when taking a challenge,
and you will see a failure similar to:

```
subtractor script
  subtracts two numbers
  ✘ expected: "3"
         got: ""

    (compared using ==)
```

Address the failure by defining the script:

```shell
#!/bin/bash

echo $(($1 - $2))
```

Now run the spec again, and watch it pass:

```
subtractor script
  #subtracts two numbers
    Test Passed
```

# Learn More

You can learn how to use it on the [RSpec website](http://rspec.info/).


{% comment %}

- <https://www.qualified.io/kb/languages/shell/rspec>

- Fixed the last output having "adder script"

- Should substitute Qualified terms with Codewars terms, e.g, challenge/kata

{% endcomment %}
