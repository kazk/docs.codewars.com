---
title: Mocha
language: javascript
---

# {{ page.title }}

Codewars supports [Mocha](http://mochajs.org/) testing framework in BDD and TDD interfaces.

## Interfaces

### Mocha BDD

BDD interface provides `describe()`, `context()`, `it()`, `specify()`, `before()`, `after()`, `beforeEach()`, and `afterEach()`:

```javascript
const assert = require("assert");
describe('Array', function() {
  before(function() {
    // ...
  });

  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      assert.equal(-1, [1,2,3].indexOf(5));
    });
  });
});
```

### Mocha TDD

TDD interface provides `suite()`, `test()`, `suiteSetup()`, `suiteTeardown()`, `setup()`, and `teardown()`:

```javascript
const assert = require("assert");
suite('Array', function() {
  setup(function() {
    // ...
  });

  suite('#indexOf()', function() {
    test('should return -1 when not present', function() {
      assert.equal(-1, [1,2,3].indexOf(5));
    });
  });
});
```

## Assertions

Mocha allows you to use any assertion library you want and so does not auto-require a certain library for you by default.

### Chai

We recommend that you use the [Chai](http://chaijs.com) BDD/TDD assertion library.
It supports the following assertion styles:

#### Should

```javascript
require("chai").should();

foo.should.be.a('string');
foo.should.equal('bar');
foo.should.have.length(3);
tea.should.have.property('flavors').with.length(3);
```

#### Expect

```javascript
var expect = require("chai").expect;

expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.length(3);
expect(tea).to.have.property('flavors').with.length(3);
```

#### Assert

```javascript
var assert = require("chai").assert;

assert.typeOf(foo, 'string');
assert.equal(foo, 'bar');
assert.lengthOf(foo, 3)
assert.property(tea, 'flavors');
assert.lengthOf(tea.flavors, 3);
```

## NPM Packages

The following test related packages are available:

* should
* expect
* chai
* chai-spies
* chai-stats
* chai-factories
* chai-things
* chai-fuzzy
* chai-interface
* chai-change
* chai-subset

{% comment %}

- <https://www.qualified.io/kb/languages/javascript/mocha_bdd>
- <https://www.qualified.io/kb/languages/javascript/mocha_tdd>

- Fixed broken link to Chai

{% endcomment %}
