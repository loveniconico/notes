# 1. 链接数据库
- Console
```sql
/*链接数据库服务器*/
mysql -h [数据库地址:端口] -u [用户名] -p

/*链接数据库*/
mysql -h [数据库地址:端口] -u [用户名] -p [数据库]

/*以上操作完毕后会进入mysql的Console*/
```
- PHP
```php
/**
 *传入的数据都是字符串,都为可选参数
 */
mysqli_connect ([数据库地址], [用户名], [用户密码], [要访问的数据库名], [数据库所在的端口号], [socket]);

/**
 *断开与数据库服务器的链接
 */
bool mysqli_close ( mysqli $link );
```
# 2. 选择数据库
- MySQLConsole
```sql
use [数据名称];
```
- PHP
```php
mysqli_select_db([MySQL连接],[数据名称]);
```
# MySQL数据类型(不完全)
## 数值型

|类型|大小|范围(有符号)|范围(无符号)|用途|
|---|----|-----------|------------|---|
|`TINYIN`|1字节|[-2<sup>8</sup>/2 , 2<sup>8</sup>/2)|[0 , 2<sup>8</sup>)|小整数值,最高可指定3位数字|
|`SMALLINT`|2字节|[-2<sup>16</sup>/2 , 2<sup>16</sup>/2)|[0 , 2<sup>16</sup>)|大整数值,最高可指定5位数字|
|`MEDIUMINT`|3字节|[-2<sup>24</sup>/2 , 2<sup>24</sup>/2)|[0 , 2<sup>24</sup>)|大整数值,最高可指定8位数字|
|`INT`或`INTEGER`|4字节|[-2<sup>32</sup>/2 , 2<sup>32</sup>/2)|[0 , 2<sup>32</sup>)|大整数值,最高可指定10位数字|
|`BIGINT`|8字节|[-2<sup>64</sup>/2 , 2<sup>64</sup>/2)|[0 , 2<sup>64</sup>)|极大整数值,最高可指定20位数字|
|`FLOAT(M,D)`|4字节|||单精度浮点数值,小数精度可以达到6位|
|`DOUBLE(M,D)`|8字节|||双精度浮点数值,小数精度可以达到15位|
|`DECIMAL`|对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2|依赖于M和D的值|依赖于M和D的值|小数值|

> **M** 而整个数字的位数为**M**（包含小数位数）,**D** 表示小数点后有**D**位数字.在`DOUBLE`和`FLOAT`中这两个参数都不是必需参数,`FLOAT`默认为10, 2,`DOUBLE`默认为16, 4;如果**D**的数值超过**

## 字符串

|类型|大小|用途|
|---|----|---|
|`CHAR`|0-255字节|定长字符串|
|`VARCHAR`|0-65535 字节|变长字符串|
|`TINYBLOB`|0-255字节|不超过 255 个字符的二进制字符串|
|`TINYTEXT`|0-255字节|短文本字符串|
|`BLOB`|0-65 535字节|二进制形式的长文本数据|
|`TEXT`|0-65 535字节|长文本数据|
|`MEDIUMBLOB`|0-16 777 215字节|二进制形式的中等长度文本数据|
|`MEDIUMTEXT`|0-16 777 215字节|中等长度文本数据|
|`LONGBLOB`|0-4 294 967 295字节|二进制形式的极大文本数据|
|`LONGTEXT`|0-4 294 967 295字节|极大文本数据|

## 时间

|类型|大小(字节)|范围|格式|用途|
|---|----|---|---|---|
|DATE|3|1000-01-01 ~ 9999-12-31|YYYY-MM-DD|日期值|
|TIME|3|-838:59:59 ~ 838:59:59|HH:MM:SS|时间值或持续时间|
|YEAR|1|1901 ~ 2155|YYYY|年份值|
|DATETIME|8|1000-01-01 00:00:00 ~ 9999-12-31 23:59:59|YYYY-MM-DD HH:MM:SS|混合日期和时间值|
|TIMESTAMP|4|1970-01-01 00:00:00 ~ 2038<br>结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07，格林尼治时间 2038年1月19日 凌晨 03:14:07|YYYYMMDD HHMMSS|混合日期和时间值，时间戳|

