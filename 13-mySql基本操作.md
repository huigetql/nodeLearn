## Node.js 连接数据库

#### 安装

```
npm install mysql
```

#### 连接数据库

```
//引入
const mysql = require("mysql");
//设置数据库参数
let options = {
	//主机名
	host : "localhost",
	//端口号，默认3306，可选
	port : "3306",
	//用户名
	user : "root",
	//密码
	password : "123456",
	//连接表名
	database : "test"
}
//创建数据库
let connection = mysql.createConnection(options)
//启动数据库
connection.connect(function(err){})
//执行数据库语句
参数 ： 
sqlStr : sql语句，对数据库的增删改查语句，可以用变量的形式
ValueAr : 参数数组，在sql语句中的value值用 ? 代替，在此项参数找值。反应速度更快
function : 回调函数，err监听操作是否有异常，results表示查询结果，fields表示字段信息

connection.query(sqlStr[,ValueArr],function(err,results,fields){})
```



#### 数据库相关操作

##### 创建数据库

```
create database 数据库名
```

##### 删除数据库

```
drop database 数据库名
```

##### 创建数据表

```
create table 表名 (
	//逗号结尾
	`字段名` 字段属性,
	·········
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

解析

+ 如果不想字段为NULL，则可以设置字段属性为NOT NULL
+ AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
+ PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。
+ ENGINE 设置存储引擎，CHARSET 设置编码。

##### 删除数据表

```
drop table 表名
```

##### 选择数据库

```
use 库名
```

##### 插入数据

```
//可插入多条，如果数据时字符型，必须使用单引号或者双引号
insert into 表名 (字段) values (字段值)
```

##### 更新数据

```
//可同时更新多个字段，可以自where子句中指定任何条件，也可以在一个单独表中同时更新数据
update 表名 set field1=newValue1,field2=newValue2 [where ···]
```

##### 删除数据

```
//如果没有指定where子句，则会删除表中全部记录
delete from 表名 [where ···]
```

##### 排序

```
select * from 表名 order by 列1 asc|desc,列2 asc|desc
```

+ 将行数据按照列1进行排序，如果某些行列1的值相同时，则按照列2排序，以此类推
+ 默认按照列值从小到大排列
+ asc从小到大排列，即升序
+ desc从大到小排序，即降序