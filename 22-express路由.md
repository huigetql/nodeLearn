## Express路由

#### 简介

路由表示应用程序端点的定义已经响应客户端请求的方式。他包含一个请求方式（methods）、一个路径（path）和路由匹配时返回的函数（callback）

```
app.methods(patth,callback)
```

#### 路由方法

get、post、put、head、delete、options、trace、copy、lock、mkcol、move、purge、propfind、proppatch、unlock、report、mkactivity、checkout、merge、m-search、notify、subscribe、unsubscribe、patch、search 和 connect。

常用为get 和 post

#### 路径

​	**1.字符串路径**

```
app.get("/login",(req,res)=>{})
```

此路径地址将与/login匹配

​	**2.字符串模式路径（类正则）**

```
app.get('/ab?cd',(req,res)=>{})
```

此路径将与abcd、acd匹配  ?在正则中表示0或者1，即有或者没有

```
app.get('/ab*cd',(req,res)=>{})
```

此路径将与abcd、abefcd、abNOTREGcd匹配  *在正则中表示0或者1，即有或者没有，但在这里需要注意的是，\*表示匹配**任意、多个**字符

```
app.get('/ab+cd',(req,res)=>{})
```

此路径将与abcd、abbcd、abb····cd匹配  +在正则中表示[1,?]，即至少一个

​	**3.正则路径**

```
app.get(/a/,(req,res)=>{})
```

此路径匹配带a的内容

#### 基础路由

```
const express = require("express");
var app = express();

app.get("/",function(req,res){
	res.send(`<h1>主页</h1>`);
});
app.get("/login",function(req,res){
	res.send(“登录页面”);
});
app.get("/registe",function(req,res){
	res.send(“注册页面”);
});

app.listen(8080);
```

#### 动态路由

​	**路由参数**

路由参数被命名为URL段，用于捕获URL中在其位置处指定的值。捕获的值将填充到`req.params`对象中，并将路径中指定的route参数的名称作为其各自的键。

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

要使用路由参数定义路由，只需在路由路径中指定路由参数，如下所示。

```javascript
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params)
})
```

路径参数的名称必须由“文字字符”（[A-Za-z0-9_]）组成。

由于连字符（`-`）和点（`.`）是按字面解释的，因此可以将它们与路由参数一起使用，以实现有用的目的。

```
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }
Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
```

要更好地控制可以由route参数匹配的确切字符串，可以在括号（`()`）后面附加一个正则表达式：

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

由于正则表达式通常是文字字符串的一部分，因此请确保`\`使用其他反斜杠对所有字符进行转义，例如`\\d+`。

在Express 4.x中，[不以常规方式解释正则表达式中](https://github.com/expressjs/express/issues/2495)[的`*`字符](https://github.com/expressjs/express/issues/2495)。解决方法是使用`{0,}`代替`*`。这可能会在Express 5中修复。

#### 路线处理程序

可用多个回调函数来处理请求，但必须确保这些回调函数会调用next()方法

路由处理程序可以采用函数，函数数组或二者组合的形式。

多个回调函数可以处理一条路由（确保指定了`next`对象）。例如：

```javascript
app.get('/example/b', function (req, res, next) {
  console.log('the response will be sent by the next function ...')
  next()
}, function (req, res) {
  res.send('Hello from B!')
})
```

回调函数数组可以处理路由。例如：

```javascript
var cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

var cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/c', [cb0, cb1])
```

独立功能和功能数组的组合可以处理路由。例如：

```
var cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

var cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/d', [cb0, cb1], function (req, res, next) {
  next()
}, function (req, res) {
  res.send('Hello from D!')
})
```

## 应对方法

`res`下表中响应对象（）上的方法可以将响应发送到客户端，并终止请求-响应周期。如果从路由处理程序中未调用这些方法，则客户端请求将被挂起。

| 方法                                                         | 描述                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [res.download()](http://www.expressjs.com.cn/en/4x/api.html#res.download) | 提示要下载的文件。                                     |
| [res.end（）](http://www.expressjs.com.cn/en/4x/api.html#res.end) | 结束响应过程。                                         |
| [res.json（）](http://www.expressjs.com.cn/en/4x/api.html#res.json) | 发送JSON响应。                                         |
| [res.jsonp（）](http://www.expressjs.com.cn/en/4x/api.html#res.jsonp) | 发送带有JSONP支持的JSON响应。                          |
| [res.redirect（）](http://www.expressjs.com.cn/en/4x/api.html#res.redirect) | 重定向请求。                                           |
| [res.render（）](http://www.expressjs.com.cn/en/4x/api.html#res.render) | 渲染视图模板。                                         |
| [res.send（）](http://www.expressjs.com.cn/en/4x/api.html#res.send) | 发送各种类型的响应。                                   |
| [res.sendFile（）](http://www.expressjs.com.cn/en/4x/api.html#res.sendFile) | 将文件作为八位字节流发送。                             |
| [res.sendStatus（）](http://www.expressjs.com.cn/en/4x/api.html#res.sendStatus) | 设置响应状态代码，并将其字符串表示形式发送为响应正文。 |

#### app.route ()

用来为路由路径创建可链式调用的路由处理程序`app.route()`

这是使用定义的链式路由处理程序的示例`app.route()`。

```javascript
app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  })
```

## 快速路由器

使用`express.Router`该类创建模块化的，可安装的路由处理程序。一个`Router`实例是一个完整的中间件和路由系统; 因此，它通常被称为“迷你应用程序”。

以下示例将路由器创建为模块，在其中加载中间件功能，定义一些路由，并将路由器模块安装在主应用程序的路径上。

`birds.js`在app目录中创建一个名为以下内容的路由器文件：

```javascript
var express = require('express')
var router = express.Router()

// middleware that is specific to this router
router.use(function timeLog (req, res, next) {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page')
})
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds')
})

module.exports = router
```

然后，在应用程序中加载路由器模块：

```javascript
var birds = require('./birds')
// ...
app.use('/birds', birds)
```

该应用程序现在将能够处理对`/birds`和的请求`/birds/about`，以及调用`timeLog`特定于该路线的中间件功能。