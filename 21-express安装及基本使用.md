## Express

#### 安装

```
// save 会生成 package.json文件 
npm install express --save  
```

#### Express脚手架的安装

```
npm i express-generator
```

可通过express -h查案命令行的指令含义

```
Options:
    --version        输出版本号
-e, --ejs            添加对 ejs 模板引擎的支持
    --pug            添加对 pug 模板引擎的支持
    --hbs            添加对 handlebars 模板引擎的支持
-H, --hogan          添加对 hogan.js 模板引擎的支持
-v, --view <engine>  添加对视图引擎（view） <engine> 的支持 (ejs|hbs|hjs|jade|pug|twig|vash) （默认是 jade 模板引擎）
    --no-view        创建不带视图引擎的项目
-c, --css <engine>   添加样式表引擎 <engine> 的支持 (less|stylus|compass|sass) （默认是普通的 css 文件）
    --git            添加 .gitignore
-f, --force          强制在非空目录下创建
-h, --help           输出使用方法
```

创建一个名为myApp 的Express应用，并使用ejs模板引擎

```
express --view=ejs myApp 
```

进入myApp，并安装依赖

```
cd myapp
npm install
```

**启动Express应用：**

```
set DEBUG=myapp:* & npm start
```

#### 基本使用

引入express模块

```
const express = require("express");
```

创建express实例

```
let app = express();
```

设置访问端口号

```
app.listen(port,()=>{})
```

设置访问路径

```
app.get/post(path,(req,res)=>{})
```



