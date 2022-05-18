# 入门



## clickhouse 特点





- 适合做宽表，分析
- 单表性能优于关联查询
- 避免join操作，关联查询性能，
  - A join B:会将B全部加载到内存







## clickhouse 安装



配置打开文件限制

nofile：文件数

nproc：进程数





selinux：  security 。。 ：安全防护

ClickHouse各文件目录：
    bin/    ===>  /usr/bin/ 
    conf/   ===>  /etc/clickhouse-server/
    lib/    ===>  /var/lib/clickhouse 
    log/    ===>  /var/log/clickhouse-server







启动clickhouse：

sudo clickhouse status;

sudo clickhouse start/stop/restart

udo vim /etc/clickhouse-server/config.xml  



clickhouse-client --query "show databases;"



## 数据类型



### 整形









## 表索引





### MergeTree



#### TTL

##### 列级别的TTL



##### 表级别的TTL



## SQL 操作







###  查询操作



join操作







