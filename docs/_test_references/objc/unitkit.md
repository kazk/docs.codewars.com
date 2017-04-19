---
title: UnitKit Testing Framework
language: objc
---

# UnitKit Testing Framework

Codewars supports [UnitKit](https://github.com/etoile/UnitKit),
a minimalistic testing framework for Objective-C.

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

### `UKPass()` {#uk-pass}

Reports a success.

### `UKFail()` {#uk-fail}

Reports a failure.

### `UKTrue(condition)` {#uk-true}

Tests that an expression is true.

### `UKFalse(condition)` {#uk-false}

Tests that an expression is false.

### `UKNil(ref)` {#uk-nil}

Tests that `ref == nil`.

### `UKNotNil(ref)` {#uk-not-nil}

Tests that `ref != nil`.

### `UKIntsEqual(a, b)` {#uk-ints-equal}

Tests that two primitive integers are equal.

`a` is the expected value and `b` the tested value.

Don't pass `unsigned long long` integers that cannot safely casted to `long long`.

### `UKIntsNotEqual(a, b)` {#uk-ints-not-equal}

Tests that two primitive integers are not equal.

`a` is the non-expected value and `b` the tested value.

Don't pass `unsigned long long` integers that cannot safely casted to `long long`.

### `UKFloatsEqual(a, b, d)` {#uk-floats-equal}

Tests that two primitive floats are equal or almost,
this evaluates whether `fabs(a - b) <= d` is `true`.

`d` is the error margin.

`a` is the expected value and `b` the tested value.

### `UKFloatsNotEqual(a, b, d)` {#uk-floats-not-equal}

Tests that two primitive floats are not equal,
this evaluates whether `fabs(a - b) > d` is `true`.

`d` is the error margin.

`a` is the non-expected value and `b` the tested value.

### `UKObjectKindOf(a, b)` {#uk-object-kind-of}

Tests that `a` is a subclass of `b`.

### `UKObjectsEqual(a, b)` {#uk-objects-equal}

Tests that `[a isEqual: b]`.

`a` is the expected value and `b` the tested value.

### `UKObjectsNotEqual(a, b)` {#uk-objects-not-equal}

Tests that `![a isEqual: b]`.

`a` is the non-expected value and `b` the tested value.

### `UKObjectsSame(a, b)` {#uk-objects-same}

Tests that the objects are identical with `a == b`.

`a` is the expected value and `b` the tested value.

### `UKObjectsNotSame(a, b)` {#uk-objects-not-same}

Tests that the objects are not identical with `a != b`.

`a` is the non-expected value and `b` the tested value.

### `UKStringsEqual(a, b)` {#uk-strings-equal}

Tests that `[a isEqual: b]`.

`a` is the expected value and `b` the tested value.

### `UKStringsNotEqual(a, b)` {#uk-strings-not-equal}

Tests that `![a isEqual: b]`.

`a` is the non-expected value and `b` the tested value.

### `UKStringContains(a, b)` {#uk-strings-contains}

Tests that `b` is a substring of `a`.

### `UKStringDoesNotContain(a, b)` {#uk-strings-does-not-contain}

Tests that `b` is not a substring of `a`.

### `UKRaisesException(a)` {#uk-raises-exception}

Tests that the code piece raises an exception.

### `UKDoesNotRaiseException(a)` {#uk-does-not-raise-exception}

Tests that the code piece raises no exception.

### `UKRaisesExceptionNamed(a, b)` {#uk-raises-exception-named}

Tests that the code piece raises an exception of the name `b`.

### `UKRaisesExceptionClass(a, b)` {#uk-raises-exception-class}

Tests that the code piece raises an exception of the class name `b`.


{% comment %}

- <https://www.qualified.io/kb/languages/objc/unitkit>

- Corrected the second `UKFloatsEqual` to `UKFloatsNotEqual`
- Added more from UKTest.h

{% endcomment %}
