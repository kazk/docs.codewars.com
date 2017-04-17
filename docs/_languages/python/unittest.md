---
title: unittest Testing Framework
---

# unittest Testing Framework

Codewars supports the `unittest` unit testing framework.

These notes are adopted from [unittest — Basic Example.](https://docs.python.org/2/library/unittest.html#basic-example)

## Basic Example

The `unittest` module provides a rich set of tools for constructing and running tests.
This section demonstrates that a small subset of the tools suffice to get started.

Here is a short script to test three string methods:

```python
import unittest

class Test(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)
```

## Test class

You **must** have a class named `Test`, which is a subclass of `unittest.TestCase`.

## Tests

In the example, the three individual tests are defined with methods whose names start with the letters `test`.
This naming convention informs the test runner about which methods represent tests.

## Assertions

The crux of each test is a call to `assertEqual()` to check for an expected result;
`assertTrue()` or `assertFalse()` to verify a condition;
or `assertRaises()` to verify that a specific exception gets raised.
These methods are used instead of the `assert` statement so the test runner can accumulate all test results and produce a report.

## Setup and Tear Down

The `setUp()` and `tearDown()` methods allow you to define instructions that will be executed before and after each test method.

## Learn More

[You can learn how to use it on the Python Website](https://docs.python.org/2/library/unittest.html).

