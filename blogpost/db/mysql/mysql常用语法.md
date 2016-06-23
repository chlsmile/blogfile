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

- 查看某个库里有哪些表
```mysql
show tables;
```

- 创建表
```mysql
create table t_student (
  id bigint(20) unsigned not null  auto_increment comment '主键,自增长',
  name varchar(50) not null default '' comment '姓名',
  mobile varchar(20) not null default '' comment '电话',
  age tinyint(3) not null comment '年龄',
  home_addr varchar(200) not null default '' comment '住址',
  remark varchar(100) default NULL comment '备注',
  create_time datetime not null comment '创建时间',
  update_time datetime not null comment '更新时间',
  primary key(id)
) engine=InnoDB default charset=utf8 comment='学生表';
```
- 删除表
```mysql
drop table t_student;
```

- 修改表-增加字段
```mysql
```
- 修改表-删除字段
```mysql
```
- 修改表-增加索引
```mysql
```

- 修改表-删除索引
```mysql
```


