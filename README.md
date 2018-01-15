# \<defer-script\> [WIP]

[![Build Status](https://travis-ci.org/TheProfs/defer-script.svg?branch=master)](https://travis-ci.org/TheProfs/defer-script)

Load deferred scripts that survive vulcanisation/bundling.

## Usage

```bash
$ bower install --save defer-script
```

### Basic

In the below example, `testLib` will be loaded *after* the element is attached,
regardless if this element was vulcanised/bundled.

In short, the `src` is not included in any bundles.

```html
<defer-script src="/lib/test-lib.js"></defer-script>
```

**Important:** All non-`http`/`https` scripts are passed through
[`this.resolveUrl()`][resolve-url] to resolve their relative path.

### Multiple scripts

You can provide multiple `src`'s by separating them with a comma.

```html
<defer-script src="/lib/foo.js, /lib/bar.js"></defer-script>
```

### Non-local scripts

Providing an `src` that includes `http`/`https` will not attempt to resolve it
relatively(i.e using `this.resolveUrl(src)`), therefore keeping it intact.

```html
<defer-script src="http://foo-cdn.com/foo-lib.js"></defer-script>
```

### Checking load status

When all `src`s have loaded successfully, a `loaded` attribute will be added
to the element.

```html
<defer-script src="/lib/foo.js, /lib/bar.js" loaded></defer-script>
```

The element will also fire `load`/`error` events where appropriate:

```javascript

// Success, all srcs have loaded
document.querySelector('defer-script').addEventListener('load', () => {
  console.log('loaded')
})

// Error, at least 1 src has failed to load
document.querySelector('defer-script').addEventListener('error', e => {
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
