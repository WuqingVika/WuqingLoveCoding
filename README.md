# WuqingLoveCoding <学习的一点一滴>

## 2017/2/26

- 1.快速删除表中数据，并将另一表tet数据插入到表haha中；
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
4.buildpath里修改jre 1.7, 添加tomcat Server..
5.再记得window ->preferences->Tomcat->tomcat 6.x->jdk->jdk1.7

## 2017/03/01 星期三

- 1.TL9000项目导入时，需要右击项目-》myeclipse-》deployment assembly->add folder->default root 点击apply,然后再project facets->web->修改第二个为ROOT.
- 2.婴儿被领养问题，查出每个婴儿最终领养情况。第一种方式：
select b.* ,username  from baby b left join keepBabyLog k 
on b.yid =k.yid and k.id=(select max(id) from keepBabyLog g where b.yid=g.yid)
第二种方式：select b.* ,(select username from keepBabyLog k  where k.yid=b.yid  order by k.id desc limit 1)from baby b

## 2017/03/06 星期三

- 1.TL9000项目中regionGridnamewindow.jsp弹出选择网格时，保存后关闭当前页面，并刷新页面。
           ``` //关闭并刷新
							var win;
							var obj;
							if (top) {
							    win = top;
							} else {
							    win = window;
							}
							if (win.opener) {
							    obj = win.opener;
							} else {
							    obj = win.dialogArguments;
							}

							if (obj.button) {
							    obj.button.submit();
							} else if (obj.apply) {

							    obj.apply.submit();
							}
							win.close();
							//关闭刷新 end
```
