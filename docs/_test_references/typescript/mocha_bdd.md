---
title: Mocha Testing Framework (BDD)
language: typescript
---

# Mocha Testing Framework (BDD)

Codewars supports the Mocha testing framework, in a BDD or TDD setup.

The following is a Mocha BDD example on how to use the framework using the built in Node.js assertion library:

```typescript
/// <reference path="/runner/typings/node/index.d.ts" />
/// <reference path="/runner/typings/mocha/index.d.ts" />
/// <reference path="/runner/typings/chai/index.d.ts" />
import solution = require('./solution')
// import the type of assertion library you wish to use (Chai recommended)
import {assert} from "chai";

describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      assert.equal(-1, [1,2,3].indexOf(5));
      assert.equal(-1, [1,2,3].indexOf(0));
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

```typescript
require("chai").should();

foo.should.be.a('string');
foo.should.equal('bar');
foo.should.have.length(3);
tea.should.have.property('flavors').with.length(3);
```

#### Expect

```typescript
var expect = require("chai").expect;

expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.length(3);
expect(tea).to.have.property('flavors').with.length(3);
```

#### Assert

```typescript
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

- <https://www.qualified.io/kb/languages/typescript/mocha_bdd>

- Fixed the broken link to Chai

- Should fix examples:
  - Node.js `assert` not used in the first example
  - Use TypeScript syntax in assertion style examples

```typescript
import { should } from 'chai';
should();
```

```typescript
import { expect } from 'chai';
```

```typescript
import { assert } from 'chai';
```

{% endcomment %}
