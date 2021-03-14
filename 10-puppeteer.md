## puppeteer

#### 作用

+ 生成页面 PDF。
+ 抓取 SPA（单页应用）并生成预渲染内容。
+ 自动提交表单，进行 UI 测试，键盘输入等。
+ 创建一个时时更新的自动化测试环境。 使用最新的 JavaScript 和浏览器功能直接在最新版本的Chrome中执行测试。
+ 捕获网站的 [timeline trace](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference)，用来帮助分析性能问题。
+ 测试浏览器扩展。



#### 环境和安装

Puppeteer本身依赖6.4以上的Node，但是为了异步超级好用的[async/await](http://es6.ruanyifeng.com/#docs/async)，推荐使用7.6版本以上的Node。另外headless Chrome本身对服务器依赖的库的版本要求比较高，centos服务器依赖偏稳定，v6很难使用headless Chrome，提升依赖版本可能出现各种服务器问题（包括且不限于无法使用ssh），最好使用高版本服务器。



> npm i puppeteer 



#### 引用

> const puppeteer = require("puppeteer")



#### 使用

```
//创建浏览器实例   异步操作
let browser = puppeteer.launch([option])
```

`option` 参数

- `ignoreHTTPSErrors` 是否在导航期间忽略 HTTPS 错误. 默认是 `false`。
- `headless`  是否以 [无头模式](https://developers.google.com/web/updates/2017/04/headless-chrome) 运行浏览器。默认是 `true`，除非 `devtools` 选项是 `true`。无头模式即看不到过程
- `executablePath` 可运行 Chromium 或 Chrome 可执行文件的路径，而不是绑定的 Chromium。如果 `executablePath` 是一个相对路径，那么他相对于 [当前工作路径](https://nodejs.org/api/process.html#process_process_cwd) 解析。
- `slowMo` 将 Puppeteer 操作减少指定的毫秒数。这样你就可以看清发生了什么，这很有用。
- defaultViewport<?Object>为每个页面设置一个默认视口大小。默认是 800x600。如果为null的话就禁用视图口。
  - `width`  页面宽度像素。
  - `height`  页面高度像素。
  - `hasTouch` 指定viewport是否支持触摸事件。默认是 `false`。
- `args` 传递给浏览器实例的其他参数。 这些参数可以参考 [这里](http://peter.sh/experiments/chromium-command-line-switches/)。
- `handleSIGINT`  Ctrl-C 关闭浏览器进程。默认是 `true`。
- `timeout` 等待浏览器实例启动的最长时间（以毫秒为单位）。默认是 `30000` (30 秒). 通过 `0` 来禁用超时。
- `pipe`通过管道而不是WebSocket连接到浏览器。默认是 `false`



```
//创建页面实例   异步操作
const page = browser.newPage()
```



``page``常用方法

```
//跳到url页面
page.goto('url')

//等待时间在进行下一步
page.waitFor(time)

//获取某个DOM元素，单个元素，返回ElementHandle
page.$("selector")

//获取全部DOM元素,一个数组，返回ElementHandle
page.$$("selector")

//获取页面某DOM内容 相当于在页面执行 document.querySelector()，然后把匹配到的元素作为第一个参数传给 pageFunction
page.$eval(selector, pageFunction[, ...args])

//获取页面某DOM内容 相当于在页面执行 document.querySelectorAll(selector))，然后把匹配到的元素数组作为第一个参数传给 pageFunction
page.$$eval(selector, pageFunction[, ...args])

//向页面某个内容写入text，options参数为delay，每个字符输入延迟，默认为0
page.type(selector,text[,options])

//点击页面某个内容
page.click(selector)

//聚焦到某个匹配元素，如果元素不存在就会报错，如果有多个，则聚焦到第一个
page.focus(selector)

//请求拦截，会激活request.abort()、request.continue()和request.respond()方法，提供了修改页面发出的网络请求
page.setRequestInterception(boolean)
//通过以下方式监听请求
page.on("request",(intercceptedRequest)=>{})
```



``ElementHandle``：继承自JSHandle，每一个page.$()或者page.$$()都会返回一个ElementHandle，该属性可以执行一些方法



