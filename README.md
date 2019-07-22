# hive jdbc storage handler
based on https://github.com/apache/hive/tree/master/jdbc-handler (tag rel/release-2.3.5, HIVE-1555:hive 2.3.0 support JDBC Storage Handler).

works fine with hive 2.1.0(hdp 2.6.3.0-235):
- modify hive and hadoop version.
- modify maven shade configuration, add extra jar and mysql driver.
- fix limit bug (reference part of HIVE-1010).

# usage
```
set role admin;
add jar hdfs:///path/to/hive-jdbc-handler-1.0.0.jar;

CREATE EXTERNAL TABLE mysql_your_table(
  id BIGINT,
  code STRING
)
STORED BY 'org.apache.hive.storage.jdbc.JdbcStorageHandler'
TBLPROPERTIES (
    "hive.sql.database.type" = "MYSQL",
    "hive.sql.jdbc.driver" = "com.mysql.jdbc.Driver",
    "hive.sql.jdbc.url" = "jdbc:mysql://IP:PORT/db?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&failOverReadOnly=false&verifyServerCertificate=false&useSSL=false",
    "hive.sql.dbcp.username" = "username",
    "hive.sql.dbcp.password" = "password",
    "hive.sql.query" = "SELECT id,code FROM your_table",
    "hive.sql.dbcp.maxActive" = "4"
);
```
