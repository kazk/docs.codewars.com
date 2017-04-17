---
title: clojure.test Testing Framework
category: testing
---

# clojure.test Testing Framework

## Overview

Codewars supports [clojure.test](http://clojure.github.io/clojure/clojure.test-api.html), the built-in testing framework for Clojure 1.6.0

The following notes are largely derived from: [clojure.test - Clojure API Documentation](http://clojure.github.io/clojure/clojure.test-api.html).

## Setup

A minimal test fixture looks as follows:

Solution Code:

```clojure
(ns clojure.greeter)

(defn make-greeter [greeter-name]
  (fn [your-name]
    (format "My name is %s! Welcome, %s!"
             greeter-name
             your-name)))
```

Test Fixture:

```clojure
(ns clojure.greeter-test
  (:require [clojure.test :refer :all]
            [clojure.greeter :refer :all]))

(deftest Greetings
  (is
   (= ((make-greeter "Shoki, the Demon Queller")
       "Son Gokū, the Monkey King")
      "My name is Shoki, the Demon Queller! Welcome, Son Gokū, the Monkey King!")))
```

## is

The core of the `clojure.test` library is the `is` macro, which lets you make assertions of any arbitrary expression:

```clojure
(is (= 4 (+ 2 2)))
(is (instance? Integer 256))
(is (.startsWith "abcde" "ab"))
```

These are all passing tests. They are all expected to output:

```
Test Passed
```

The following test won't pass, however:

```clojure
(deftest Will-Fail
  (is (= 5 (+ 2 2))))
```

It will output:

```
Will-Fail
   expected: (= 5 (+ 2 2)) - actual: (not (= 5 4))
```

The `expected:` line shows you the original expression, and the `actual:` shows you what actually happened.
In this case, it shows that `(+ 2 2)` returned `4`, which is not `=` to `5`.

There are two special assertions for testing exceptions.
The `(is (thrown? c ...))` form tests if an exception of class `c` is thrown:

```clojure
(is (thrown? ArithmeticException (/ 1 0)))
```

`(is (thrown-with-msg? c re ...))` does the same thing and
also tests that the message on the exception matches the regular expression `re`:

```clojure
(is (thrown-with-msg? ArithmeticException #"Divide by zero" (/ 1 0)))
```

### Documenting Tests

`is` takes an optional second argument, a string describing the assertion.
This message will be included in the error report.

```clojure
(is (= 5 (+ 2 2)) "Crazy arithmetic")
```

In addition, you can document groups of assertions with the "testing" macro, which takes a string followed by any number of assertions.
The string will be included in failure reports.
Calls to "testing" may be nested, and all of the strings will be joined together with spaces in the final report,
in a style similar to [RSpec](http://rspec.info/).

```clojure
(testing "Arithmetic"
  (testing "with positive integers"
    (is (= 4 (+ 2 2)))
    (is (= 7 (+ 3 4))))

  (testing "with negative integers"
    (is (= -4 (+ -2 -2)))
    (is (= -1 (+ 3 -4)))))
```

Note that, unlike RSpec, the `testing` macro may only be used INSIDE a `deftest`.

## are

Usage: `(are argv expr & args)`

Checks multiple assertions with a template expression.

See [clojure.template/do-template](https://clojure.github.io/clojure/clojure.template-api.html#clojure.template/do-template)
for an explanation of templates.

Example:

```clojure
(are [x y] (= x y)
     2 (+ 1 1)
     4 (* 2 2))
```

Expands to:

```clojure
(do (is (= 2 (+ 1 1)))
    (is (= 4 (* 2 2))))
```

Note: This breaks some reporting features, such as line numbers.

## with-redefs

One of the most powerful tools of testing in clojure is the `with-redefs` macro, which allows you to _mock_ functions.

This is especially useful when you want to prevent access to built-ins for some exercise.
For example, the following disables `clojure.core/reverse`:

```clojure
(with-redefs
  [clojure.core/reverse
   (fn [& _]
     (throw (Exception. "Sorry! The reverse built-in is disabled for this kata!")))]

  (deftest Reversing
    (is (= (reverse [1]) [1]))))
```

We should expect this test to fail, since it is clearly is using `clojure.core/reverse`.
