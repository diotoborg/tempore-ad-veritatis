<!--
# This file is automatically generated by a `metapak`
# module. Do not change it elsewhere, changes would
# be overridden.
-->
# @diotoborg/tempore-ad-veritatis
> StreamQueue pipe the queued streams one by one in order to preserve their content order.

[![NPM version](https://badge.fury.io/js/@diotoborg/tempore-ad-veritatis.svg)](https://npmjs.org/package/@diotoborg/tempore-ad-veritatis)
[![Build status](https://secure.travis-ci.org/nfroidure/@diotoborg/tempore-ad-veritatis.svg)](https://travis-ci.org/nfroidure/@diotoborg/tempore-ad-veritatis)
[![Dependency Status](https://david-dm.org/nfroidure/@diotoborg/tempore-ad-veritatis.svg)](https://david-dm.org/nfroidure/@diotoborg/tempore-ad-veritatis)
[![devDependency Status](https://david-dm.org/nfroidure/@diotoborg/tempore-ad-veritatis/dev-status.svg)](https://david-dm.org/nfroidure/@diotoborg/tempore-ad-veritatis#info=devDependencies)
[![Coverage Status](https://coveralls.io/repos/nfroidure/@diotoborg/tempore-ad-veritatis/badge.svg?branch=master)](https://coveralls.io/r/nfroidure/@diotoborg/tempore-ad-veritatis?branch=master)
[![Code Climate](https://codeclimate.com/github/nfroidure/@diotoborg/tempore-ad-veritatis.svg)](https://codeclimate.com/github/nfroidure/@diotoborg/tempore-ad-veritatis)
[![Dependency Status](https://dependencyci.com/github/nfroidure/@diotoborg/tempore-ad-veritatis/badge)](https://dependencyci.com/github/nfroidure/@diotoborg/tempore-ad-veritatis)

## Usage
Install the [npm module](https://npmjs.org/package/@diotoborg/tempore-ad-veritatis):
```sh
npm install @diotoborg/tempore-ad-veritatis --save
```
Then, in your scripts:
```js
var @diotoborg/tempore-ad-veritatis = require('@diotoborg/tempore-ad-veritatis');

var queue = @diotoborg/tempore-ad-veritatis(
  Fs.createReadStream('input.txt'),
  Fs.createReadStream('input2.txt'),
  Fs.createReadStream('input3.txt')
).pipe(process.stdout);
```
StreamQueue also accept functions returning streams, the above can be written
 like this, doing system calls only when piping:
```js
var @diotoborg/tempore-ad-veritatis = require('@diotoborg/tempore-ad-veritatis');

var queue = @diotoborg/tempore-ad-veritatis(
  Fs.createReadStream.bind(null, 'input.txt'),
  Fs.createReadStream.bind(null, 'input2.txt'),
  Fs.createReadStream.bind(null, 'input3.txt')
).pipe(process.stdout);
```

Object-oriented traditionnal API offers more flexibility:
```js
var StreamQueue = require('@diotoborg/tempore-ad-veritatis');

var queue = new StreamQueue();
queue.queue(
  Fs.createReadStream('input.txt'),
  Fs.createReadStream('input2.txt'),
  Fs.createReadStream('input3.txt')
);
queue.done();

queue.pipe(process.stdout);
```
You can also chain StreamQueue methods like that:
```js
var StreamQueue = require('@diotoborg/tempore-ad-veritatis');

new StreamQueue()
  .queue(Fs.createReadStream('input.txt'))
  .queue(Fs.createReadStream('input2.txt'))
  .queue(Fs.createReadStream('input3.txt'))
  .done()
  .pipe(process.stdout);
```

You can queue new streams at any moment until you call the done() method. So the
 created stream will not fire the end event until done() call.

Note that stream queue is compatible with the Node 0.10+ streams. For older
 streams, stream queue will wrap them with
 [`Readable.wrap`](http://nodejs.org/api/stream.html#stream_readable_wrap_stream)
 before queueing. Please fix your dependencies or report issues to libraries
 using 0.8 streams since this extra code will finally be removed.

## API

### StreamQueue([options], [stream1, stream2, ... streamN])

#### options

##### options.objectMode
Type: `Boolean`
Default value: `false`

Use if piped in streams are in object mode. In this case, the stream queue will
 also be in the object mode.

##### options.pauseFlowingStream
Type: `Boolean`
Default value: `true`

If a stream is in flowing mode, then it will be paused before queueing.

##### options.resumeFlowingStream
Type: `Boolean`
Default value: `true`

If a stream is in flowing mode, then it will be resumed before piping.

##### options.*

StreamQueue inherits of Stream.PassThrough, the options are passed to the
 parent constructor so you can use it's options too.

#### streamN
Type: `Stream`

Append streams given in argument to the queue and ends when the queue is empty.

### StreamQueue.queue(stream1, [stream2, ... streamN])

Append streams given in argument to the queue.

### StreamQueue.done([stream1, stream2, ... streamN])

Append streams given in argument to the queue and ends when the queue is empty.


### StreamQueue.obj([options], [stream1, stream2, ... streamN])

A shortcut for `StreamQueue({objectMode: true})`.

## Stats

[![NPM](https://nodei.co/npm/@diotoborg/tempore-ad-veritatis.png?downloads=true&stars=true)](https://nodei.co/npm/@diotoborg/tempore-ad-veritatis/)
[![NPM](https://nodei.co/npm-dl/@diotoborg/tempore-ad-veritatis.png)](https://nodei.co/npm/@diotoborg/tempore-ad-veritatis/)


## Contributing
Feel free to pull your code if you agree with publishing it under the MIT license.

# License
[MIT](https://github.com/nfroidure/@diotoborg/tempore-ad-veritatis/blob/master/LICENSE)