# 创建数据库的表
- MySQLConsole
```sql
/*创建表*/
CREATE TABLE [表名] ([列名] [列的数据类型]);

/*实例*/
CREATE TABLE IF NOT EXISTS 'table'(
   'id' INT UNSIGNED AUTO_INCREMENT,
   'title' VARCHAR(100) NOT NULL,
   'date' DATE,
   PRIMARY KEY ( 'id' )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
/**实例解析
 *'IF NOT EXISTS':如果同名表不存在则创建
 *'UNSIGNED':数值无符号
 *'NOT NULL':数据不允许为空(null)
 *'AUTO_INCREMENT':定义列为自增的属性，一般用于主键,数值会自动加1
 *'PRIMARY KEY':定义列为主键,您可以使用多列来定义主键,列间以逗号分隔
 *'ENGINE':设置存储引擎(http://www.jianshu.com/p/7bc5612b507e)
 *'CHARSET':设置编码
 */

```
- PHP
```php
$sql = mysqli_connect ('127.0.0.1', 'root', 'root', 'DBName', 3306);
$query = "CREATE TABLE IF NOT EXISTS 'table'(
    'id' INT UNSIGNED AUTO_INCREMENT,
    'title' VARCHAR(100) NOT NULL,
    'date' DATE,
    PRIMARY KEY ( 'id' )
)ENGINE=InnoDB DEFAULT CHARSET=utf8";

$resultmode = MYSQLI_USE_RESULT;//(如果需要检索大量数据，请使用这个;可省略,默认为MYSQLI_STORE_RESULT)
mysqli_query($sqlLink,$query,$resultmode);
```

# 插入数据
- MySQLConsole
```sql
INSERT INTO [table_name]( [field1], [field2],...[fieldN] )
                        VALUES
                        ( [value1], [value2],...[valueN] ),
                        ( [value1], [value2],...[valueN] ),
                        ( [value1], [value2],...[valueN] );

/*增加列*/
ALTER TABLE tableName ADD columnName [类型及属性] [位置];
```

- PHP
```php
$sql = mysqli_connect ('127.0.0.1', 'root', 'root', 'DBName', 3306);
$query = "INSERT INTO [table_name]( [field1], [field2],...[fieldN] )
                        VALUES
                        ( [value1], [value2],...[valueN] ),
                        ( [value1], [value2],...[valueN] ),
                        ( [value1], [value2],...[valueN] );";
mysqli_query($sqlLink,$query);
```

# 删除表&删除数据(行)
### **以下慎用,真有可能变成`从删库到跑路`**
- MySQLConsole
```sql
/*删除表*/
DROP TABLE tableName;

/*删除表内的所有内容*/
DELETE FROM tableName;

/*删除符合条件的数据行*/
DELETE FROM tableName WHERE [条件];

/*删除指定列和其内容*/
ALTER TABLE tableName DROP columnName;
```
- PHP
```php
$sql = mysqli_connect ('127.0.0.1', 'root', 'root', 'DBName', 3306);
$query = "DROP TABLE table";
$query = "DELETE FROM table";
$query = "DELETE FROM table WHERE name = ''";
mysqli_query($sql,$query);
```

# 修改数据(升级数据)
- MySQLConsole
```sql
//修改表名
ALTER TABLE tableName RENAME TO newTableName;

//修改列属性
ALTER TABLE tableName MODIFY columnName [新属性];

//修改列名又修改属性
ALTER TABLE tableName CHANGE oldColumnName NewColumnName [属性];

//修改列的默认值
ALTER TABLE tableName ALTER columnName SET DEFAULT [默认值];

//修改指定的列的值
UPDATE tableName SET column_1=newVal, column_2=newVal

//修改符合条件的指定的列的值
UPDATE tableName SET column_1=newVal, column_2=newVal WHERE [条件]
```
- PHP
```php
$sql = mysqli_connect ('127.0.0.1', 'root', 'root', 'DBName', 3306);
$query = "UPDATE tableName SET column_1=newVal, column_2=newVal";
mysqli_query($sql,$query);
```

