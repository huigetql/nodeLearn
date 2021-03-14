## 路径模块和系统模块



> __dirname : 获得当前执行文件所在目录的完整目录名

> __filename : 获得当前执行文件的带有完整绝对路径的文件名

> process.cwd() : 获得当前执行node命令时候的文件夹目录名

#### 路径模块

```
// 引入path模块
const path = require("path")

// 返回 path 最后一部分   ext : 可选文件扩展名
path.basename(path[,ext])

// 返回 path 目录名
path.dirname(path)

// 返回 path 的扩展名 即 path 的最后一部分中从最后一次出现 .（句点）字符直到字符串结束。 如果在 path 的最后一部分中没有 .，或者如果 path 的基本名称（参见 path.basename()）除了第一个字符以外没有 .，则返回空字符串。
path.extname(path)

// 会将所有给定的 path 片段连接到一起（使用平台特定的分隔符作为定界符），然后规范化生成的路径
path.join([...paths])


// 会返回一个对象，其属性表示 path 的有效元素。 尾部的目录分隔符会被忽略
	{ root: '/',
	dir: '/目录1/目录2',
	base: '文件.txt',
	ext: '.txt',
	name: '文件' }	
path.parse(path)
// 路径或路径片段的序列解析为绝对路径
path.resolve([...paths])
let arr = ['/learning','node','nodejs']
path.resolve(...arr)   //C:\learning\node\nodejs 
```





#### 系统模块

```
//引入系统模块
const os = require("path")
```



## `os.arch()`

返回为其编译 Node.js 二进制文件的操作系统的 CPU 架构。 可能的值有：`'arm'`、 `'arm64'`、 `'ia32'`、 `'mips'`、 `'mipsel'`、 `'ppc'`、 `'ppc64'`、 `'s390'`、 `'s390x'`、 `'x32'` 和 `'x64'`。



## `os.cpus()`

返回一个对象数组，其中包含有关每个逻辑 CPU 内核的信息

每个对象上包含的属性有：

- `model` 
- `speed` 以兆赫兹为单位。
- `times` 
  - `user` : 在用户模式下花费的毫秒数。
  - `nice`  : CPU 在良好模式下花费的毫秒数。
  - `sys`  :  CPU 在系统模式下花费的毫秒数。
  - `idle` : CPU 在空闲模式下花费的毫秒数。
  - `irq` : CPU 在中断请求模式下花费的毫秒数。



## `os.freemem()`

以整数的形式返回空闲的系统内存量（以字节为单位）。



## `os.platform()`

返回标识操作系统平台的字符串。 该值在编译时设置。 可能的值有 `'aix'`、 `'darwin'`、 `'freebsd'`、 `'linux'`、 `'openbsd'`、 `'sunos'` 和 `'win32'`。

返回的值等价于 [`process.platform`](http://nodejs.cn/s/wxcquH)。

如果 Node.js 在 Android 操作系统上构建，则也可能返回 `'android'` 值。 [Android 的支持是实验性的](http://nodejs.cn/s/4Wkt3D)。



## `os.totalmem()`

以整数的形式返回系统的内存总量（以字节为单位）