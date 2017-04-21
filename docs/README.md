## Goals

- Easy to contribute
- Easy to maintain
- Easy to find


## Collections

### `languages`

Collection of general environment information for each supported language.

See [_languages/README.md](_languages/README.md) for details.

### `test_references`

Collection of test frameworks for each supported language.

See [_test_references/README.md](_test_references/README.md) for details.


### `references`

Collection of generic reference manuals.

See [_references/README.md](_references/README.md) for details.


### `tutorials`

Collection of documentations intended to teach/train users.

See [_tutorials/README.md](_tutorials/README.md) for details.


### `infos`

Collections of documents containing generic information.

See [_infos/README.md](_infos/README.md) for details.


## Development

### Bundler

```
bundle install
bundle exec jekyll serve --config _config.yml,_config_dev.yml
```

### Docker

```
docker run --rm --label=jekyll \
  --volume=$(pwd):/srv/jekyll \
  -it \
  -p 127.0.0.1:4000:4000 \
  jekyll/jekyll \
  jekyll serve --config _config.yml,_config_dev.yml
```

## TODO

- Reduce complexity
- Cleanup messy markups/hacks
- Contribution guide
- License
- Improve documentation
- Consider setting up CI for PR

### Styling

- Typography
- Colors
- Responsive
- Assets

### Navigation

- Obvious
- Visible
- Simple
- Consistent

- Links to Codewars/GitHub/Gitter
- Secondary breadcrumb navigation
- Support sequential navs where it makes sense (e.g., tutorials)


## Known Issues/Concerns

### Syntax Highlighting

There're some syntax highlighting issues because Jekyll uses older version of Rouge.

- JavaScript issues with newer syntax
- F# not supported

It's possible to use client side syntax highlighters like
[Prism](http://prismjs.com/examples.html) by disabling Rouge if needed.


### Directory Structure

The document root will be less cluttered by having `_collections/:collection-name`,
but Jekyll doesn't allow placing collections in subfolders.
