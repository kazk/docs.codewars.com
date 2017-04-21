---
title: Codewars Testing Framework
language: coffeescript
---

# Codewars Testing Framework

A lightweight, custom testing framework for CoffeeScript.

The `Test` object provides the testing functionality needed to validate a kata's requirements.
It is a frozen object and cannot be modified.

## Assertion Methods

### `Test.expect passed, msg`

Core assertion method that all other methods build off of.
`msg` argument is optional.
If it is not provided then a generic message will be used. Best practice is to provide your own message.

Pass/Fail status will be written to the output stream.

### `Test.assertEquals actual, expected, msg`

Checks that the actual value equals (`===`) the expected value.
A useful message will be displayed for both pass and fail outcomes.
The `msg` argument is optional.
If given it will be displayed in addition to the typical message used.

### `Test.assertNotEquals actual, unexpected, msg`

Checks that the actual value does not equal (`!==`) the unexpected value.
A useful message will be displayed for both pass and fail outcomes.
The `msg` argument is optional.
If given it will be displayed in addition to the typical message used.

### `Test.assertSimilar actual, expected, msg`

Checks that the actual value equals (`===`) the expected value.
`Test.inspect` is used to wrap the values being tested, allowing for similar values to be considered the same.
A useful message will be displayed for both pass and fail outcomes.
The `msg` argument is optional.
If given it will be displayed in addition to the typical message used.

### `Test.assertNotSimilar actual, unexpected, msg`

Checks that the actual value does not equal (`!==`) the unexpected value.
`Test.inspect` is used to wrap the values being tested, allowing for similar values to be considered the same.
A useful message will be displayed for both pass and fail outcomes.
The `msg` argument is optional.
If given it will be displayed in addition to the typical message used.

### `Test.expectError msg, fn`

Useful for testing that an error was expected to happen.
`msg` is optional but best practice is to provide one.

### `Test.expectNoError msg, fn`

Useful for testing that an error was not expected to happen.
`msg` is optional but best practice is to provide one.

## Spec Methods

### `describe msg, fn`

Top level method for describing/grouping a set of tests.
Globally aliased as `describe`.

```coffee
describe 'Foo', ->

# or

Test.describe 'Foo', ->
```

### `it msg, fn`

Used in conjunction with describe to group related sets of tests in a spec.
Globally aliased as `it`.

```coffee
describe 'Foo', ->
  it 'should be defined', ->
    Test.expect @Foo, 'Foo is not defined'
```

### `before(fn)`

Any callbacks sent to this method will be called before each `it` spec is ran.

```coffee
# this is a contrived example
describe 'Foo', ->
  a = 0

  # called before each spec is ran
  before ->
    a++

  it 'should should do something', ->
    Test.assertEquals a, 1

  it 'should do something else', ->
    Test.assertEquals a, 2
```

## Helper Methods

### `Test.inspect object`

Returns a string representation of the object.

### `Test.randomize array`

Shuffles the contents of an array.

### `Test.randomNumber()`

Returns a random integer.

### `Test.randomToken()`

Returns a random string of characters.

### `Test.sample array`

Returns a single, randomly chosen item from an array.


{% comment %}

- <https://www.qualified.io/kb/languages/coffeescript/cw-2>
- Removed `Test.callCount methodName → Integer` for Codewars
-
{% endcomment %}
