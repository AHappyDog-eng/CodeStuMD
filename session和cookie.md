### Session 和 Cookie 的作用

**Session**是一种无状态的协议 ， 我们用浏览器访问一个服务器 ， 每次都是**新**的请求**Session** 和 **Cookie**的作用就是为了弥补 http 的无状态的缺陷 可以记录用户的访问信息

### Session 是 什么？

**Session**是 客户端访问服务器之后 服务器开辟的一块小内存 ， 专门来储存用户**会话**期间的一些用户的操作

用户第一次访问的时候服务器会生成一个sessionId 来进行储存

接下来客户端每次向同一个网站发送请求时，请求头都会带上该 Cookie信息（包含 sessionId ）， 然后，服务器通过读取请求头中的 Cookie 信息，获取名称为 JSESSIONID 的值，得到此次请求的 sessionId。

**注意 sessionId 是靠cookie 来传送的** 如果禁用cookie session 也就没用了

### Cookie 的定义

**cookie** 储存在浏览器之中 ，相当于浏览器开辟的一块内存区域 大小不用的浏览器有不同的cookie空间

#### Cookie 包含 会话Cookie 和 永久的 Cookie

会话Cookie 意思代表 ， 在浏览器访问 客户端的时候 将会存储用户的访问信息 ， 会话cookie只存在于当前会话之中， 如果浏览器关闭 这次对服务器的 访问的话 ， cookie 会清除

永久的 cookie 不会清除 ， 可以设置**过期**的时间

Cookie的 **httpOnly** 代表 只能从浏览器中获取Cookie 如果 不开启httpOnly 会造成危险，比如黑客伪造身份 访问敏感资源 造成跨域攻击

### Cookie的作用域 

Domain 和 Path 两个属性 代表的是 Domain 代表那些主机可以接受Cookie 不指定doMain 默认 当前主机

