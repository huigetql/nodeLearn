### Token的起源

在介绍基于`Token`的身份验证的原理与优势之前，不妨先看看**之前**的认证都是怎么做的。

- 基于服务器的验证

我们都是知道`HTTP`协议是无状态的，这种无状态意味着程序需要验证每一次请求，从而辨别客户端的身份。

在这之前，程序都是通过在服务端存储的登录信息来辨别请求的。这种方式一般都是通过存储`Session`来完成。

- 基于服务器验证方式暴露的一些问题

1.`Seesion`：每次认证用户发起请求时，服务器需要去创建一个记录来存储信息。当越来越多的用户发请求时，**内存**的开销也会不断增加。

2.可扩展性：在服务端的内存中使用`Seesion`存储登录信息，伴随而来的是可扩展性问题。

3.`CORS`(跨域资源共享)：当我们需要让数据跨多台移动设备上使用时，跨域资源的共享会是一个让人头疼的问题。在使用`Ajax`抓取另一个域的资源，就可以会出现禁止请求的情况。

4.`CSRF`(跨站请求伪造)：用户在访问银行网站时，他们很容易受到跨站请求伪造的攻击，并且能够被利用其访问其他的网站。

在这些问题中，可扩展行是最突出的。因此我们有必要去寻求一种更有行之有效的方法。

### 基于Token的验证原理

基于Token的身份验证是**无状态**的，我们**不将**用户信息存在服务器中。这种概念解决了在服务端存储信息时的许多问题。`NoSession`意味着你的程序可以根据需要去增减机器，而不用去担心用户是否登录。

### 基于Token的身份验证的过程如下:

1. 用户通过用户名和密码发送请求。
2. 服务器端程序验证。

   3.服务器端程序返回一个**带签名**的`token` 给客户端。

   4.客户端储存`token`,并且每次访问`API`都携带`Token`到服务器端的。

   5.服务端验证`token`，校验成功则返回请求数据，校验失败则返回错误码。

### 基本操作

1. 安装

   ```
   npm install jsonwebtoken;
   ```

2. 使用加密

   ```javascript
   const jwt = require("jsonwebtoken");
   let token = jwt.sign(payload,secretOrPrivateKey,[options,fn])
   /*
   	payload : 有效载荷,可为对象、buffer、有效json字符串
   	secretOrPrivateKey : 私钥，可为字符串、buffer、object
   	options : 
   		algorithm : 加密算法
   		expiresIn : 表示有效期 不带单位默认为秒  如带单位如: "2 days", "10h", "7d"
   		······· 还有一些无关紧要请看文档
   */
   ```

   


### 项目中使用token总结

使用基于 `Token` 的身份验证方法，在服务端**不需要**存储用户的登录记录。大概的流程是这样的：

1.前端使用用户名跟密码请求首次登录

2.后服务端收到请求，去验证用户名与密码是否正确

3.验证成功后，服务端会根据用户`id`、用户名、定义好的秘钥、过期时间生成一个 `Token`，再把这个 `Token` 发送给前端

4.前端收到 返回的`Token` ，把它存储起来，比如放在 `Cookie` 里或者 `Local Storage` 里

5.前端每次路由跳转，判断 `localStroage` 有无 `token` ，没有则跳转到登录页。有则请求获取用户信息，改变登录状态；

6.前端每次向服务端请求资源的时候需要在**请求头**里携带服务端签发的`Token`

7.服务端收到请求，然后去验证前端请求里面带着的 `Token`。没有或者 `token` 过期，返回`401`。如果验证成功，就向前端返回请求的数据。

8.前端得到 `401` 状态码，重定向到登录页面。