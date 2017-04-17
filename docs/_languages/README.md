# `environments`

Collection of general environment information for each supported language.

## Front Matter

```
---
title:     Title/Display Name
language:  Language tag
versions:  List of supported versions
tests:     List of supported test frameworks
packages:  List of installed packages
services:  List of services
timout:    String describing the allowed execution time
runner:    Docker image name
---
```

```
---
title:      JavaScript
language:   javascript
versions:   [Node v0.10.x, Node v0.10.x/Babel, Node v6.6.x, Node v6.6.x/Babel]
tests:      [Codewars, Mocha BDD, Mocha TDD]
packages:   [] # TODO
services:
  - sqlite3
  - redis
  - mongodb
timeout:    12000ms
runner:     codewars/node-runner
---
```

## Output

`/environments/:path/`

## Content

Any content is included in the output `/environments/:language/` using layout `_layouts/environment.html`.

