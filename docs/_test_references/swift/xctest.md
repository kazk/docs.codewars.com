---
title: XCTest Testing Framework
language: swift
---

# XCTest Testing Framework

## Overview

Codewars supports the [XCTest](https://developer.apple.com/reference/xctest) testing framework.

## XCTest Quick Start

All tests start with a subclass of `XCTestCase`.
You can then add one or more test case methods to that class, each of which must start with `test`.

You must also include the main entry point method to start the tests.

### Assertions

Use `XCTAssert*` functions to create your assertions, for example, `XCTAssertEqual(_ actual:_ expected:_ message)`.

### Example

```swift
import XCTest

class PersonTest: XCTestCase {
    static var allTests = [
        ("testGreet", testGreet),
    ]
    func testGreet() {
        let person = Person("Jorge")
        XCTAssertEqual(person.greet("Aditya"), "Hello, Aditya, I am Jorge, it's nice to meet you!")
    }
}

XCTMain([
  testCase(PersonTest.allTests)
])
```

## Learn More

You can learn more on the Apple [XCTest website](https://developer.apple.com/reference/xctest).

{% comment %}

- <https://www.qualified.io/kb/languages/swift/xctest>

{% endcomment %}
