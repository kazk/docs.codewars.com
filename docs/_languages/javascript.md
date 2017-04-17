---
title:    JavaScript
language: javascript
versions: [Node v0.10.x, Node v6.6.x]
tests:    [Codewars, Mocha BDD, Mocha TDD]

packages: [] # TODO

services:
  - sqlite3
  - redis
  - mongodb

timeout: 12000ms

runner: codewars/node-runner
---

{% include environment-overview.html language=page.language %}

