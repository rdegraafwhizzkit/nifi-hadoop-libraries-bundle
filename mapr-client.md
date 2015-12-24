mapr-client-setup
-----------------

Instructions to setup MapR client on fresh linux server.


1. install rpm tools

```bash
sudo sayum install syslinux
```

2. install mapr-client

```bash
sudo rpm -Uvh mapr-client-4.0.2.29870.GA-1.x86_64.rpm
```

3. connect mapr-client to Hadoop cluster. 

```bash
# /opt/mapr/server/configure.sh [-N <cluster name>] -c -C <CLDB node>[:<port>][,<CLDB node>[:<port>]...]
sudo  /opt/mapr/server/configure.sh -c -N datalake_qa -C hadoop1:7022,hadoop2:7022,hadoop3:7022-Z zk1:5000,zk2:5000,zk3:5000 -HS hadoop1
```

4. configure core-site.xml

```bash
sudo vi /opt/mapr/hadoop/hadoop-2.5.1/etc/hadoop/core-site.xml
```

replace `my_uid`, `my_qid` and `my_username` with your account info. 

```xml
<configuration>
<property>
  <name>hadoop.spoofed.user.uid</name>
  <value>my_uid</value>
</property>
<property>
  <name>hadoop.spoofed.user.gid</name>
  <value>my_qid</value>
</property>
<property>
  <name>hadoop.spoofed.user.username</name>
  <value>my_username</value>
</property>
<property>
    <name>fs.defaultFS</name>
    <value>maprfs://hadoop:7022</value>
</property>
</configuration>
```

6. Test

```
hadoop fs -ls /datalake/tenant/user 
```
 