### 1.express解决跨域问题

```js
可使用中间件来设置请求头和请求源
const express = require("express");
let router = express.Router();
router.use((req,res,next)=>{
	res.append("Access-Control-Allow-Origin","*");
    res.append("Access-Control-Allow-Content-Type","*");
    next();
})
```

