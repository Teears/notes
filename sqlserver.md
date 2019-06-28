# notes
some notes for study  

## DDL——数据定义语言  
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

## DML——数据库的修改  
* 插入数据  
insert into student  
values ( ‘01001’, ‘张三’,27, ‘M’, ‘CS’ )  
insert into student ( sno , sage, sname)  
values ( ‘01002’ , NULL, ‘李四’)  
* 删除数据  
delete from <表名> where <条件>  
* 修改数据  
update student  
set sdept = ‘ma’, sage=sage+1  
where sno = ‘001’  

## DML—— 数据查询（Select）  
**Select子句**  
* distinct去除重复  
select distinct sdept from student  
* \*表示所有属性  
select \* from student  
* 更名  
select sno as ‘学 号’,cno as 课程号,grade 成绩 from sc  

**Where子句**  
* 运算符  
<、<=、=等  
between  
In  
is null  
and、or、not  
* Like  
% —— 匹配任意字符串  
_ —— 匹配任意一个字符  
select sno，sname  
from  student  
where sname Like ‘张%’  
* 表连接  

**From 子句**  
* 元组变量方便引用  
select T.sno，sname，cno，grade  
from Student as T，sc S  
where T.sno = S.sno  

**Order by子句**  
asc升序（缺省）、desc降序  
order by sage desc  

**子查询**  
* 单值比较  
父查询与单值子查询之间用比较运算符进行连接 运算符：>、>=、=、<=、<、<>  
* 多值  
子查询返回多行一列 运算符：In、All、Some(或Any)、Exists  
Select * From Student Where sage <= all (  
Select sage From Student )  

**聚合函数**  
* Avg( ) Sum( ) Min( ) Max( ) Count( ) Count(\*)、Count(Distinct…)  
* Group By  
只有出现在Group By子句中的属性，才可出现在Select子句中  
Select sdept，count(\*) as stu_count  
From Student  
Group By sdept  
* Having  
跟在Group By子句的后面,针对聚合函数的结果值进行筛选  

**存在判断Exists**  
不关心子查询的具体内容，因此用 Select \*  
Select sno,sname  
From Student  
Where Exists  
( Select * From SC Where SC.sno = Student.sno And grade = 100)  

**块插入**  
Insert Into SC  
Select sno,’c05’,null  
From Student  
Where sdept = ‘CS’  

**更新块**  
Update SC  
Set grade = grade+10  
Where sno in  
(select sno from student where sdept=‘CS’)  

**example**  
Select sname from student  
where not exists  
(select * from course  
where not exists  
(select * from sc  
and cno=course.cno))  
