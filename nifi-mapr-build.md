Build Full NiFi with MapR Dependencies
======================================

## If using MapR > 1.0.0

### Clone
```
git clone http://git-wip-us.apache.org/repos/asf/nifi.git
git checkout -b 1.0.0 origin/rel/nifi-1.0.0
```

```
cd nifi
# assuming you are running MapR 5.1 - otherwise check the docs for the appropriate version
# for  mapr 4.0.2 use version : 2.5.1-mapr-1503
mvn -T 2.0C clean install -DskipTests -Pmapr -Dhadoop.version=2.7.0-mapr-1602
```

### Deploy
final build will be created at `nifi-assembly/target/nifi-1.x.0-SNAPSHOT-bin.zip`




## If using NiFi < 1.0.0
### Create MapR maven profile
change your ~/.m2/settings.xml so that you have:

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      https://maven.apache.org/xsd/settings-1.0.0.xsd">
<profiles>
    <profile>
      <id>mapr</id>
      <repositories>
        <repository>
          <id>mapr-repo</id>
          <name>MapR Repository</name>
          <url>http://repository.mapr.com/maven/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>false</enabled>
          </snapshots>
        </repository>
      </repositories>
    </profile>
</profiles>
</settings>
```

### Clone

Clone NiFi 0.x branch 

```
git clone http://git-wip-us.apache.org/repos/asf/nifi.git
# git checkout -b 0.x origin/rel/nifi-0.7.0
git checkout -b 0.x origin/0.x
```

### Remove

> `inotify` Hadoop API is still not compatible with MapR. 
Remove `org.apache.nifi.processors.hadoop.inotify.GetHDFSEvents`
from `nifi/nifi-nar-bundles/nifi-hadoop-bundle/nifi-hdfs-processors/src/main/resources/META-INF/services/org.apache.nifi.processor.Processor`
and all references to `org.apache.nifi.processors.hadoop.inotify` package from src `main` and `test` folders

### Build 

```
cd nifi
# assuming you are running MapR 5.1 - otherwise check the docs for the appropriate version
# for  mapr 4.0.2 use version : 2.5.1-mapr-1503
mvn -T 2.0C clean install -DskipTests -Pmapr -Dhadoop.version=2.7.0-mapr-1602
```

### Deploy
final build will be created at `nifi-assembly/target/nifi-0.x.0-SNAPSHOT-bin.zip`

