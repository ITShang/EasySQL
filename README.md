# EasySQL
 面向对象SQL生成
    
参考Hibernate中对SQL语句的操作方式，将面向过程的数据库SQL操作修改为面向对象的方式。有效的解决了在手写SQL语句过程中的语法问题，简化了SQL编写，提升了准确性。

操作类型
----------
支持传统的增加(RPersistence)、删除(RDelete)、修改(RUpdate)、查询(RSelect)

示例
-----------
连接查询RGoup和RUser表:
   
    DataTable::RGroup rgp;
    DataTable::RUser rus;
    RSelect select({rus.table,rgp.table});
    select.select(rus.table,{rus.id,rus.account}).
            on(rus.table,rus.id,rgp.table,rgp.userId).
            createCriteria().
            add(Restrictions::eq(rgp.table,rgp.id,request->groupId));

更新RGroup_User和RUser表:

    DataTable::RGroup_User rgu;
    DataTable::RUser ru;

    RUpdate rpd({rgu.table,ru.table});
    rpd.update(rgu.table,rgu.groupId,request->groupId).
            on(rgu.table,rgu.userId,ru.table,ru.id).
            createCriteria().
            add(Restrictions::eq(rgu.table,rgu.groupId,request->oldGroupId)).
            add(Restrictions::eq(ru.table,ru.account,request->user.accountId));
