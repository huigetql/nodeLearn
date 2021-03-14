### HTTP模块

引入

```
const http = require("http");
```

创建server服务器对象

```
const server = http.createServer();
```

监听对当前服务器对象的请求，当服务器被请求时，会触发请求事件

```
server.on("request",(req,res)=>{})
```

服务器监听端口号

```
server.listen(port,()=>{})
```

设置状态码和响应头

```
response.writeHead(200, { 'Content-Type': 'text/plain' });
```

设置响应头

```
response.setHeader('Content-Type', 'text/html');
```

写入内容

```
response.write(fileData);
```

结束响应

```
response.end();
```