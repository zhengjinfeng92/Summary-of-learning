## 数据库空值（null）是否走索引

### 负向查询（不等于 !=）不能命中索引，会导致全表扫描。

```
!=  和 not in都属于负向查询，会全表扫描，不走索引
```

### 允许空值，不等于(!=)查询，可能导致不符合预期的结果

如果允许空值，**不等于(!=)的查询，不会将空值行(row)包含进来**，此时的结果集往往是不符合预期的，此时往往要加上一个or条件，把空值(is null)结果包含进来;

为null的值不能通过=！查询出来，需要用is null；

```
is null 和 is not null 都可以走索引
```



### 某些or条件，有可能导致全表扫描，此时应该优化为union

```sql
select * from user where id=1 or id is null; -- 会导致全表扫描
select * from user where id=1 
union
select * from user where id is null;  -- 改成这样可以走索引
```

*本文测试于MySQL5.6。*

[原文地址](https://mp.weixin.qq.com/s/XRSPITgWWK-2Ee-cSIqw1w)

