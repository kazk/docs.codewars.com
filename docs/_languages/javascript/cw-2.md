---
title: Codewars Testing Framework
---

# Codewars Testing Framework

The `Test` object provides the testing functionality needed to validate a kata's requirements.
It is a frozen object and cannot be modified.

## Assertions

### Test.expect(passed[, message]) {#expect}

Core assertion method that all other methods build off of.
`message` argument is optional.
If it is not provided then a generic message will be used.
Best practice is to provide your own message.
Pass/Fail status will be written to the output stream.

### Test.assertEquals(actual, expected[, message]) {#assert-equals}

Checks that the actual value equals (`===`) the expected value.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional. If given it will be displayed in addition to the typical message used.

### Test.assertNotEquals(actual, unexpected[, message]) {#assert-not-equals}

Checks that the actual value does not equal (`!==`) the unexpected value.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional.
If given it will be displayed in addition to the typical message used.

### Test.assertSimilar(actual, expected[, message]) {#assert-similar}

Checks that the actual value equals (`===`) the expected value.
[`Test.inspect`](#inspect) is used to wrap the values being tested,
allowing for similar values to be considered the same.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional. If given it will be displayed in addition to the typical message used.

### Test.assertNotSimilar(actual, unexpected[, message]) {#assert-not-similar}

Checks that the actual value does not equal (`!==`) the unexpected value.
[`Test.inspect`](#inspect) is used to wrap the values being tested,
allowing for similar values to be considered the same.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional. If given it will be displayed in addition to the typical message used.

### Test.assertDeepEquals(actual, expected[, message]) {#assert-deep-equals}

Checks that the actual value equals the expected value by performing deep comparison.
Unlike [`Test.assertSimilar`](#assert-similar), values are not turned into strings.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional. If given it will be displayed in addition to the typical message used.

### Test.assertNotDeepEquals(actual, unexpected[, message]) {#assert-not-deep-equals}

Checks that the actual value does not equal the unexpected value by performing deep comparison.
Unlike [`Test.assertNotSimilar`](#assert-not-similar), values are not turned into strings.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional. If given it will be displayed in addition to the typical message used.

### Test.assertContains(actual, expected[, message]) {#assert-contains}

Checks that the actual value contains the expected element.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional. If given it will be displayed in addition to the typical message used.

### Test.assertNotContains(actual, unexpected[, message]) {#assert-not-contains}

Checks that the actual value does not contain the unexpected element.
A useful message will be displayed for both pass and fail outcomes.
The `message` argument is optional. If given it will be displayed in addition to the typical message used.

### Test.expectError([message, ]fn) {#expect-error}

Useful for testing that an error was expected to happen.
`message` is optional but best practice is to provide one.

### Test.expectNoError([message, ]fn) {#expect-no-error}

Useful for testing that an error was not expected to happen.
`message` is optional but best practice is to provide one.

## Spec Methods

### Test.describe(subject, fn) {#describe}

Top level method for describing/grouping a set of tests. Globally aliased as `describe`.

```javascript
describe("Foo", function() {

});

// or

Test.describe("Foo", function() {

});
```

### Test.it(subject, fn) {#it}

Used in conjunction with describe to group related sets of tests in a spec. Globally aliased as `it`.

```javascript
describe("Foo", function() {
  it("should be defined", function() {
    Test.expect(this.Foo, "Foo is not defined");
  });
});
```

### Test.before(callback) {#before}

Any callbacks sent to this method will be called before each it spec is ran. Globally aliased as `before`.

```javascript
// this is a contrived example
describe("Foo", function() {
  var a = 0;

  // called before each spec is ran
  before(function() {
    a++;
  });

  it("should should do something", function() {
    Test.assertEquals(a, 1);
  });

  it("should do something else", function() {
    Test.assertEquals(a, 2);
  });
});
```

## Helper Methods

### Test.inspect(object) {#inspect}

Returns a string representation of the object.

### Test.randomize(array) {#randomize}

Shuffles the contents of an array.

### Test.randomNumber() {#random-number}

Returns a random integer.

### Test.randomToken() {#random-token}

Returns a random string of characters.

### Test.sample(array) {#sample}

Returns a single, randomly chosen item from an array.

