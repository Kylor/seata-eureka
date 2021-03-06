# seata-eureka

demo地址：https://github.com/Kylor/seata-eureka

seata服务下载地址 https://github.com/seata/seata/releases

seata服务运行: ./seata-server.sh -p 8091 -h 127.0.0.1

seata服务配置：

file.conf:
```Bash
## transaction log store, only used in seata-server
store {
  ## store mode: file、db
  mode = "db"
  ## database store property
  db {
    ## the implement of javax.sql.DataSource, such as DruidDataSource(druid)/BasicDataSource(dbcp) etc.
    datasource = "druid"
    ## mysql/oracle/postgresql/h2/oceanbase etc.
    dbType = "mysql"
    driverClassName = "com.mysql.jdbc.Driver"
    url = "jdbc:mysql://127.0.0.1:3306/mydb"
    user = "root"
    password = "123456"
    minConn = 5
    maxConn = 30
    globalTable = "global_table"
    branchTable = "branch_table"
    lockTable = "lock_table"
    queryLimit = 100
    maxWait = 5000
  }
}
```

registry.conf:
```Bash
registry {
  # file 、nacos 、eureka、redis、zk、consul、etcd3、sofa
  type = "eureka"

  eureka {
    serviceUrl = "http://localhost:8761/eureka"
    application = "eureka-server"
    weight = "1"
  }
  
  file {
    name = "file.conf"
  }
  
}

config {
  # file、nacos 、apollo、zk、consul、etcd3
  type = "file"
  
  file {
    name = "file.conf"
  }
}
```
注意截止2020年5月23号。
```Bash
<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-sleuth</artifactId>
<!--            <version>2.2.2.RELEASE</version>-->
            <version>2.2.1.RELEASE</version>
        </dependency>
```
 请使用2.2.1版本。 2.2.2版本会报错。

运行顺序：

1.eureka

2.seate服务

3.account

4.storage

5.order

6.bussiness

调用bussiness模块里面controller函数查看结果。