# 查询数据
- MySQLConsole
```sql
/**
 * 语法: SELECT [返回的数据列] FROME [查询的表] WHERE [查询的条件]
 */
/*返回整个表的内容*/
SELECT * FROM table_anme ;
/*返回指定列的内容*/
SELECT column_name FROM table_anme ;
/*返回指定列的内容*/
SELECT column1_name,column2_name,... FROM table_anme ;
/*对整个表进行指定的列的升降序排列*/
SELECT * FROM guitarwars ORDER BY column_name [ASC/DESC]
/*返回符合条件的行*/
SELECT * FROM table_anme WHERE [条件] ;
/*返回符合条件的数据*/
SELECT column_name FROM table_anme WHERE [条件] ;
/*返回指定的数量的条目*/
SELECT * FROM table_anme LIMIT [数量];
/*返回多个表的数据(表与表需要有数据关联)*/
SELECT
    table_anme1.id,
    table_anme2.name
FROM table_anme1
INNER JOIN table_anme2
ON (table_anme1.id = table_anme2.id)

SELECT
    table_anme1.id,
    table_anme2.name
FROM table_anme1
    INNER JOIN table_anme2
USING (id)
```

- PHP
```php
$sql = mysqli_connect ('127.0.0.1', 'root', 'root', 'DBName', 3306);
$query = "SELECT * FROM table_anme WHERE [条件] ;";
$retval = mysqli_query($sqlLink,$query);//返回的是结果集标识,数据还在mysql中需要特定的函数取出数据

//以下数据返回的是
$row = mysqli_fetch_all($result);
/**以上返回的格式是:
 *Array
 *(
 *  [0] => Array(
 *      [0] => val_1
 *      [1] => val_2
 *      ...
 *      [n] => val_n )
 *  [1] => Array(
 *      [0] => val_1
 *      [1] => val_2
 *      ...
 *      [n] => val_n )
 *  ...
 *  [n] => Array(
 *      [0] => val_1
 *      [1] => val_2
 *      ...
 *      [n] => val_n )
 *)
 */

//以下数据返回的是单条数据
//第一次请求的是返回第一条符合条件的数据,第二次请求的是返回第二条符合条件的数据,以此类推
$row = mysqli_fetch_array($retval,MYSQLI_BOTH);
//mysqli_fetch_array第二参数默认为'MYSQLI_BOTH',可以不写
/**返回的格式是:
 *Array(
 *  [0] => val_1
 *  [column_name_1] => val_1
 *  [1] => val_2
 *  [column_name_2] => val_2
 *  ...
 *  [n-1] => val_n
 *  [column_name_n] => val_n )
 */
$row = mysqli_fetch_array($retval,MYSQLI_ASSOC);
$row = mysqli_fetch_assoc($retval);
/**以上返回的格式是:
 *Array(
 *  [column_name_1] => val_1
 *  [column_name_2] => val_2
 *  ...
 *  [column_name_n] => val_n )
 */
$row = mysqli_fetch_array($retval,MYSQLI_NUM);
$row = mysqli_fetch_row($retval);
/**以上返回的格式是:
 *Array(
 *  [0] => val_1
 *  [1] => val_2
 *  ...
 *  [n] => val_n
 */
```

# MySQL语句总结

- `DROP TABLE tableName` : 会从数据库删除整个表和表内的数据
- `DESCRIBE tableName` : 返回一个表的结构,并且不会暴露表内的数据
- `SELECT * FROM tableName` : 返回表内所有的数据,若`*`为列名则返回该列的所有数据
- `DELETE FROM tableName` : 删除表内的所有数据
- `WHERE` : SQL的条件语句,结合其他SQL命令使用,一般跟在其他SQL命令后面
- `LIMIT` : 用于控制SQL语句操作上的数量,例如 :删除多少条,返回多少条
- `ASC` :升序排列
- `DESC` :降序排列
- `INNER JOIN ` : 连接两个表
- ``
