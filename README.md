# \<async-script\> [WIP]

[![Build Status](https://travis-ci.org/TheProfs/async-script.svg?branch=master)](https://travis-ci.org/TheProfs/async-script)

Asynchronously load scripts that survive vulcanisation/bundling.

## Usage

### Basic

In the below example, `testLib` will be loaded *after* the element is attached,
regardless if this element was vulcanised/bundled.

In short, the `src` is not included in any bundles.

```html
<async-script src="/lib/test-lib.js"></async-script>
```

**Important:** All non-`http`/`https` scripts are passed through
[`this.resolveUrl()`][resolve-url] to resolve their relative path.

### Multiple scripts

You can provide multiple `src`'s by separating them with a comma.

```html
<async-script src="/lib/foo.js, /lib/bar.js"></async-script>
```

### Non-local scripts

Providing an `src` that includes `http`/`https` will not attempt to resolve it
relatively(i.e using `this.resolveUrl(src)`), therefore keeping it intact.

```html
<async-script src="http://foo-cdn.com/foo-lib.js"></async-script>
```

### Status Events

The element will fire `load`/`error` events where appropriate:

```javascript

// Success, all srcs have loaded
document.querySelector('async-script').addEventListener('load', () => {
  console.log('loaded')
})

// Error, at least 1 src has failed to load
document.querySelector('async-script').addEventListener('error', e => {
  console.error(e.detail)
})
```

## Tests

```
$ polymer test
```

## Authors

- [The Profs][the-profs]

## License

MIT License

[resolve-url]: https://www.polymer-project.org/1.0/docs/api/Polymer.Base#method-resolveUrl
[the-profs]: https://github.com/TheProfs
