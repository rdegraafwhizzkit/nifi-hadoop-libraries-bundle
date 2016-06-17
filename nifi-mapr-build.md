Build Full NiFi with MapR Dependencies
======================================
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
# git clone https://github.com/apache/nifi.git
git clone http://git-wip-us.apache.org/repos/asf/nifi.git
git checkout -b 0.x origin/0.x
```

### Build 

```
cd nifi
# assuming you are running 5.1 - otherwise check the docs for the appropriate version
# for  mapr 4.0.2 use version : 2.5.1-mapr-1503
mvn -T 2.0C clean install -DskipTests -Pmapr -Dhadoop.version=2.7.0-mapr-1602
mvn -T 2.0C clean install -DskipTests -Pmapr -Dhadoop.version=2.5.1-mapr-1503
```

### Deploy
final build will be created at `nifi-assembly/target/nifi-0.x.0-SNAPSHOT-bin.zip`
