# gulp-json-modify

[![Build Status](https://travis-ci.org/olioex/gulp-json-modify.png?branch=master)](https://travis-ci.org/olioex/gulp-json-modify)

[![NPM version](https://badge.fury.io/js/gulp-json-modify.png)](http://badge.fury.io/js/gulp-json-modify)

> Replace data in a JSON file with something else

## Usage

#### Install

```bash
$ npm install gulp-json-modify --save
```

## Example

```js
var gulp = require('gulp')
var jsonModify = require('gulp-json-modify')

// Basic usage:
// Will patch the version
gulp.task('jsonModify', function(){
  gulp.src('./component.json')
  .pipe(jsonModify())
  .pipe(gulp.dest('./'))
})

// Defined method of updating:
// Semantic
gulp.task('jsonModify', function(){
  gulp.src('./*.json')
  .pipe(jsonModify({type:'minor'}))
  .pipe(gulp.dest('./'))
})

// Defined method of updating:
// Semantic major
gulp.task('jsonModify', function(){
  gulp.src('./bower.json')
  .pipe(jsonModify({type:'major'}))
  .pipe(gulp.dest('./'))
})

// Defined method of updating:
// Set a specific version
gulp.task('jsonModify', function(){
  gulp.src('./*.json')
  .pipe(jsonModify({version: '1.2.3'}))
  .pipe(gulp.dest('./'))
})

// Update bower, component, npm at once:
gulp.task('jsonModify', function(){
  gulp.src(['./bower.json', './component.json', './package.json'])
  .pipe(jsonModify({type:'major'}))
  .pipe(gulp.dest('./'))
})

// Override the tab size for indenting
// (or simply omit to keep the current formatting)
gulp.task('jsonModify', function(){
  gulp.src('./package.json')
  .pipe(jsonModify({ indent: 4 }))
  .pipe(gulp.dest('./'))
})

// Define the key for versioning off
gulp.task('jsonModify', function(){
  gulp.src('./package.json')
  .pipe(jsonModify({key: "appversion"}))
  .pipe(gulp.dest('./'))
})


```
#### jsonModifying version and outputting different files
```js
// `fs` is used instead of require to prevent caching in watch (require caches)
var fs = require('fs')
var semver = require('semver')

var getPackageJson = function () {
  return JSON.parse(fs.readFileSync('./package.json', 'utf8'))
}

// jsonModify data in multiple files
gulp.task('jsonModify', function () {

  return gulp.src(['./bower.json', './package.json', './src/manifest.json'])
    .pipe(tasks.jsonModify({
      key: 'version', value: '1.0.0'
    }))
    .pipe(manifestFilter)
    .pipe(gulp.dest('./src'))
    .pipe(manifestFilter.restore())
    .pipe(regularJsons)
    .pipe(gulp.dest('./'))
})

// Run the gulp tasks
gulp.task('default', function(){
  gulp.run('jsonModify')
})
```

####You can view more examples in the [example folder.](https://github.com/stevelacy/gulp-json-modify/tree/master/examples)

## Options

* **key**: key to replace (required)
* **value**: set to value (required)

Example:

```js
.pipe(jsonModify({ key: 'app_id', value: '1234' })
```

##### Dot notation is supported for sub-keys

```js

.pipe(jsonModify({ key: 'key.subkey', value: 'set-me-to' }))

/*
{
  "key": {
    "subkey": "<value>"
  }
}
*/
```

### options.indent

Set the amount of spaces for indentation in the result JSON file.

## /ht

https://github.com/stevelacy/gulp-bump

## LICENSE

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
