#### 条件

- 使用where子句对表中的数据筛选，结果为true的行会出现在结果集中
- 语法如下：

```
select * from 表名 where 条件;
```

##### 比较运算符

- 等于=
- 大于>
- 大于等于>=
- 小于<
- 小于等于<=
- 不等于!=或<>

##### 逻辑运算符

- and
- or
- not

##### 模糊查询

- like
- %表示任意多个任意字符
- _表示一个任意字符

##### 范围查询

- in表示在一个非连续的范围内，用()表示，如查找id是1,2,3的学生

  ```
  select * from students where id in (1,3,8)
  ```

- between ... and ...表示在一个连续的范围内

##### 空判断

- 注意：null与''(空字符串)是不同的
- 判空is null
- 判非空is not null

##### 优先级

- 小括号，not，比较运算符，逻辑运算符
- and比or先运算，如果同时出现并希望先算or，需要结合()使用