# gulp-json-modify

[![CI](https://github.com/OLIOEX/gulp-json-modify/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/OLIOEX/gulp-json-modify/actions/workflows/ci.yml)
[![npm version](https://img.shields.io/npm/v/gulp-json-modify.svg)](https://www.npmjs.com/package/gulp-json-modify)

> Modify a value in a JSON file using [gulp](https://gulpjs.com)

## Install

Requires Node.js 20 or later.

```bash
npm install --save-dev gulp-json-modify
```

## Usage

```js
const { src, dest } = require('gulp')
const jsonModify = require('gulp-json-modify')

function setVersion() {
  return src(['./bower.json', './package.json'])
    .pipe(jsonModify({
      key: 'version',
      value: '1.0.0'
    }))
    .pipe(dest('./'))
}

exports.default = setVersion
```

## Options

### key

Type: `string` (required)

The key to set. Use dot notation to set nested keys:

```js
.pipe(jsonModify({ key: 'key.subkey', value: 'set-me-to' }))

/*
{
  "key": {
    "subkey": "set-me-to"
  }
}
*/
```

Missing intermediate objects are created.

### value

Type: any JSON-serialisable value (required)

The value to set. Falsy values such as `false`, `0` and `''` are allowed; only `undefined` is rejected.

### indent

Type: `number | string`

The indentation passed to `JSON.stringify`. By default, the plugin detects the indentation already used in the file (tabs or spaces) and keeps it. A trailing newline is also kept if the file had one.

## Releasing

Releases are published to npm by GitHub Actions ([`publish.yml`](.github/workflows/publish.yml)) using npm trusted publishing.

1. Bump the version and tag it: `npm version patch` (or `minor` / `major`)
2. Push the commit and tag: `git push --follow-tags`
3. Create a GitHub Release from the new `vX.Y.Z` tag. Publishing the release triggers the npm publish.

The workflow fails if the release tag does not match the version in `package.json`.

## Credits

Based on [gulp-bump](https://github.com/stevelacy/gulp-bump).

## License

(MIT License)

Copyright (c) 2015 Steve Lacy <me@slacy.me> slacy.me

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
