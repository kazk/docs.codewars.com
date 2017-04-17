---
title: RSpec Testing Framework
---

{% comment %}
https://www.qualified.io/kb/languages/ruby/rspec
{% endcomment %}

# RSpec Testing Framework

Codewars supports the RSpec behavior-driven testing framework.

These notes are adopted from [rspec-core.](http://rspec.info/documentation/3.3/rspec-core/)

## Basic Example

RSpec uses the words "describe" and "it" so we can express concepts like a conversation:

```
"Describe an order."
"It sums the prices of its line items."
```

```ruby
describe Order do
  it "sums the prices of its line items" do
    order = Order.new

    order.add_entry(LineItem.new(:item => Item.new(
      :price => Money.new(1.11, :USD)
    )))
    order.add_entry(LineItem.new(:item => Item.new(
      :price => Money.new(2.22, :USD),
      :quantity => 2
    )))

    expect(order.total).to eq(Money.new(5.55, :USD))
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
describe Calculator do
  describe '#add' do
    it 'returns the sum of its arguments' do
      expect(Calculator.new.add(1, 2)).to eq(3)
    end
  end
end
```

Run this by clicking the **VALIDATE TEST CASES** in the challenge creator, or **RUN TESTS** when taking a challenge,
and you will see a failure similar to:

```
uninitialized constant Calculator (NameError)
```

Address the failure by defining a skeleton of the Calculator class in the _Solution_ code area:

```ruby
class Calculator
  def add(a, b)
  end
end
```

Now run the spec again, and watch the expectation fail:

```
expected: 3 got: nil (compared using ==)
```

Implement the simplest solution, by changing the definition of Calculator#add to:

```ruby
def add(a, b)
  a + b
end
```

Now run the spec again, and watch it pass:

```
Calculator
  #add
    returns the sum of its arguments
      Test Passed
```

# Learn More

[You can learn how to use it on the RSpec Website](http://rspec.info/).
