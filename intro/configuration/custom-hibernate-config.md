# Custom Hibernate Config

For full Hibernate configuration support, you can point the ORM extension to an XML file containing any configuration properties you wish to configure:

```js
this.ormSettings = {
    // ...
    ormconfig : "./config/persistence.xml"
};
```

You can then populate the XML file with valid Hibernate configuration syntax:

```xml
<!-- persistence.xml -->
<?xml version="1.0" encoding="UTF-8"?>    
<!DOCTYPE hibernate-configuration PUBLIC    
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"    
        "https://hibernate.org/dtd/hibernate-reverse-engineering-3.0.dtd">    
<hibernate-configuration>    
    <session-factory>    
    
    <!-- https://docs.jboss.org/hibernate/orm/5.4/javadocs/org/hibernate/cfg/AvailableSettings.html#USE_SQL_COMMENTS -->
    <property name="hibernate.use_sql_comments">true</property>
    <property name="hibernate.cache.use_query_cache">true</property>
         
    </session-factory>
</hibernate-configuration>
```
