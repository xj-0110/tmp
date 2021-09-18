# HBase

## 集群搭建

前置条件：hadoop环境（可以不需要yarn） zookeeper环境

下载解压安装包

进入hbase/config/下修改相应的配置文件

1、regionservers文件

```bash
hadoop102
hadoop103
hadoop104
```

2、hbase-env.sh文件

```bash
#添加java_home
export JAVA_HOME=/opt/module/jdk1.8.0_202

#注释掉
# export HBASE_MASTER_OPTS="$HBASE_MASTER_OPTS -XX:PermSize=128m -XX:MaxPermSize=128m"
# export HBASE_REGIONSERVER_OPTS="$HBASE_REGIONSERVER_OPTS -XX:PermSize=128m -XX:MaxPermSize=128m"

#修改 内置zk为false
export HBASE_MANAGES_ZK=false
```

3、hbase-site.xml

```bash
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <property>
    <name>hbase.rootdir</name>
    <value>hdfs://hadoop102:9000/HBase</value>
  </property>
  <property>
    <name>hbase.cluster.distributed</name>
    <value>true</value>
  </property>
  <property>
    <name>hbase.master.port</name>
    <value>16000</value>
  </property>
  <property>
    <name>hbase.zookeeper.quorum</name>
    <value>hadoop102,hadoop103,hadoop104</value>
  </property>
  <property>
    <name>hbase.zookeeper.dataDir</name>
    <value>/opt/module/zookeeper-3.5.7/zkData</value>
  </property>
</configuration>
```

配置完成

bin目录下 启动集群 在哪台机器执行启动命令 那台机器就为master

## 基本操作

### DDL

1. 增

### DML





与HIVE集成



```
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-common-1.3.1.jar $HIVE_HOME/lib/hbase-common-1.3.1.jar
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-server-1.3.1 $HIVE_HOME/lib/hbase-server-1.3.1
您在 /var/spool/mail/root 中有新邮件
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-server-1.3.1.jar $HIVE_HOME/lib/hbase-server-1.3.1.jar
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-client-1.3.1.jar $HIVE_HOME/lib/hbase-client-1.3.1.jar
您在 /var/spool/mail/root 中有新邮件
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-protocol-1.3.1.jar $HIVE_HOME/lib/hbase-protocol-1.3.1.jar
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-it-1.3.1.jar $HIVE_HOME/lib/hbase-it-1.3.1.jar
您在 /var/spool/mail/root 中有新邮件
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar $HIVE_HOME/lib/htrace-core-3.1.0-incubating.jar
ln: 无法创建符号链接"/opt/module/hive-2.3.4/lib/htrace-core-3.1.0-incubating.jar": 文件已存在
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-hadoop2-compat-1.3.1.jar $HIVE_HOME/lib/hbase-hadoop2-compat-1.3.1.jar
您在 /var/spool/mail/root 中有新邮件
[root@hadoop102 ~]# ln -s $HBASE_HOME/lib/hbase-hadoop-compat-1.3.1.jar $HIVE_HOME/lib/hbase-hadoop-compat-1.3.1.jar

```











```
create table hive_hbase_emp_table
(empno int ,ename string ,job string ,mgr int,hiredate string,sal double,comm double,deptno int )
stored by 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
with serdeproperties ("hbase.columns.mapping"=":key,info:ename,info:job,info:mgr,info:hiredate,info:sal,info:comm,info:deptno")
tblproperties ("hbase.table.name"="hbase_emp_table");

```





















