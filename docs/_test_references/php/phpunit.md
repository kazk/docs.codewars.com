---
title: PHPUnit
language: php
---

# {{ page.title }}

Codewars supports [PHPUnit](https://phpunit.de/) testing framework.

All tests start with a subclass of `TestCase`.
You can then add one or more test case methods to that class,
each of which must start with `test`.

## Assertions

Use `$this->assert*` methods to create your assertions,
such as `$this->assertEquals(expected, actual, [message])`.

**Example**

```php?start_inline=true
class TwoOldestAgesFunction extends TestCase {
    public function testAlgorithm() {
        $results1 = twoOldestAges([1, 5, 87, 45, 8, 8]);
        $this->assertEquals(45, $results1[0]);
        $this->assertEquals(87, $results1[1]);
        $results2 = twoOldestAges([6, 5, 83, 5, 3, 18]);
        $this->assertEquals([18, 83], $results2);
    }
}
```

## Learn More

You can learn more on the [PHPUnit website](https://phpunit.de/).

{% comment %}

- <https://www.qualified.io/kb/languages/php/phpunit>
  - Fixed the order of parameters

{% endcomment %}
