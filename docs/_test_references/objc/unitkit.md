---
title: UnitKit Testing Framework
language: objc
---

# UnitKit Testing Framework

Codewars supports the [UnitKit](https://github.com/etoile/UnitKit) unit testing framework,
which is a minimalistic testing framework for Objective-C.

## Basic Setup

```objc
@implementation TestSuite
  // add a test here
  // this must start with test
  - (void) testAddOne
  {
    // add assertions here
    UKIntsEqual(@1, addOne(@2));
  }
@end
```


## Assertions

For a full list of assertions see [UKTest.h](https://github.com/etoile/UnitKit/blob/master/FrameworkSource/UKTest.h).

### `UKPass()`

Reports a success.

### `UKFail()`

Reports a failure.

### `UKTrue(condition)`

Tests that an expression is true.

### `UKFalse(condition)`

Tests that an expression is false.

### `UKNil(ref)`

Tests that `ref == nil`.

### `UKNotNil(ref)`

Tests that `ref != nil`.

### `UKIntsEqual(a, b)`

Tests that two primitive integers are equal.

`a` is the expected value and `b` the tested value.

Don't pass `unsigned long long` integers that cannot safely casted to `long long`.

### `UKIntsNotEqual(a, b)`

Tests that two primitive integers are not equal.

`a` is the non-expected value and `b` the tested value.

Don't pass `unsigned long long` integers that cannot safely casted to `long long`.

### `UKFloatsEqual(a, b, d)`

Tests that two primitive floats are equal or almost, this evaluates whether `fabs(a - b) <= d` is `true`.

`d` is the error margin.

`a` is the expected value and `b` the tested value.

### `UKFloatsEqual(a, b, d)`

Tests that two primitive floats are not equal, this evaluates whether `fabs(a - b) > d` is `true`.

`d` is the error margin.

`a` is the non-expected value and `b` the tested value.

### `UKObjectsEqual(a, b)`

Tests that `[a isEqual: b]`.

`a` is the expected value and `b` the tested value.

### `UKObjectsNotEqual(a, b)`

Tests that `![a isEqual: b]`.

`a` is the non-expected value and `b` the tested value.

### `UKObjectsSame(a, b)`

Tests that the objects are identical with `a == b`.

`a` is the expected value and `b` the tested value.

### `UKObjectsNotSame(a, b)`

Tests that the objects are not identical with `a != b`.

`a` is the non-expected value and `b` the tested value.


{% comment %}
https://www.qualified.io/kb/languages/objc/unitkit
{% endcomment %}
