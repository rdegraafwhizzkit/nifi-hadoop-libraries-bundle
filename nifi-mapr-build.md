Build Full NiFi with MapR Dependencies
======================================

### Clone
```
git clone https://git-wip-us.apache.org/repos/asf/nifi.git
# change branch to latest stable nifi release (if you dont want master branch)
git checkout -b 1.2.0 rel/nifi-1.2.0
```

```
cd nifi
# assuming you are running MapR 5.2 - otherwise check the docs for the appropriate version
MAVEN_OPTS="-Xms1024m -Xmx3076m -XX:MaxPermSize=256m"
mvn -T 2.0C clean install -DskipTests -Pmapr -Dhadoop.version=2.7.0-mapr-1607
```

### Deploy
final build will be created at `nifi-assembly/target/nifi-1.x.0-SNAPSHOT-bin.zip`

