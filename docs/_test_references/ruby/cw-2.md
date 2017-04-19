---
title: Codewars Testing Framework
language: ruby
---

# Codewars Testing Framework

The Test class provides the testing functionality needed to validate a kata's requirements.
It is a frozen singleton class and cannot be modified.

## Assertions

### `Test.expect(passed, msg = nil)` {#expect}

Core assertion method that all other methods build off of.
The `msg` argument is optional.
If it is not provided then a generic message will be used.
Best practice is to provide your own message.
Pass/Fail status will be written to the output stream.

### `Test.assert_equals(actual, expected, msg = nil)` {#assert-equals}

Checks that the actual value equals the expected value.
A useful message will be displayed for both pass and fail outcomes.
The `msg` argument is optional.
If given it will be displayed in addition to the typical message used.

### `Test.assert_not_equals(actual, unexpected, msg = nil)` {#assert-not-equals}

Checks that the actual value does not equal the unexpected value.
A useful message will be displayed for both pass and fail outcomes.
The `msg` argument is optional.
If given it will be displayed in addition to the typical message used.

### `Test.expect_error(msg, &block)` {#expect-error}

Useful for testing that an error was expected to happen.
The `msg` is optional but best practice is to provide one.

### `Test.expect_no_error(msg, &block)` {#expect-no-error}

Useful for testing that an error was not expected to happen.
The `msg` is optional but best practice is to provide one.


## Spec Methods

### `Test.describe(msg, &block)` {#describe}

Top level method for describing/grouping a set of tests.
Globally aliased as `describe`.

```ruby
describe "Foo" do

end

# or

Test.describe "Foo" do

end
```

### `Test.it(msg, &block)` {#it}

Used in conjunction with describe to group related sets of tests in a spec.
Globally aliased as `it`.

```ruby
describe "Foo" do
  it "should be defined" do
    Test.expect(defined?(Foo), "Foo is not defined")
  end
end
```

### `Test.before(&block)` {#before}

Any blocks sent to this method will be called before each `it` spec is ran.

```ruby
# this is a contrived example
describe "Foo" do
  a = 0

  # called before each spec is ran
  before do
    a++
  end

  it "should should do something" do
    Test.assert_equals(a, 1)
  end

  it "should do something else" do
    Test.assert_equals(a, 2)
  end
end
```

## Helper Methods

### `Test.random_number()` {#random-number}

Returns a random number.

### `Test.random_token()` {#random-token}

Returns a random string.


{% comment %}

- <https://www.codewars.com/docs/ruby-test-reference>
- <https://www.qualified.io/kb/languages/ruby/cw-2>

{% endcomment %}
