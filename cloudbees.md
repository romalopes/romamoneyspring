# Step by Step creation of the environment

```
bees app:create -a romamoneyspring -t tomcat7
bees db:create romamoneyspring

bees app:bind -a romamoneyspring -db romamoneyspring -as romamoneyspring
bees config:set -a romamoneyspring -P spring.profiles.active=default,javaee
bees config:set -a romamoneyspring -P jdbc.initLocation=classpath:db/mysql/initDB.sql
bees config:set -a romamoneyspring -P jdbc.dataLocation=classpath:db/mysql/populateDB.sql
bees config:set -a romamoneyspring -P hibernate.dialect=org.hibernate.dialect.MySQLDialect
bees config:set -a romamoneyspring -P jpa.database=MYSQL
bees config:set -a romamoneyspring -P jpa.showSql=false


bees app:deploy -a romamoneyspring target/romamoneyspring.war
```

# Spring romamoneyspring Clickstart FAQ

## How does the ClickStart specifies usage of MySQL with a JNDI DataSource

By default, Springromamoneyspring uses an embedded HSQL Database defined in `data-access.properties`.

The CloudBees Spring romamoneyspring Clickstart overides the default parameters defined in `data-access.properties`
to use a JNDI DataSource connected to a MySQL DataSource. This is done setting System Properties with the CloudBees SDK
command `bees config:set -P param=value`. These System Properties are defined in the ClickStart configuration file:
[clickstart.json](https://github.com/CloudBees-community/spring-romamoneyspring-clickstart/blob/master/clickstart.json).

* Use a JNDI DataSource instead of an embedded DataSource activating the Spring Profile `javaee` (see `datasource-config.xml`)

    ```
    bees config:set -a <MYAPP> -P spring.profiles.active=default,javaee
    ```

* Specify the MySQL dialect

    ```
    config:set -a romamoneyspring -P jdbc.initLocation=classpath:db/mysql/initDB.sql
    config:set -a romamoneyspring -P jdbc.dataLocation=classpath:db/mysql/populateDB.sql
    config:set -a romamoneyspring -P hibernate.dialect=org.hibernate.dialect.MySQLDialect
    config:set -a romamoneyspring -P jpa.database=MYSQL
    ```
    
Note: it is possible to override `data-access.properties` values with System Properties because the `<context:property-placeholder />` is defined with `system-properties-mode="OVERRIDE"`:

```xml
<context:property-placeholder 
   location="classpath:spring/data-access.properties" 
   system-properties-mode="OVERRIDE"/>
```
