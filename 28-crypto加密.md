## crypto加密

#### 1.	安装

```
npm install crypto --save
```

#### 2.	导入

```
const crypto = require("crypto")
```

#### 3.	使用

```
 //创建算法   
let sf = crypto.createHash("md5")
//加密(默认2进制)
sf.update(String)
//转换加密(base64格式)
let content = sf.digest("hex")
```

