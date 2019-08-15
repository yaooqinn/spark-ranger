# Spark SQL Ranger Security Plugin [![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html) [![](https://tokei.rs/b1/github/yaooqinn/spark-ranger)](https://github.com/yaooqinn/spark-ranger)  [![codecov](https://codecov.io/gh/yaooqinn/spark-ranger/branch/master/graph/badge.svg)](https://codecov.io/gh/yaooqinn/spark-ranger) [![Build Status](https://travis-ci.com/yaooqinn/spark-ranger.svg?branch=master)](https://travis-ci.com/yaooqinn/spark-ranger) [![HitCount](http://hits.dwyl.io/yaooqinn/spark-ranger.svg)](http://hits.dwyl.io/yaooqinn/spark-ranger)

ACL Management for Apache Spark SQL with Apache Ranger, enabling:

- Table/Column level authorization
- Row level filtering
- Data masking

## Build
Spark SQL Ranger Security Plugin is built based on [Apache Maven](http://maven.apache.org),

```bash
mvn clean package -Pspark-2.3 -Pranger-1.0 -DskipTests
```

Currently, available profiles are:

Spark: -Pspark-2.3, -Pspark2.4

Ranger: -Pranger-1.0, -Pranger-1.1, -Pranger-1.2

## Usage

### Installation

Place the spark-ranger-<version>.jar into $SPARK_HOME/jars.

### Configurations

#### Ranger admin client configurations

Create ranger-spark-security.xml in $SPARK_HOME/conf and add the following configurations for pointing to the right ranger admin server

```xml

<configuration>

    <property>
        <name>ranger.plugin.spark.policy.rest.url</name>
        <value>ranger admin address like http://ranger-admin.org:6080</value>
    </property>

    <property>
        <name>ranger.plugin.spark.service.name</name>
        <value>a ranger hive service name</value>
    </property>

    <property>
        <name>ranger.plugin.spark.policy.cache.dir</name>
        <value>./a ranger hive service name/policycache</value>
    </property>

    <property>
        <name>ranger.plugin.spark.policy.pollIntervalMs</name>
        <value>5000</value>
    </property>

    <property>
        <name>ranger.plugin.spark.policy.source.impl</name>
        <value>org.apache.ranger.admin.client.RangerAdminRESTClient</value>
    </property>

</configuration>
```

Create ranger-spark-audit.xml in $SPARK_HOME/conf and add the following configurations to enable/disable auditing.

```xml
<configuration>

    <property>
        <name>xasecure.audit.is.enabled</name>
        <value>true</value>
    </property>

    <property>
        <name>xasecure.audit.destination.db</name>
        <value>false</value>
    </property>

    <property>
        <name>xasecure.audit.destination.db.jdbc.driver</name>
        <value>com.mysql.jdbc.Driver</value>
    </property>

    <property>
        <name>xasecure.audit.destination.db.jdbc.url</name>
        <value>jdbc:mysql://10.171.161.78/ranger</value>
    </property>

    <property>
        <name>xasecure.audit.destination.db.password</name>
        <value>rangeradmin</value>
    </property>

    <property>
        <name>xasecure.audit.destination.db.user</name>
        <value>rangeradmin</value>
    </property>

</configuration>

```

#### Enable plugin via spark extensions

spark.sql.extensions=org.apache.ranger.authorization.spark.authorizer.RangerSparkSQLExtension
