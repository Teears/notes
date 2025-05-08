\[\]可选 <>名称  
show variables like '%secure%';
# 目录
---------
* [基本操作](#基本操作)
* [数据类型及运算符](#数据类型及运算符)
* [MySQL函数](#MySQL函数)

---------

# 基本操作
**库**  
创建库：show databases; -> create database database_name; -> show create database database_name\g 
删除库：drop database database_name;  
查看存储引擎：show engines \g  
查看错误：show warnings;  
**创建表**  
指定库：use <库名>;  
创建表：create table <表名>(字段名 数据类型);*多个字段用逗号分隔*  
**约束**  
主键约束：primary key | \[constraint <约束名>\]primary key(字段1,字段2,...)  
外键约束：\[constraint <外键名>\] foreign key 字段名1 \[,字段名2,...\] references <主表名> 主键列1 \[,主键列2,...\] *外键名是自己设定的*  
非空约束：not null  
唯一性约束：unique | \[constraint sth\] unique(<字段名>)  
默认约束：default 默认值  
表属性值自动增加：auto_increment *必须设置在主键且只能设置一个*  
**查看表**  
查看表基本结构：describ/desc 表名;  
查看表详细结构：show create table <表名\g>  
**修改表**  
改表名：alter table <旧表名> rename \[to\] <新表名>;  
改字段数据类型：alter table <表名> modify <字段名> <新数据类型>;  
改字段名：alter table <表名> change <旧字段名> <新字段名> <新数据类型>;  
添加字段：alter table <表名> add <新字段名> <数据类型> \[约束条件\] \[first | after 已存在的字段名\];  
删除字段：alter table <表名> drop <字段名>;  
修改字段排列位置：alter table <表名> modify <字段名> <数据类型> first | after <字段名>;  
更改表的存储引擎：alter table <表名> engine=<更改后的引擎名>; *MySQL默认InnoDB*  
删除外键约束：alter table <表名> drop foreign key <外键名>;  
表中插入数据：insert into <表名> values(数据1),(数据2),...;  
**删除表**  
删除没有被关联的表：dorp table \[if exists\] 表1,表2...;  
删除被关联的表：删除子表课可以直接操作，删除父表需要先解除外键约束才能操作。  
# 数据类型及运算符
整数：tinyint/smallint/mediumint/int/bigint  
浮点定点数：float/double/decimal(m,d)  
日期时间：year（yyyy）/time（hh:mm:ss）/date（yyyy-mm-dd）/datetime（yyyy-mm-dd hh:mm:ss）/timestamp（yyyy-mm-dd hh:mm:ss）  
**字符串**  
文本字符串：char(m)/varchar(m) / tinytext/text/mediumtext/longtext   enum（字段名 enum('值1','值2',...)）/set（字段名 set('值1'，'值2'，...)）  
二进制字符串：bit(m)/binary(m)/varbinary(m)/tinyblob(m)/blob(m)/mediumblob(m)/longblob(m)  
查看插入结果：select * from 表名  
查看二进制插入结果：select bin(b+0) from 表名 *b+0表示将二进制转换为对应的数字*  
**运算符**  
算数运算符：+ - * / %  
比较运算符：=、<=>、<>（!=）、<、<=、>、>=、is null（isnull）、is not null、  
least(值1,值2,...)、greatest(值1,值2,...)、expr between min and max、  
expr in(值1,值2,..)、not in、  
'expr' like '匹配条件'（‘%’匹配任何数目的字符，‘_’仅匹配一个字符）、  
'expr' regexp '匹配条件'（‘^’匹配以该字符后面字符开头的字符串，‘$’匹配以该字符后面字符结尾的字符串，‘.’匹配任何一单字符，‘\[...\]’匹配括号内任何字符，‘\*’匹配任意个在它前面的字符）p115  
逻辑运算符：not（!） and（&&） or（||） xor
位运算符：| & ^（位异或） << >> -  
# MySQL函
**数学函数**  
绝对值圆周率平方根取余：abs(x)、pi()、sqrt(x)、mod(x,y)  
获取整数：ceil(x)、ceiling(x)返回不小于x的最小整数，返回值转化为bigint、floor(x)返回不大于x的最大整数，返回值转化为bigint  
随机数：rand()、rand(x)  
舍入：round(x)、round(x,y)将x四舍五入保留到y位，truncate(x,y)x舍去到小数点后y位  
符号函数：sign(x)返回-1、0或1  
幂运算：pow(x,y)、power(x,y)x的y次方  
对数运算：log(x)基数为e的对数,log10(x)基数为10的对数  
角度弧度转化函数：randians(x)将x由角度转化为弧度、degrees(x)弧度转换为角度  
正弦反正弦：sin(x),asin(x)  
余弦反余弦：cos(x),acos(x)  
正切反正切余切：tan(x),atan(x),cot(x)  
**字符串函数**
计算字符数：char_length)('str');
计算串长：length('str');*数字和字母长度为1，一个汉字3字节*  
合并字符串：concat(s1,s2,...); concat_ws(x,s1,s2,...);*x是分隔符*  
替换字符串：insert(s1,x,len,s2);将s1第x个字符开始长度为4的字符串替换为s2  
字母大小写转换：lower(str)、lcase(str)转换为小写字母，upper(str)、ucase(str)转换为大写  
截取串：left(s,n)取s的左边n个字符，right(s,n)取右边n个  
填充串：lpad(s1,len,s2)将s1用s2从左边填充到len长度，rpad(s1,len,s2)从右填充。*如果s1长度大于len则将s1缩短*  
删除空格的：ltrim(s)、rtrim(s)、trim(s)分别删除s左边、右边和两侧的空格  
删除指定串：trim(s1,from,s)删除s两侧的s1子串  
重复串：repeat(s,n)  
空格函数：space(n)返回n个空格组成的串  
替换函数：replace(s,s1,s2)将s中的所有s1替换为s2  
比较串大小：strcmp(s1,s2)  
获取子串：substring(s,n,len)、mid(s,n,len)返回从s的第n个开始长度为len的串，若n为复则倒数  
匹配子串：locate(str1,str)、position(str1 in str)、instr(str,str1)返回str1在str中的起始位置  
逆序：reverse(s)  
返回指定位置字符串：elt(n,str1,str2,...)返回第n个字符串  
返回指定字符串的位置：field(s,s1,s2,...)返回s的位置  
返回子串位置：find_in_set(s1,s2) *s2是字符串列表'str1,str2,...'*  
选取字符串：make_set(x,s1,s2,...) 由x的二进制选定对应位字符串组成  
**时间日期**  
获取当前日期或时间：curdata()、current_date()按yyyy-mm-dd返回，curdate() + 0以yyyymmdd形式返回；curtime()和current_time()返回hh:mm:ss  
获取当前日期和时间：current_timestamp()、localtime()、now()、sysdate()  
Unix时间戳：unix_timestamp(date)，date是时间

