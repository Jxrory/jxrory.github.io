# websocket 协议

```text
GET ws://localhost:3000/ws/chat HTTP/1.1
Host: localhost
Upgrade: websocket
Connection: Upgrade
Origin: http://localhost:3000
Sec-WebSocket-Key: client-random-string
Sec-WebSocket-Version: 13
```

该请求和普通的 HTTP 请求有几点不同：

- GET 请求的地址不是类似`/path/`，而是以`ws://`开头的地址；
- 请求头`Upgrade: websocket`和`Connection: Upgrade`表示这个连接将要被转换为 WebSocket 连接；
- `Sec-WebSocket-Key`是用于标识这个连接，并非用于加密数据；
- `Sec-WebSocket-Version`指定了 WebSocket 的协议版本。

服务器如果接受该请求:

```text
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: server-random-string
```

该响应代码`101`表示本次连接的`HTTP`协议即将被更改，更改后的协议就是`Upgrade: websocket`指定的 WebSocket 协议。

**为什么 WebSocket 连接可以实现全双工通信而 HTTP 连接不行呢？**

实际上 HTTP 协议是建立在 TCP 协议之上的，TCP 协议本身就实现了全双工通信，但是 HTTP 协议的请求－应答机制限制了全双工通信。WebSocket 连接建立以后，其实只是简单规定了一下：接下来，咱们通信就不使用 HTTP 协议了，直接互相发数据吧。

## 参考

- [廖雪峰的官方网站 - WebSocket](https://www.liaoxuefeng.com/wiki/1022910821149312/1103303693824096)
