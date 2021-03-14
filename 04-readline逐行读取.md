## readline 逐行读取

#### 引入

> const readline = require("readline")

#### 创建`readline.interface()`实例`readline.Interface` 类的实例是使用 `readline.createInterface()` 方法构造的。 每个实例都关联一个 `input` [可读流](http://nodejs.cn/s/zz7Dx3)和一个 `output` [可写流](http://nodejs.cn/s/LzH75p)。 `output` 流用于为到达的用户输入打印提示，并从 `input` 流读取

> const rl = readline.createInterface(option)

`option`<object>

+ input : 要监听的可读流，
+ output : 将逐行读取数据写入的可写流



#### `rl.question(query,callback)`事件

+ query : 要写入`output`的语句或者询问，前置提示符
+ callback : 调用时传入用户的输入以作为相应query

`rl.question()` 方法通过将 `query` 写入 `output` 来显示它，并等待用户在 `input` 上提供输入，然后调用 `callback` 函数将提供的输入作为第一个参数传入。

当调用时，如果 `input` 流已暂停，则 `rl.question()` 将恢复 `input` 流。

如果 `readline.Interface` 创建时 `output` 被设置为 `null` 或 `undefined`，则不会写入 `query`。



#### `rl.on()`

监听事件



#### ` rl.close()`

`rl.close()` 方法会关闭 `readline.Interface` 实例，并放弃对 `input` 和 `output` 流的控制。 当调用时，将触发 `'close'` 事件。

调用 `rl.close()` 不会立即停止 `readline.Interface` 实例触发的其他事件（包括 `'line'`）。







