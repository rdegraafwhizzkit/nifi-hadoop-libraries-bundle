Build Full NiFi with MapR Dependencies
======================================

## If using NiFI > 1.0.0

### Clone
```
git clone http://git-wip-us.apache.org/repos/asf/nifi.git
git checkout -b 1.0.0 rel/nifi-1.0.0
```

```
cd nifi
# assuming you are running MapR 5.1 - otherwise check the docs for the appropriate version
mvn -T 2.0C clean install -DskipTests -Pmapr -Dhadoop.version=2.7.0-mapr-1602
```

### Deploy
final build will be created at `nifi-assembly/target/nifi-1.x.0-SNAPSHOT-bin.zip`

