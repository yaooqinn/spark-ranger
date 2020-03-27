# Installation Addons

We have listed some tips and known problems about this library you can consider. 

## Ranger Admin does not list databases, tables and columns when you create or edit policies.

Because the Ranger Admin does use Hadoop 3 Hive libraries, listing databases, tables and columns do not work in Ranger Admin. To configure listing capabality put below files in $RANGER_HOME/ews/webapp/WEB-INF/lib/ :

- hive-exec-1.2.1.spark2.jar (Hadoop 3 compatible version needed. You can download from [here](https://github.com/MobinRanjbar/hive-exec-jar/releases).
- hive-jdbc-1.2.1.spark2.jar (Available on Spark Jars folder)
- hive-metastore-1.2.1.spark2.jar (Available on Spark Jars folder)
- hive-service-1.2.1.jar (Download from internet)

and ranger-admin restart.

## The dependency issues in Apache Ranger 2.X.X

### NoClassDefFoundError: com.kstruct.gethostname4j.Hostname

To resolve it, place 'gethostname4j.jar' into $SPARK_HOME/jars.

### NoClassDefFoundError: com.sun.jna.Platform

To resolve it, place 'jna-5.5.0.jar' into $SPARK_HOME/jars.



