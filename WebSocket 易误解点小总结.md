# WebSocket 易误解点小总结

> 为避免以讹传讹的事情发生，以下内容均出自RFC6455(WebSocket协议标准文档)、WebSocket.org、Mozilla Developer Network。每部分都会附带原文和我简单地认识/讲解。

RFC6455文档地址：[https://tools.ietf.org/html/rfc6455](https://tools.ietf.org/html/rfc6455)

## 定义

阅读之前，你需要先搞明白以下几个关键术语。

- 长连接
- 短连接
- Socket
- TCP

## WebSocket出现的意义
-  Historically, creating web applications that need bidirectional
   communication between a client and a server (e.g., instant messaging
   and gaming applications) has required an abuse of HTTP to poll the
   server for updates while sending upstream notifications as distinct
   HTTP calls.
   
   > 我们知道Http是一种无状态的连接，所以无法直接借助Http来实现服务器和客户端的双向通信，但通过轮询(poll)的方式也能间接的实现了伪双向通信。之前使用的comet技术就是依据类似的原理（准确说是long-poll长轮询，相比一般的轮询，服务端会保持请求处于更长的一段时间直至超时）实现的一套双向通信技术。但缺点也很明显，自己去查缺点。
 
-  A simpler solution would be to use a single TCP connection for
   traffic in both directions.  This is what the WebSocket Protocol
   provides. 
   
   > 初步说明了WebSocket使用的单一的TCP连接建立起来的双向通信，这个跟Socket通信很像，所以顾名思义跟WebSocket最接近的技术应该是Socket。

-  The WebSocket Protocol is designed to supersede existing
   bidirectional communication technologies that use HTTP as a transport
   layer to benefit from existing infrastructure (proxies, filtering,
   authentication).
   
   > 我觉得有人认为WebSocket建立于HTTP基础上是不是误解了这句话的意思？这句话的意思分明是"WebSocket协议是为了取代那些现有的使用HTTP作为传输介质的双向通信技术"，而不是"WebSocket协议是使用了HTTP作为传输介质的双向通信技术"......所以说请不要相信很多渣渣翻译，看标准文档才是唯一出路。
   
## WebSocket架构
-  The protocol has two parts: a handshake and the data transfer.

   The handshake from the client looks as follows:

        GET /chat HTTP/1.1
        Host: server.example.com
        Upgrade: websocket
        Connection: Upgrade
        Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
        Origin: http://example.com
        Sec-WebSocket-Protocol: chat, superchat
        Sec-WebSocket-Version: 13

   The handshake from the server looks as follows:

        HTTP/1.1 101 Switching Protocols
        Upgrade: websocket
        Connection: Upgrade
        Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
        Sec-WebSocket-Protocol: chat
        
   Once the client and server have both sent their handshakes, and if
   the handshake was successful, then the data transfer part starts.
   This is a two-way communication channel where each side can,
   independently from the other, send data at will.
   
   > 协议由两部分组成，一个是握手，一个是数据传输。上面展示了握手的交互过程，确实借助了普通的Http协议来实现握手的过程，但是整个WebSocket连接所要传输的数据是需要借助建立起来的管道来传输，而非Http协议。


## WebSocket与TCP、HTTP的关系
-  The WebSocket Protocol is an independent TCP-based protocol.  Its
   only relationship to HTTP is that its handshake is interpreted by
   HTTP servers as an Upgrade request.

   By default, the WebSocket Protocol uses port 80 for regular WebSocket
   connections and port 443 for WebSocket connections tunneled over
   Transport Layer Security (TLS)   
	
	> 这里是文档原文写的，非常清楚了。跟HTTP的关系就开始一个握手，其他一点关系都没有。所以如果要封装或者使用WebSocket，其原理跟Socket基本一样的。
	
	
	
	时间不早了，今晚上的WebSocket与Http关系之争已经有结论了。后续更多关于WebSocket的使用研究就需要在实践中得真知了。欢迎大家一起来讨论！Σ(っ °Д °;)っ