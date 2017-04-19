---
title: Fuchu Testing Framework
language: fsharp
---

# Fuchu Testing Framework

## Overview

Codewars supports the [Fuchu](https://github.com/mausch/Fuchu) testing framework.

These notes are adapted from the [Fuchu repository](https://github.com/mausch/Fuchu).

## Fuchu Quick Start

Here's the simplest test possible:

```
open Fuchu

let simpleTest =
    testCase "A simple test" <|
        fun _ -> Assert.Equal("2+2", 4, 2+2)
```

Tests can be grouped (with arbitrary nesting):

```
let tests =
    testList "A test group" [
        testCase "one test" <|
            fun _ -> Assert.Equal("2+2", 4, 2+2)
        testCase "another test" <|
            fun _ -> Assert.Equal("3+3", 3, 3+3)
    ]
```

The first parameter in the assertions describes the assertion.
This is usually an optional parameter in most test frameworks;
in Fuchu it's required to foster descriptive failures,
so you'll get a failure like "3+3 Expected value 3, actual 6"
instead of just "Expected value 3, actual 6".

For more examples, including a few ways to do common things in other test frameworks like setup/teardown and parameterized tests,
see the F# tests and the C# tests.

## Assertions

Fuchu is mainly oriented to test organization.
Although it does have a few basic assertions,
 you're encouraged to write your own specialized assertions for each project
(they're only a couple of lines in F#),
or you can use [NUnit]({{ "/languages/csharp/nunit" | relative_url }} "NUnit Testing Framework").

## Learn More

[You can learn more on the Fuchu website](https://github.com/mausch/Fuchu).


{% comment %}

- <https://www.qualified.io/kb/languages/fsharp/fuchu>

kramdown doesn't support F# syntax highlighting because it doesn't support Rouge 2.0.

{% endcomment %}
