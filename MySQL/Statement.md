## SELECT 语句
### 语法
> SELECT column_name,column_name  
FROM table_name;  

> SELECT * FROM table_name;  


## SELECT DISTINCT 语句
### 语法
> SELECT DISTINCT column_name,column_name  
FROM table_name;  
> * DISTINCT 关键词用于返回唯一不同的值，即去重  


## WHERE 子句
用于过滤记录，提取那些满足指定条件的记录
### 语法
> SELECT column_name,column_name  
FROM table_name  
WHERE column_name operator value;  
> * 文本用‘’，数字不需要  

|  运算符   | 描述  |
|  :----  | :----  |
|=	|等于|
|<>	|不等于|
|>	|大于|
|<	|小于|
|>=	|大于等于|
|<=	|小于等于|
|BETWEEN	|在某个范围内|
|LIKE	|搜索某种模式|
|IN	|指定针对某个列的多个可能值|

## AND & OR 运算符
* AND：两个条件都成立
* OR：两个条件中只要有一个成立
> SELECT * FROM Websites  
WHERE alexa > 15  
AND (country='CN' OR country='USA');  
> * 可以结合使用

## ORDER BY 关键字
用于对结果集按照一个列或者多个列进行排序  
默认升序  
降序：DESC关键字
### 语法
> SELECT column_name,column_name  
FROM table_name  
ORDER BY column_name,column_name ASC|DESC;

