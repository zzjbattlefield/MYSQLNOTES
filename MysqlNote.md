# CURD
## 增删改查技巧
### 忽略错误 "ignore" 
使用ignore可以使Mysql忽略错误语句继续执行  

栗子:  
```mysql
insert ignore into "table" 
```

### DUPLICATE KEY UPDATE 
实现不存在就插入,存在就更新  

栗子:  
```mysql
INSERT INTO "table" (id,emp,ip) VALUES 
(5,8004,"192.168.1.1"),
(6,8005,"192.168.1.2")
ON DUPLICATE KEY UPDATE ip = VALUES(ip)
当要插入的数据在表中已经存在的时候(字段为唯一性约束)就会用插入的ip去更新原来表中的数据
```

### 表连接修改
可以将UPDATE语句中的WHERE子查询改成表连接  

```mysql
UPDATE t_emp e JOIN t_dept d ON e.deptno = d.deptno AND d.name='SALES'
SET e.sal=10000,d.name='销售部';
将t_emp表中所有叫销售部的员工工资改成10000,并且修改t_dept中的部门名称
```

### 表连接删除
DELETE语句也可以使用表连接  

```mysql
DELETE e,d FROM t_emp e join t_dept d on e.deptno = d.deptno AND d.dname='销售部';
DELETE 后跟随的表都是会删除的表上面会把部门表中的销售部和员工表中销售部员工全部删除
```
