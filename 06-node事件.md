## Node事件

```
// 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();
// 通过 eventEmitter.on("fnName",function(){}) 监听事件
// 通过 eventEmitter.emit("fnName") 触发事件
```