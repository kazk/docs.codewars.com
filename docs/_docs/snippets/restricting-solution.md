---
title:    Restricting Solution
category: snippets
tags:
  - examples
  - test
---

## Problem

Often times kata authors want to prevent certain code from being used within a kata, to increase the level of difficulty.

## Solution

Validate submitted solution by reading `solution.txt`.

## Examples

### JavaScript

by @jhoffner ([src](https://www.codewars.com/kumite/579d80d97cb1f385ed000231?sel=579d80d97cb1f385ed000231))

#### Code

```javascript
// write a add function that doesn't use the plus symbol
function add(a, b) {
  return a + b;
}

// Make sure to view the test cases to see how this test fails
```

#### Test Cases

```javascript
const fs = require('fs');
const solution = fs.readFileSync('/home/codewarrior/solution.txt', 'utf8');

describe("Check Solution", function() {
  it("should prevent the '+' symbol from being used anywhere in the code", function() {
    Test.expect(solution.indexOf('+') == -1, "Your code isn't allowed to include the + symbol!");
  });
});
```

### Ruby

by @10XL ([src](https://www.codewars.com/kumite/579d80d97cb1f385ed000231?sel=58c3fec98b4f2e7e0e000138))

#### Code

```ruby
# write a add function that doesn't use the plus symbol
def add(a, b)
  a + b
end

# Make sure to view the test cases to see how this test fails
```

#### Test Cases

```ruby
solution = File.open('/home/codewarrior/solution.txt', 'r').read

describe "Check Solution" do
 it "should prevent the '+' symbol from being used anywhere in the code" do
   Test.expect(solution.exclude?('+'), "Your code isn't allowed to include the + symbol!")
 end
end
```

### PHP

by @donaldsebleung ([src](https://www.codewars.com/kumite/579d80d97cb1f385ed000231?sel=58c67d4c6aed00e7120001b6))

#### Code

```php?start_inline=true
// TODO: Write a function that doesn't use the add symbol
function add($a, $b) {
  return $a + $b;
}

// Make sure to view the test cases to see how this test fails
```

#### Test Cases

```php?start_inline=true
class AddWithoutAdditionSignTest extends TestCase {
  public function testThatAddFunctionDoesNotUseAdditionSign() {
    // Open the text file containing the user solution code and read the entire file
    $user_solution_source_code = fread(fopen('/home/codewarrior/solution.txt', 'r'), filesize('/home/codewarrior/solution.txt'));
    // Print user solution code onto the console (just to show that it works)
    echo $user_solution_source_code . "\r\n";
    // Use a regular expression to test for the (forbidden) '+' symbol in the user solution
    $this->assertNotRegExp('/\+/', $user_solution_source_code, "Your solution musn't contain the '+' symbol!");
  }
}
```


## Discussion

The above method fails if the user's solution modifies the `soltion.txt`.

A possible workaround is to read `solution.txt` in preloaded section so the user's solution is read before it's modified.

### JavaScript

by @10XL ([src](https://www.codewars.com/kumite/579d80d97cb1f385ed000231?sel=58e0f03292d04c7805000012))

#### Preloaded Code

```javascript
const realSolution = require('fs').readFileSync('/home/codewarrior/solution.txt', 'utf8');
```

#### Code

```javascript
// write a add function that doesn't use the plus symbol
function add(a, b) {
  return a + b;
}

// Make sure to view the test cases to see how this test fails
// Rewrite solution.txt
require('fs').writeFileSync('/home/codewarrior/solution.txt', 'no pluses here!')
```

#### Test Cases

```javascript
const fs = require('fs');
const solution = fs.readFileSync('/home/codewarrior/solution.txt', 'utf8');

describe("Check Solution", function() {
  it("should prevent the '+' symbol from being used anywhere in the code", function() {
    Test.expect(solution.indexOf('+') == -1, "Your code isn't allowed to include the + symbol!");
  });
});

describe("Check Real Solution", function() {
  it("should prevent the '+' symbol from being used anywhere in the code", function() {
    Test.expect(realSolution.indexOf('+') == -1, "Your code isn't allowed to include the + symbol!");
  });
});
```
