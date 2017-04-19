## Goals

- Easy to contribute
- Easy to maintain
- Easy to find


## Collections

### `languages`

Collection of general environment information for each supported language.

See [_languages/README.md](_languages/README.md) for details.

### `docs`

Collection of any types of documentations.

See [_docs/README.md](_docs/README.md) for details.


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


- Organize documents by topic/target audience
- Aggregate by language and add links to bottom of language page


## Known Issues

There're some syntax highlighting issues because Jekyll uses older version of Rouge.

- JavaScript issues with newer syntax
- F# not supported

It's possible to use client side syntax highlighters like
[Prism](http://prismjs.com/examples.html) by disabling Rouge if needed.
