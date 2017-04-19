---
title: UnitKit Testing Framework
language: objc

assertions:
  - name: UKPass()
    id: uk-pass
    desc: |
      Reports a success.

  - name: UKFail()
    id: uk-fail
    desc: |
      Reports a failure.

  - name: UKTrue(condition)
    id: uk-true
    desc: |
      Tests that an expression is true.

  - name: UKFalse(condition)
    id: uk-false
    desc: |
      Tests that an expression is false.

  - name: UKNil(ref)
    id: uk-nil
    desc: |
      Tests that `ref == nil`.

  - name: UKNotNil(ref)
    id: uk-not-nil
    desc: |
      Tests that `ref != nil`.

  - name: UKIntsEqual(a, b)
    id: uk-ints-equal
    desc: |
      Tests that two primitive integers are equal.

      `a` is the expected value and `b` the tested value.

      Don't pass `unsigned long long` integers that cannot safely casted to `long long`.

  - name: UKIntsNotEqual(a, b)
    id: uk-ints-not-equal
    desc: |
      Tests that two primitive integers are not equal.

      `a` is the non-expected value and `b` the tested value.

      Don't pass `unsigned long long` integers that cannot safely casted to `long long`.

  - name: UKFloatsEqual(a, b, d)
    id: uk-floats-equal
    desc: |
      Tests that two primitive floats are equal or almost,
      this evaluates whether `fabs(a - b) <= d` is `true`.

      `d` is the error margin.

      `a` is the expected value and `b` the tested value.

  - name: UKFloatsNotEqual(a, b, d)
    id: uk-floats-not-equal
    desc: |
      Tests that two primitive floats are not equal,
      this evaluates whether `fabs(a - b) > d` is `true`.

      `d` is the error margin.

      `a` is the non-expected value and `b` the tested value.

  - name: UKObjectKindOf(a, b)
    id: uk-object-kind-of
    desc: |
      Tests that `a` is a subclass of `b`.

  - name: UKObjectsEqual(a, b)
    id: uk-objects-equal
    desc: |
      Tests that `[a isEqual: b]`.

      `a` is the expected value and `b` the tested value.

  - name: UKObjectsNotEqual(a, b)
    id: uk-objects-not-equal
    desc: |
      Tests that `![a isEqual: b]`.

      `a` is the non-expected value and `b` the tested value.

  - name: UKObjectsSame(a, b)
    id: uk-objects-same
    desc: |
      Tests that the objects are identical with `a == b`.

      `a` is the expected value and `b` the tested value.

  - name: UKObjectsNotSame(a, b)
    id: uk-objects-not-same
    desc: |
      Tests that the objects are not identical with `a != b`.

      `a` is the non-expected value and `b` the tested value.

  - name: UKStringsEqual(a, b)
    id: uk-strings-equal
    desc: |
      Tests that `[a isEqual: b]`.

      `a` is the expected value and `b` the tested value.

  - name: UKStringsNotEqual(a, b)
    id: uk-strings-not-equal
    desc: |
      Tests that `![a isEqual: b]`.

      `a` is the non-expected value and `b` the tested value.

  - name: UKStringContains(a, b)
    id: uk-strings-contains
    desc: |
      Tests that `b` is a substring of `a`.

  - name: UKStringDoesNotContain(a, b)
    id: uk-strings-does-not-contain
    desc: |
      Tests that `b` is not a substring of `a`.

  - name: UKRaisesException(a)
    id: uk-raises-exception
    desc: |
      Tests that the code piece raises an exception.

  - name: UKDoesNotRaiseException(a)
    id: uk-does-not-raise-exception
    desc: |
      Tests that the code piece raises no exception.

  - name: UKRaisesExceptionNamed(a, b)
    id: uk-raises-exception-named
    desc: |
      Tests that the code piece raises an exception of the name `b`.

  - name: UKRaisesExceptionClass(a, b)
    id: uk-raises-exception-class
    desc: |
      Tests that the code piece raises an exception of the class name `b`.
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

{% comment %}

{% for a in page.assertions %}
- [`{{ a.name }}`](#{{ a.id }})
{% endfor %}

{% endcomment %}

For a full list of assertions see [UKTest.h](https://github.com/etoile/UnitKit/blob/master/FrameworkSource/UKTest.h).

{% for a in page.assertions %}
### `{{a.name}}` {#{{ a.id }}}

{{ a.desc | markdownify }}
{% endfor %}

{% comment %}

- https://www.qualified.io/kb/languages/objc/unitkit
  - Corrected the second `UKFloatsEqual` to `UKFloatsNotEqual`
  - Added more from UKTest.h

{% endcomment %}


{% comment %}

POC using YAML Front Matter

Pros:

- Documentation data
  - Can be used to generate table of contents server-side
- Helps to keep consistency
- Allows more complex markups without raising the contribution barrier

Cons:

- Browsing files on GitHub :(
  But this is already affected by using front matters and liquid templates.

{% endcomment %}
