# 获取部分行

- 当数据量过大时，在一页中查看数据是一件非常麻烦的事情
- 语法

```
select * from 表名
limit start,count
```

- 从start开始，获取count条数据
- start索引从0开始

#### 示例：分页

- 已知：每页显示m条数据，当前显示第n页
- 求总页数：此段逻辑后面会在python中实现
  - 查询总条数p1
  - 使用p1除以m得到p2
  - 如果整除则p2为总数页
  - 如果不整除则p2+1为总页数
- 求第n页的数据

```
select * from students
where isdelete=0
limit (n-1)*m,m
```