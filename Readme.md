# Socket.IO RedisStore

Socket.io RedisStore is a remote persistent key/value storage engine for Socket.io as well as an inter-process dispatch layer for Socket.io servers. RedisStore uses Redis Pub/Sub to distribute Socket.io framed messages to the connected Socket.io servers.

### Use it:

(requires socket.io >= 0.8.5):

```javascript
var sio = require('socket.io')
  , RedisStore = sio.RedisStore
  , io = sio.listen()

io.configure(function () {
  io.set('store', new RedisStore)
})
```

### Persist it:

```javascript
io.sockets.on('connection', function(socket) {
  var nick = 'dshaw'
  socket.set('nickname', nick, function() {
    socket.emit('nickname', nick)
  })
})
```

### Scale it:

Point all socket.io processes and server instances at the same Redis server.

```javascript
io.configure(function () {
  io.set('store', new RedisStore({ host: 'http://redis.example.com' }))
})
```

### Extend it:

Want to implement your own dispatch layer, but Redis for your key/value store? Totally doable. In fact, that is exactly what `socket.io-zero` does. Zero provides a ZeroMQ-based dispatch layer, then uses RedisStores "storage" implementation.

Example: https://github.com/dshaw/socket.io-zero

### Resources:
  - [redis.io](https://redis.io)
  - [socket.io](http://socket.io/)
  - [socket.io mailing list](http://groups.google.com/group/socket_io)
  - [#socket.io on freenode.net](http://webchat.freenode.net?channels=socket.io&uio=d4)
