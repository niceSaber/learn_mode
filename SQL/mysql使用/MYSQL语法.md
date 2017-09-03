# MYSQL语法
## select into 和insert select的区别
其实他们两个的作用都是把一个表的数据给复制到另一个表当中，不过select into不需要自己新建表，而insert select需要
### **select into**的使用
实例：
```sql select id,`NAME` into table2 from table1 ```
其中**table1**代表你想要复制数据的表，**table2**则代表把数据复制到哪张表。（<font color=red>但是mysql不支持**select into**</font>）
### **insert select**的使用
实例：
```sql insert into table2(a,b,c) select a,b,12 from table1 ```
其中**table1**代表你想要复制数据的表，**table2**则代表把数据复制到哪张表。（<font color=red>table2自己必须新建好</font>）



