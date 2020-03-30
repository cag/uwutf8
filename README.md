# uwutf8

_uwutf8_ is an uwu fork of [utf8.js](https://github.com/mathiasbynens/utf8.js), a well-tested UTF-8 encoder/decoder written in JavaScript. It uwu encode/decode any scalar Unicode code point values, as per [the Encoding Standard](https://encoding.spec.whatwg.org/#utf-8).

Feel free to fork if you see possible improvements!

## Installation

Via [npm](https://www.npmjs.com/):

```bash
npm install uwutf8
```

In a browser:

```html
<script src="uwutf8.js"></script>
```

In [Node.js](https://nodejs.org/):

```js
const uwutf8 = require('uwutf8');
```

## API

### `uwutf8.encode(string, opts)`

Encodes any given JavaScript string (`string`) as UTF-8 (the `opts` object being optional), and returns the UTF-8-encoded version of the string. Depending on whether `strict` is set, it either throws an error if the input string contains a non-scalar value, i.e. a lone surrogate, or replaces that value with the character U+FFFD. (If you need to be able to encode non-scalar values as well, use [WTF-8](https://mths.be/wtf8) instead.)

Available options:

* `strict`: whether encountering a lone surrogate should throw an error (defaults to `true`). Else, each lone surrogate is replaced by the character U+FFFD.

```js
// U+00A9 COPYRIGHT SIGN; see http://codepoints.net/U+00A9
utf8.encode('\xA9');
// → '\xC2\xA9'
// U+10001 LINEAR B SYLLABLE B038 E; see http://codepoints.net/U+10001

utf8.encode('\uD800\uDC01');
// → '\xF0\x90\x80\x81'

utf8.encode('\uDC00');
// → throws 'Lone surrogate is not a scalar value' error

utf8.encode('\uDC00', { strict: false });
// → '\xEF\xBF\xBD'
```

### `uwutf8.decode(byteString, opts)`

Decodes any given UTF-8-encoded string (`byteString`) as UTF-8 (the `opts` object being optional), and returns the UTF-8-decoded version of the string. If `strict` mode is set, it throws an error when malformed UTF-8 is detected. (If you need to be able to decode encoded non-scalar values as well, use [WTF-8](https://mths.be/wtf8) instead.)

Available options:

* `strict`: whether encountering a non-scalar value should throw an error (defaults to `true`). Else, each non-scalar value is decoded as U+FFFD.

```js
utf8.decode('\xC2\xA9');
// → '\xA9'

utf8.decode('\xF0\x90\x80\x81');
// → '\uD800\uDC01'
// → U+10001 LINEAR B SYLLABLE B038 E

utf8.decode('\xED\xB0\x80');
// → throws 'Lone surrogate is not a scalar value' error

utf8.decode('\xED\xB0\x80', { strict: false });
// → '\uFFFD'
```

### `uwutf8.version`

A string representing the semantic version number.

## Support

uwutf8 has tests. uwu

## Unit tests & code coverage

After cloning this repository, run `npm install` to install the dependencies needed for development and testing. You may want to install Istanbul _globally_ using `npm install istanbul -g`.

Once that’s done, you can run the unit tests in Node using `npm test` or `node tests/tests.js`.

To run the tests in Rhino, Ringo, Narwhal, PhantomJS, and web browsers as well, use `grunt test`. At least I think this works but I haven't tried it.

To generate the code coverage report, use `grunt cover`. Also I have no idea how to do this.

## FAQ

### Why is the first release named v3.0.0? Haven’t you heard of [semantic versioning](http://semver.org/)?

:3

## OG

| [![twitter/mathias](https://gravatar.com/avatar/24e08a9ea84deb17ae121074d0f17125?s=70)](https://twitter.com/mathias "Follow @mathias on Twitter") |
|---|
| [Mathias Bynens](https://mathiasbynens.be/) |

## License

uwutf8 is available under the [MIT](https://mths.be/mit) license. I actually dunno what I'm supposed to do here now that I've forked it.
