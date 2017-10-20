# NiFi Hadoop Library for MapR

## About this Project
The motivation for creating this bundle is to have NiFi communicate with a MapR cluster. MapR uses different versions of the hadoop libraries and different configurations are needed.

## MapR hadoop distribution and NiFi one-time setup

1. Install MapR client on new linux server: [mapr-client.md](./mapr-client.md)
2. Set auth login config in $NIFI_HOME/conf/bootstrap.conf

    `java.arg.16=-Djava.security.auth.login.config=/opt/mapr/conf/mapr.login.conf`


## How To Use

*Works with maven version 3.3.9 or above.*

The main file that will need updating is the pom.xml in the nifi-mapr-nar directory. A property called mapr.version will need updating with the version of MapR that NiFi will be communicating with.

**Note:** NiFi verision can be changed if necessary in the pom.xml

Run a `mvn clean install` in the nifi-mapr-nar directory and once the build completes successfully the target NiFi bundle will be located in the target directory. The file will be called **nifi-hadoop-libraries-nar-x.y.z.nar**

Copy the nar file to the NiFi environment and replace it with the existing hadoop libraries under **$NIFI_HOME/lib** and restart NiFi. You might want to remove the **$NIFI_HOME/work/nar/extensions/nifi-hadoop-libraries-nar-x.y.z.nar-unpacked** directory while restarting to prevent old jar files being used.

# Using the HDFS Processors

When using the HDFS related processors a configuration neccessary is supplying the core-site.xml. Instead of using the hdfs:// protocol, MapR has its own to communicate with the cluster, that is **maprfs://**

Get the **core-site.xml** from the MapR environment, make the file readable by the user running NiFi and modify the contents to include the **fs.defaultFS** property. The cldbhost and port will come from the MapR environment.

```
...
<property> 
  <name>fs.defaultFS</name>
  <value>maprfs:///</value>
</property>
...
```

Once completed, the HDFS processors in NiFi will be able to communicate with a MapR cluster.
