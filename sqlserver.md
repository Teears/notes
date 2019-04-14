# notes
some notes for study  

## 数据定义语言（DDL）  
* 定义基本表的语句格式：  
create table <表名>(  
列名 列数据类型 约束  
)  

* 查看表结构：  
sp_help <表名>  

* 删除表：  
drop table <表名>  

* 增加表中的属性  
alter table <表名> add <列名> <数据类型> <约束>  

* 修改表中的某属性(某列)：  
alter table <表名> alter column <列名> <数据类型> <约束>  

* 删除表中的某属性(某列)  
alter table <表名> drop column <列名> <数据类型> <约束>



## 数据操纵语言（DML）  
