### 一、特点

服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于服务器推送技术的一种。

![](https://cdn.nlark.com/yuque/0/2021/png/1810272/1618195323781-6a68de14-9a6e-43f3-ab81-df814e448e66.png)

其他特点：

-   建立在 TCP 协议上，服务端实现简单
-   与 HTTP 协议有良好的兼容性。默认端口 80 和 443 ，握手阶段采用 HTTP 协议。

-   数据格式比较轻量，性能开销小，通信高效
-   可以发送文本、二进制数据

-   **没有同源策略**，客户端可以与任意服务器通信
-   协议标识符是 ws, 加密 wss , 服务器网址就是 URL
``` bash
ws://example.com:80/some/path
```

---
### 二、示例
```js
var ws = new WebSocket("wss://echo.websocket.org");

// 用于指定连接成功后的回调函数。
ws.onopen = function(evt) { 
  console.log("Connection open ..."); 
  ws.send("Hello WebSockets!");
};

// 用于指定当从服务器接受到信息时的回调函数。
ws.onmessage = function(evt) {
  console.log( "Received Message: " + evt.data);
  ws.close();
};

// 用于指定连接关闭后的回调函数。
ws.onclose = function(evt) {
  console.log("Connection closed.");
};  
```

[链接](https://jsbin.com/muqamiqimu/edit?js,console)

  ---
### 三、主要API 介绍


[链接](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket)

  
---
### 四、维持 websocket 连接机制- ping pong


- ** 是什么？**

有时，由于网络等原因，实际上双方已经断开了，但服务端和客户端双方并不知情，导致服务端还将为客户端发送多余消息，并且这些消息包会丢失。所以需要一种机制检测双方是连接状态。需要服务端跟客户端共同实现。

  
- **实现方法-心跳机制**

心跳机制是每隔一段时间会向服务器发送一个数据包，告诉服务器自己还活着，同时客户端会确认服务器端是否还活着，如果还活着的话，就会回传一个数据包给客户端来确定服务器端也还活着，否则的话，有可能是网络断开连接了。需要重连~


- **见代码**

[https://code.geekbang.org/fe/live.geekbang.org/-/blob/prod/src/utils/websocket.js](https://code.geekbang.org/fe/live.geekbang.org/-/blob/prod/src/utils/websocket.js)

- **断线重连机制【业务规定】**

	-   6次内：重连时间间隔 2的n方*1000 ms
	-   超过6次：间隔64s

	-   总次数不得超过10次
---
### 五、其他注意事项

-   cookie 在 wx 协议下谷歌浏览器下不显示，实际上已经传过去了