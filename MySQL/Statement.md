## SQL SELECT 语句

> SELECT column1,column2 FROM table;

> SELECT * FROM table;

> SELECT DISTINCT column FROM table;  
> * <font size=2 color=DarkGray>DISTINCT 关键词用于返回唯一不同的值，即去重</font>

## SQL WHERE 子句
WHERE 子句用于过滤记录，提取那些满足指定条件的记录

> SELECT * FROM table WHERE column='pattern';  
> * <font size=2 color=DarkGray>文本用‘’，数字不需要</font>

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