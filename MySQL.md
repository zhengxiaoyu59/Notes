MySQL
管理MySQL的命令
USE db_name;	//选择数据库
SHOW DATABASES;	//显示所有数据库
SHOW TABLES;	//显示指定数据库的所有数据表
SHOW COLUMNS FROM table;	//显示数据表的属性、属性类型、主键信息、是否为Null、Default值等其他信息
SHOW INDEX FROM table;	//显示数据表的详细索引信息，包括PRIMARY KEY
SHOW TABLE STATUS LIKE [FROM db_name] [LIKE 'pattern'] \G;	//按列打印表名包含pattern的表信息
DROP DATABASE db_name;	//删除数据库

SQL SELECT 语句
SELECT column1,column2 FROM table;
SELECT * FROM table;
SELECT DISTINCT column FROM table;	//DISTINCT 关键词用于返回唯一不同的值，即去重

SQL WHERE 子句
WHERE 子句用于过滤记录，提取那些满足指定条件的记录。
SELECT * FROM table WHERE column='pattern';	//文本用‘’，数字不需要
运算符	描述
=	等于
<>	不等于
>	大于
<	小于
>=	大于等于
<=	小于等于
BETWEEN	在某个范围内
LIKE	搜索某种模式
IN	指定针对某个列的多个可能值

