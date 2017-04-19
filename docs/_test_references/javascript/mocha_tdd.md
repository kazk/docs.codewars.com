---
title: Mocha Testing Framework (TDD)
language: javascript
---

# Mocha Testing Framework (TDD)

Codewars supports the Mocha testing framework, in a BDD or TDD setup.

The following is a Mocha TDD example on how to use the framework using the built in Node.js assertion library:

```javascript
var assert = require("assert");
suite('Array', function() {
  setup(function() {
    // ...
  });

  suite('#indexOf()', function() {
    test('should return -1 when not present', function() {
      assert.equal(-1, [1,2,3].indexOf(4));
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

The following test related packages are loaded into the VM and available for use:

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

## Learn More

You can learn more on the [Mocha website](http://mochajs.org/).



{% comment %}

- <https://www.qualified.io/kb/languages/javascript/mocha_tdd>

- Fixed broken link to chai

{% endcomment %}
