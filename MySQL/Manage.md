## 管理MySQL的命令  

* USE db_name;  
 选择数据库

* SHOW DATABASES;  
 显示所有数据库

* SHOW TABLES;  
 显示指定数据库的所有数据表

* SHOW COLUMNS FROM table;  
 显示数据表的属性、属性类型、主键信息、是否为Null、Default值等其他信息 

* SHOW INDEX FROM table;  
 显示数据表的详细索引信息，包括PRIMARY KEY

* SHOW TABLE STATUS LIKE [FROM db_name] [LIKE 'pattern'] \G;  
 按列打印表名包含pattern的表信息

* DROP DATABASE db_name;  
 删除数据库
