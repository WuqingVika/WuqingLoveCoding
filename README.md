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
