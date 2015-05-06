# MapStream
[![Build Status](http://img.shields.io/travis/dominictarr/map-stream.svg?style=flat-square)](https://travis-ci.org/dominictarr/map-stream) [![NPM version](http://img.shields.io/npm/v/map-stream.svg?style=flat-square)](https://www.npmjs.org/package/map-stream) [![NPM license](http://img.shields.io/npm/l/map-stream.svg?style=flat-square)](https://www.npmjs.org/package/map-stream)

Refactored out of [event-stream](https://github.com/dominictarr/event-stream)

## map (asyncFunction[, options])
Create a through stream from an asynchronous function.

```js
var map = require('map-stream')

map(function (data, callback) {
  //transform data
  // ...
  callback(null, data)
})
```

Each map MUST call the callback. It may callback with data, with an error or with no arguments,
- `callback()` drop this data. this makes the map work like `filter`, note:`callback(null,null)` is not the same, and will emit `null`
- `callback(null, newData)` turn data into newData
- `callback(error)` emit an error for this item.

> Note: if a callback is not called, `map` will think that it is still being processed, every call must be answered or the stream will not know when to end.

> Also, if the callback is called more than once, every call but the first will be ignored.

## Options
- `failures` - `boolean` continue mapping even if error occurred. On error `map-stream` will emit `failure` event. (default: `false`)
