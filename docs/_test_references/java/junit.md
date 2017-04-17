---
title: JUnit Testing Framework
language: java
---

# JUnit Testing Framework

## Overview

Codewars supports writing test fixtures for Java using [JUnit 4](http://junit.org/).

The notes are adapted from: [Unit Testing with JUnit - Tutorial (vogella.com)](http://www.vogella.com/tutorials/JUnit/article.html)

## Basic Setup

Solution Code:

```java
// Make sure your class is public
public class Calculator {
  // You can't test private methods, so it's
  public Double multiply(Double a, Double b) {
    return a * b;
  }
}
```

Test Fixture:

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class CalculatorTest {
  @Test
  public void testAssociativityOfMultiplication() throws Exception {
    Calculator calc = new Calculator();
    // Try to test for behavior, rather than specific inputs
    // Otherwise people may try to cheat, and only program for exercise inputs!
    for (int i = 0; i < 100; i++) {
      Double a = Math.random();
      Double b = Math.random();
      Double c = Math.random();
      String message = String.format("(%g * %g) * %g == %g * (%g * %g)", a, b, c, a, b, c);
      assertEquals(message,
              calc.multiply(calc.multiply(a, b), c),
              calc.multiply(a, calc.multiply(b, c)),
              1E-14);
    }
  }
}
```

## Annotations

JUnit 4 uses annotations to mark methods and to configure the test run.
The following table gives an overview of the most important available annotations.

|--------------------------------------+---------------------------------------------------------|
| Annotation                           | Description                                             |
|:-------------------------------------|:--------------------------------------------------------|
| `@Test`                              | Identifies a method as a test method.                   |
|--------------------------------------|---------------------------------------------------------|
| `@Test (expected = Exception.class)` | Fails if the method does not throw the named exception. |
|--------------------------------------|---------------------------------------------------------|
| `@Test(timeout=100)`                 | Fails if the method takes longer than 100 milliseconds. |
|--------------------------------------|---------------------------------------------------------|
| `@Before`                            | Executed before each test.                              |
|--------------------------------------|---------------------------------------------------------|
| `@After`                             | Executed after each test.                               |
|--------------------------------------|---------------------------------------------------------|
| `@BeforeClass`                       | Executed once, before the start of all tests.           |
|--------------------------------------|---------------------------------------------------------|
| `@AfterClass`                        | Executed once, after all tests have been finished.      |
|--------------------------------------|---------------------------------------------------------|
| `@Ignore`                            | Marks that the test should be disabled.                 |
| `@Ignore("Why disabled")`            | It is best practice to provide the optional description.|
|--------------------------------------+---------------------------------------------------------|

## Assertions

JUnit provides static methods in the `Assert` class to test for certain conditions.
These _assertion methods_ typically start with `assert` and allow you to specify the error message,
the expected and the actual result.
An _assertion method_ compares the actual value returned by a test to the expected value,
and throws an `AssertionException` if the comparison test fails.

The following table gives an overview of these methods.
Parameters in `[]` brackets are optional.

|--------------------------------------------------------+---------------------------------------------------------|
| Statement                                              | Description                                             |
|:-------------------------------------------------------|:--------------------------------------------------------|
| `fail([message])`                                      | Let the method fail. Might be used to check that a certain part of the code is not reached or to have a failing test before the test code is implemented.|
|--------------------------------------------------------|---------------------------------------------------------|
| `assertTrue([message,] boolean condition)`             | Checks that the boolean condition is true.              |
|--------------------------------------------------------|---------------------------------------------------------|
| `assertFalse([message,] boolean condition)`            | Checks that the boolean condition is false.             |
|--------------------------------------------------------|---------------------------------------------------------|
| `assertEquals([message,] expected, actual)`            | Tests that two values are the same. Note: for arrays the reference is checked not the content of the arrays. |
|--------------------------------------------------------|---------------------------------------------------------|
| `assertEquals([message,] expected, actual, tolerance)` | Test that float or double values match. The tolerance is the number of decimals which must be the same. |
|--------------------------------------------------------|---------------------------------------------------------|
| `assertNull([message,] object)`                        | Checks that the object is null.                         |
|--------------------------------------------------------|---------------------------------------------------------|
| `assertNotNull([message,] object)`                     | Checks that the object is not null.                     |
|--------------------------------------------------------|---------------------------------------------------------|
| `assertSame([message,] expected, actual)`              | Checks that both variables refer to the same object.    |
|--------------------------------------------------------|---------------------------------------------------------|
| `assertNotSame([message,] expected, actual)`           | Checks that both variables refer to different objects.  |
|--------------------------------------------------------+---------------------------------------------------------|


## Matchers

The `assertThat` method allows the use of the [CoreMatchers](http://junit.org/junit4/javadoc/4.10/org/hamcrest/CoreMatchers.html) DSL for specifying tests.

|--------------------------------------------------------+---------------------------------------------------------|
| Matcher                                                | Description                                             |
|:-------------------------------------------------------|:--------------------------------------------------------|
| `is(thing)`                                            | Overloaded, swiss-army-knife method. Can check class membership, decorate another matcher, or check for equality. |
|--------------------------------------------------------|---------------------------------------------------------|
| `equalTo(T expected)`                                  | Matches if the actual value is equal to the expected. You can use `is(T expected)` as shorthand. |
|--------------------------------------------------------|---------------------------------------------------------|
| `describedAs(String description, Matcher matcher)`     | Overrides the description when the `matcher` fails      |
|--------------------------------------------------------|---------------------------------------------------------|
| `allOf(Matcher... matchers)`                           | Evaluates to true only if ALL of the passed in matchers evaluate to true. |
|--------------------------------------------------------|---------------------------------------------------------|
| `anyOf(Matcher... matchers)`                           | Evaluates to true if ANY of the passed in `matchers` evaluate to true. |
|--------------------------------------------------------|---------------------------------------------------------|
| `anything()`                                           | This matcher always evaluates to true                   |
|--------------------------------------------------------|---------------------------------------------------------|
| `not(T matcher)`                                       | Matches only if the underlying `matcher` does not.      |
|--------------------------------------------------------+---------------------------------------------------------|


**Examples:**

```java
import static org.hamcrest.CoreMatchers.*;
import static org.junit.Assert.assertThat;

// ...

assertThat("Help! Integers don't work", 0, is(1));
/* Fails with message:
 * Help! Integers don't work
 * expected: is <1>
 * got value: <0>
 */
assertThat("Zero is one", 0, is(not(1))); // passes
```

For more notes on this see [org.hamcrest.CoreMatchers](http://junit.org/junit4/javadoc/4.10/org/hamcrest/CoreMatchers.html).

## Best practices

Writing JUnit tests Codewars is different than other environments. Here are some tips:

* You are encouraged to output what you are testing when you test it.
  That way, the person doing the exercise has some visibility into what went wrong.
* Make randomized tests; try to test for _behavior_, rather than specific input/output pairs
* Try to use underscores rather than camel case, as it makes it easier to read the test runner results
* Try not to use the `assertTrue` test assertion, it's almost never informative to the person doing the exercise


{% comment %}
https://www.codewars.com/docs/java-test-reference
https://www.qualified.io/kb/languages/java/junit
Fixed dead link
{% endcomment %}
