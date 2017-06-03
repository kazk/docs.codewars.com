---
title: Testing Rust
language: rust
---

# {{ page.title }}

Rust functions can be tested by using attributes.

## Basic Setup

```rust
fn add(a: i32, b: i32) -> i32 {
  a + b
}
```

```rust
#[test]
fn test_add() {
  assert_eq!(add(1, 1), 2);
}
```

## Attributes

- `#[test]` marks a function as a unit test.
- `#[should_panic]` marks a function as a panicking test.
