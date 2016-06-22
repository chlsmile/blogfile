## mysql常用语法

- 创建db
```mysql
create database test01 default character set utf8 default collate utf8_general_ci;
```
- 查询db列表
```mysql
show databases;
```
- 切换到指定的db
```mysql
use test01;
```
- 删除指定的db
```mysql
drop database test01;
```

- 创建表
```mysql
create table t_order (
  id bigint(20) unsigned not null auto_increment comment '数据库主键,自增长'
  primary key(id)
) engine=InnoDB auto_increment=1 default charset=utf8 comment='订单表';
```
- 删除表
```mysql
```

- 修改表-增加字段
```mysql
```
- 修改表-删除字段
```mysql
```


