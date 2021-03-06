multiplex-stream-muxer Node.js Implementation
=============================================

# DEPRECATED
## See [libp2p-multiplex](https://github.com/diasdavid/js-libp2p-multiplex) instead


---------------------------------------------------------------------------
---------------------------------------------------------------------------
---------------------------------------------------------------------------

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io) [[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs) ![Build Status](https://travis-ci.org/diasdavid/node-multiplex-stream-muxer.svg?style=flat-square)](https://travis-ci.org/diasdavid/node-multiplex-stream-muxer) ![](https://img.shields.io/badge/coverage-%3F-yellow.svg?style=flat-square) [![Dependency Status](https://david-dm.org/diasdavid/node-multiplex-stream-muxer.svg?style=flat-square)](https://david-dm.org/diasdavid/node-multiplex-stream-muxer) [![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/feross/standard)

> Abstraction on top of multiplex, implementing the abstract-stream-muxer interface

[![](https://github.com/diasdavid/abstract-stream-muxer/blob/master/img/badge.png)](https://github.com/diasdavid/abstract-stream-muxer)

# Usage

multiplex-stream-muxer follows the [abstract-stream-muxer API](https://github.com/diasdavid/abstract-stream-muxer#api)

# Example

```JavaScript
// Client.js
var MultiplexStreamMuxer = require('multiplex-stream-muxer')

var dialer = new MultiplexStreamMuxer()

var connDialer = dialer.attach(socket, false)

connDialer.dialStream(function (err, stream) {
  t.ifError(err, 'Should not throw')
  t.pass('dialed stream')
})
```

```JavaScript
// Server.js
var MultiplexStreamMuxer = require('multiplex-stream-muxer')

var listener = new MultiplexStreamMuxer()

var connListener = listener.attach(socket, true)

connListener.on('stream', function (stream) {
  t.pass('got stream')
})
```

You can also follow the net.connect pattern by listening to the `ready` and `error` events

```JavaScript
var stream = connListener.dialStream()

stream.on('ready', function () {})

stream.on('error', function (err) {})

stream.write('buffer this') // this write will be buffered untill the socket is ready to transmit
```
