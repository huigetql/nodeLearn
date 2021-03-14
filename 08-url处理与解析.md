## url模块 -- 处理和解析URL

const url = require("url")



### `url.parse(urlString)`

解析 `url` 字符串

```
const url = require("url");
let urlStr = "https://www.huawei.com/cn/?ic_medium=direct&ic_source=surlent";
console.log(url.parse(urlStr));

// 打印如下
Url {
  protocol: 'https:',
  slashes: true,
  auth: null,
  host: 'www.huawei.com',
  port: null,
  hostname: 'www.huawei.com',
  hash: null,
  search: '?ic_medium=direct&ic_source=surlent',
  query: 'ic_medium=direct&ic_source=surlent',
  pathname: '/cn/',
  path: '/cn/?ic_medium=direct&ic_source=surlent',
  href: 'https://www.huawei.com/cn/?ic_medium=direct&ic_source=surlent'
}
```



### `url.resolve(baseUrl,targetUrl)`

解析相对于baseUrl的目标URL

```
let urlStr = "http://www.baidu.com";
console.log(url.resolve(urlStr, "./learning/node"));

// 打印如下
http://www.baidu.com/learning/node
```









