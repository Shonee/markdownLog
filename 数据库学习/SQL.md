[可以定位本地路径，打开C盘根目录](c:/)

###### [SQL必知必会读书笔记](https://juejin.im/post/5d2335846fb9a07f021a2509)

##### SQL查询语法

1、在员工数据表中根据hire_date列查询最晚入职员工的所有信息：

```sql
Select * FROM employees WHERE hire_date = (SELECT MAX(hire_date) FROM employees);
//先使用函数方法获取最大的hire_date，获取一条，然后根据hire_date获取所有表中信息

SELECT * FROM employees ORDER BY hire_datee.emp_no DESC LIMIT 0,1;
//将hire_date列倒序(时间降序)排列，获取第一条，即最新的员工信息，
//limit是mysql中的语法 SQLServer中不可用，limit m,n 即从m+1开始，取n条数据

SELECT TOP 1 * FROM employees ORDER BY hire_date DESC;
//SQLServer中可以用TOP来获取指定数据条数，即从排序后数据列表中获取
```



2、两个表的关联查询

```sql
select s.*,d.dept_no 
from salaries s,dept_manager d
where s.emp_no = d.emp_no
and s.to_date='9999-01-01'
and d.to_date='9999-01-01'
//注意需要查询的是哪些内容，根据两个表之间的关系建立连接
```



3、两个表连接查询，使用内连接或者外连接查询

```sql
select e.last_name,e.first_name,d.dept_no
from employees as e 
left outer join dept_emp as d
on e.emp_no=d.emp_no
//inner join 两边表同时有对应的数据才会显示，任何一边缺失数据就不显示
//left (outer) join会读取左边数据表的全部数据，即便右边表无对应数据
//right (outer) join会读取右边数据表的全部数据，即便左边表无对应数据
//on 条件是在生成临时表时使用的条件，无论条件是否为真，都会返回左边表中的记录
//where 条件时在临时表生成之后，再对临时表进行过滤的条件，条件不为真则过滤掉
```



4、查找薪水涨幅超过15次的员工号emp_no以及其对应的涨幅次数

```sql
select emp_no,count(*)
from salaries
group by emp_no
having count(*) > 15
//使用group by进行按类分组，emp_no相同的在同一组
//可以使用count函数对每一组进行计数
//having则用来在group中进行筛选数据
//select distinct salary ...
//distinct 代表筛选出的结果去重，即相同的工资只显示一个
```



5、获取所有非manager的员工emp_no,给出两张表，dept_manager和employees表

```sql
select e.emp_no
from employees e
where e.emp_no  
not in (select d.emp_no from dept_manager d)
//in ('aa','bb')；可以通过是否存在集合中来筛选数据，即是aa或者bb的数据
//not in .. 则是不在集合中来筛选数据 
```



6、获取所有员工当前的manager，如果当前的manager是自己的话结果不显示，当前表示to_date='9999-01-01'。
结果第一列给出当前员工的emp_no,二列给出其manager对应的manager_no。

```sql
select de.emp_no,dm.emp_no as manager_no
from dept_emp de,dept_manager dm
where de.emp_no<>dm.emp_no
and de.dept_no=dm.dept_no
and de.to_date='9999-01-01'
and dm.to_date='9999-01-01'
//使用 as 将数据结果显示的列名更改
//自己是经理的员工不显示，因此要用不等于条件筛选
//查找的是当前的经理，因此经理表中一定要有时间条件
```



7、三个表的连接查询，其中一个表中存储了其他两个表的关系（使用两次join连接）

查找所有员工的last_name和first_name以及对应的dept_name，也包括暂时没有分配部门的员工

给出三个表，department、dept_emp、employees

```sql
select e.last_name,e.first_name,de.dept_name
from employees e 
left join dept_emp d on e.emp_no=d.emp_no
left join departments de on d.dept_no=de.dept_no
//用了两次left join 将三个表进行连接
```



8、同一张表的复用进行比较，筛选合适数据

对所有员工的当前(to_date='9999-01-01')薪水按照salary进行按照1-N的排名，相同salary并列且按照emp_no升序排列

```sql
select s1.emp_no,s1.salary,count(distinct s2.salary) as rank
from salaries s1,salaries s2
where s1.salary <= s2.salary
and s1.to_date='9999-01-01'
and s2.to_date='9999-01-01'
group by s1.emp_no
order by rank
//一表复用，需要同一表中的数据进行比较
//s1.salary <= s2.salary 即统计比当前salary数值大的同表内的数据，获取个数作为rank
//distinct s2.salary 用来去除工资数相同的数据，因工资相同时rank并列
```



9、将获取的一组数据作为新的表进行使用

获取员工其当前的薪水比其manager当前薪水还高的相关信息，当前表示to_date='9999-01-01',
结果第一列给出员工的emp_no，
第二列给出其manager的manager_no，
第三列给出该员工当前的薪水emp_salary,
第四列给该员工对应的manager当前的薪水manager_salary

给出 dept_emp,dept_manager,salaries三个表进行操作

```sql
select s1.emp_no,s2.emp_no as manager_no,s1.salary as emp_salary,s2.salary as manager_salary
from 
(select de.emp_no,de.dept_no,s.salary from dept_emp de,salaries s where de.emp_no=s.emp_no and s.to_date="9999-01-01") as s1,
(select dm.emp_no,dm.dept_no,s.salary from dept_manager dm,salaries s where dm.emp_no=s.emp_no and s.to_date="9999-01-01") as s2
where s1.dept_no=s2.dept_no
and s1.salary > s2.salary
//要获取工资高于自己经理的员工，涉及到比较，经理也是员工，和工资表有着相同的关系
//根据其联系获取数据创建两个新表，一个存有员工的，一个存经理的，然后对两个表进行比较
//因为要同部门才有比较，故创建的表中要有dept_no，最终获取的是编号和工资,因此也要有emp_no和salary
```



10、

给出每个员工每年薪水涨幅超过5000的员工编号emp_no、薪水变更开始日期from_date以及薪水涨幅值salary_growth，并按照salary_growth逆序排列。   

 提示：在sqlite中获取datetime时间对应的年份函数为strftime('%Y', to_date) ，给出salaries工资表

```sql
select s2.emp_no,s2.from_date,(s2.salary-s1.salary) as salary_growth
from salaries s1,salaries s2
where s1.emp_no=s2.emp_no
and s2.salary - s1.salary > 5000
and strftime('%Y',s2.to_date) - strftime('%Y',s1.to_date) = 1
order by salary_growth desc
//复用工资表salaries，s2代表涨幅后新工资，s1代表上一工资
//判断同一员工的工资涨幅是否超过5000
//判断工资上涨时间是否在一年内
```

