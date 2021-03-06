# Mysql 常见的错误

## Error Code: 1175. You are using safe update

> 使用MySQL执行update的时候报错：Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Queries and reconnect.

**1、在使用mysql执行update的时候，如果不是用主键当where语句，会报如下错误，使用主键用于where语句中正常。**

异常内容：Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Queries and reconnect.

![可视化软件 错误日志](./img/error-1175-1.jpg)

**2、这是因为MySql运行在safe-updates模式下，该模式会导致非主键条件下无法执行update或者delete命令，执行命令SET SQL_SAFE_UPDATES = 0;修改下数据库模式**

![修改数据库模式](./img/error-1175-2.jpg)

**3、为测试命令确实成功执行，我们先看执行update命令前的数据状态**

![测试是否成功第一步 查询](./img/error-1175-3.jpg)

**4、执行update命令，可以看出命令执行成功的状态**

![测试是否成功第二步 修改](./img/error-1175-4.jpg)

**5、重新查询数据库值，已经成功更新**

![测试是否成功第三步 查询修改后的数据](./img/error-1175-5.jpg)

**6、如果想要提高数据库安全等级，可以在恢复回原有的设置，执行命令：SET SQL_SAFE_UPDATES = 1;**

执行成功后，以delete命令为例，非主键情况下又报错了，说明安全等级修改成功

![如果想要提高数据库安全等级，可以在恢复回原有的设置，执行命令：SET SQL_SAFE_UPDATES = 1;](./img/error-1175-6.jpg)

## mysql解决只能用localhost连接,不能用ip连接的问题

设置允许IP访问，执行语句

```select host,user from mysql.user;```

![查询结果](./img/error-ipconnect-01.png)

``` update mysql.user set host = '%' where user = 'root';```

运行完上面的语句之后,再次执行 select host,user from mysql.user;  确认结果

![查询结果](./img/error-ipconnect-02.png)

 flush privileges;

测试：连接成功