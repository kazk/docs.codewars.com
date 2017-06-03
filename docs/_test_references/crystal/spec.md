---
title: spec
language: crystal
---

# {{ page.title }}

[`spec`](https://crystal-lang.org/api/0.21.1/Spec.html) module can be used to test Crystal code.

## Basic Setup

```ruby
def add(a, b)
  a + b
end
```

```ruby
describe "simple test" do
  it "should add" do
    add(1, 1).should eq 2
  end
end
```
