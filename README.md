# WuqingLoveCoding
学习的一点一滴
## 2017/2/26
* 1.快速删除表中数据，并将另一表tet数据插入到表haha中；
truncate table haha;
insert into haha select * from tet
## 2017/2/27 星期一
+ 1.如何杀pl/sql进程
select session_id from v$locked_object; --找到锁住的sessionid为517
SELECT sid, serial#, username, osuser FROM v$session where sid = 517;--再找到对应的。。
ALTER SYSTEM KILL SESSION '517,4552';--再杀掉
+ 2.创建hint
create OR REPLACE PROCEDURE gbase.PROC_YWGL_NRI_CABLE AS
BEGIN
truncate table gbase.CONNECTOR;--1
insert /*+ append */ into gbase.CONNECTOR select * from "NRI_CS"."CONNECTOR"@"WLZY.DBLINK" commit;--1
END;
+ 3.从svn检出app项目
1.先拷贝地址，作为工作空间中的项目检出。finish! 
2.然后对项目作调整，右击项目属性->myeclipse->project facets->web勾上改为2.5（对应的版本改下）->添加对应的jar包->更改语言;
3.再在project facets->web 修改web_context-root:ywglapp(这个就是对应上localhost:8080/ywglapp/。。。）
4.buildpath里添加tomcat Server..
