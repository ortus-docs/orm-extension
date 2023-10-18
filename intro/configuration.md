---
description: Easily configure Hibernate with CFML
---

# Configuration

### Application.cfc

The ORM can be configured by a struct of settings set in `this.ormSettings` in your main `Application.cfc`:

```js
component{
    this.ORMenabled = true;
    this.ormSettings = {
        // << Here Be ORM Configuration! 🤪 >>
    };
}
```

### ORM Settings

The full list of available properties you can use to configure the ORM are the following:

<table><thead><tr><th width="258">Setting Name</th><th width="128">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>autoGenMap</code></td><td><code>true</code></td><td>Specifies whether ColdFusion should automatically generate entity mappings for the persistent CFCs. If <code>autogenmap=false</code>, the mapping should be provided in the form of <code>.HBMXML</code> files.</td></tr><tr><td><code>autoManageSession</code></td><td><code>true</code></td><td>Allows the engine to manage the Hibernate session. It is recommended not to let the engine manage it for you.  <br><br>Use <code>transaction</code> blocks in order to demarcate your regions that should start, flush and end a transaction.<br><br><a href="https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#transactions">https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#transactions</a></td></tr><tr><td><code>cacheConfig</code></td><td><code>true</code></td><td>Specifies the location of the configuration file that the secondary cache provider should use. This setting is used only when <code>secondaryCacheEnabled=true</code>. See <a href="configuration.md#secondary-cache">Secondary Cache</a> below.</td></tr><tr><td><code>cacheProvider</code></td><td><code>"ehcache"</code></td><td><p>Specifies the cache provider that ORM should use as a secondary cache. The values can be:</p><ul><li><code>Ehcache</code></li><li><code>ConcurrentHashMap</code></li><li>The fully qualified name of the class for any other cache provider.</li></ul><p>See <a href="configuration.md#secondary-cache">Secondary Cache</a> below.</p></td></tr><tr><td><code>catalog</code></td><td></td><td>Specifies the default Database Catalog that ORM should use.</td></tr><tr><td><code>cfclocation</code></td><td><code>empty</code></td><td><p>Specifies the directory (or array of directories) that should be used to search for persistent CFCs to generate the mapping. </p><p></p><p><strong>Always specify it or pay a performance startup price.</strong></p><p></p><p><strong>Important:</strong></p><p>If it is not set, the extension looks at the application directory, its sub-directories, and its mapped directories to search for persistent CFCs.</p></td></tr><tr><td><code>datasource</code></td><td><code>application.datasource</code></td><td>This setting defines the data source to be utilized by the ORM.  If not used, defaults to the <code>this.datasource</code> in the <code>Application.cfc</code></td></tr><tr><td><code>dbcreate</code></td><td><code>none</code></td><td><ul><li><code>update</code> : Creates the database according to your ORM model.  It only does incremental updates. It will never remove tables, indexes, etc.</li><li><code>dropcreate</code> : Same as above but it destroys the database if it has ny content and recreates it every time the ORM is reloaded.</li><li><code>none</code> : Does not change the database at all.</li></ul></td></tr><tr><td><code>dialect</code></td><td><code>autodiscover</code></td><td>The dialect to use for your database. By default Hibernate will introspect the datasource and try to figure it out.  See the dialects section below.<br><br>You can also use the fully Java qualified name of the class.<br><br>See the <a href="configuration.md#dialects">dialects</a> section below.</td></tr><tr><td><code>eventHandling</code></td><td><code>false</code></td><td>If true, then it enables the ORM event callbacks in entities and globally via the <code>eventHandler</code></td></tr><tr><td><code>eventHandler</code></td><td></td><td>The CFC path of the CFC that will manage the global ORM events.</td></tr><tr><td><code>flushAtRequestEnd</code></td><td><code>true</code></td><td>Specifies if an orm flush should be called automatically at the end of a request.  In our opinion this SHOULD never be true.  A database persistence should be done via <code>transaction</code> tags and good transaction demarcation.</td></tr><tr><td><code>logSQL</code></td><td><code>false</code></td><td>Specifies if the SQL queries should be logged to the console.</td></tr><tr><td><code>namingstrategy</code></td><td><code>default</code></td><td>Defines the naming convention to use on table and column names.<br><br>- <code>default</code> : Uses the table or column names as is<br>- <code>smart</code> : This strategy changes the logical table or column name to uppercase.<br>- <code>CFC PATH</code> : Use your own CFC to determine naming - see <a href="#custom-naming-strategy">Custom Naming Strategy</a>.</td></tr><tr><td><code>ormconfig</code></td><td></td><td>The path to a custom Hibernate configuration file:<br><br>- hibernate.properties<br>- hibernate.cfc.xml<br><br>Please see <a href="configuration/custom-hibernate-config.md">Custom Hibernate Config</a></td></tr><tr><td><code>savemapping</code></td><td><code>false</code></td><td>If enabled, the ORM will create the Hibernate mapping XML (<code>*.hbmxml</code>) files alongside the entities.  This is great for debugging your entities and relationships.</td></tr><tr><td><code>schema</code></td><td></td><td>The default database schema to use</td></tr><tr><td><code>secondaryCacheEnabled</code></td><td><code>false</code></td><td>Enable the secondary cache or not. See our <a href="../usage/caching.md">Caching</a> section.</td></tr><tr><td><code>skipCFCWithError</code></td><td><code>false</code></td><td>If <code>true</code>, then the ORM will ignore CFCs that have compile time errors in them.  Use <code>false</code> to throw exceptions.</td></tr><tr><td><code>sqlScript</code></td><td></td><td>Path to a SQL script file that will be executed after the ORM is initialized.  A great way to seed a database.</td></tr><tr><td><code>useDBForMapping</code></td><td><code>true</code></td><td><p>Specifies whether the database has to be inspected to identify the missing information required to generate the Hibernate mapping. </p><p></p><p>The database is inspected to get the column data type, primary key and foreign key information.</p></td></tr></tbody></table>

### Dialects

By using the `ormsettings.dialect` you can tell Hibernate which specific database dialect to use for building queries.  By default, Hibernate tries to inspect the datasource and define it for you.  95% of the time, this works.  However, if you want a specific one, then you can use the following names or a fully qualified Java class name.

<table><thead><tr><th width="238">Dialect (short name)</th><th>Remarks</th></tr></thead><tbody><tr><td>Cache71</td><td>Support for the Caché database, version 2007.1.</td></tr><tr><td>CockroachDB192</td><td>Support for the CockroachDB database version 19.2.</td></tr><tr><td>CockroachDB201</td><td>Support for the CockroachDB database version 20.1.</td></tr><tr><td>CUBRID</td><td>Support for the CUBRID database, version 8.3. May work with later versions.</td></tr><tr><td>DB2</td><td>Support for the DB2 database, version 8.2.</td></tr><tr><td>DB297</td><td>Support for the DB2 database, version 9.7.</td></tr><tr><td>DB2390</td><td>Support for DB2 Universal Database for OS/390, also known as DB2/390.</td></tr><tr><td>DB2400</td><td>Support for DB2 Universal Database for iSeries, also known as DB2/400.</td></tr><tr><td>DB2400V7R3</td><td>Support for DB2 Universal Database for i, also known as DB2/400, version 7.3</td></tr><tr><td>DerbyTenFive</td><td>Support for the Derby database, version 10.5</td></tr><tr><td>DerbyTenSix</td><td>Support for the Derby database, version 10.6</td></tr><tr><td>DerbyTenSeven</td><td>Support for the Derby database, version 10.7</td></tr><tr><td>Firebird</td><td>Support for the Firebird database</td></tr><tr><td>FrontBase</td><td>Support for the Frontbase database</td></tr><tr><td>H2</td><td>Support for the H2 database</td></tr><tr><td>HANACloudColumnStore</td><td>Support for the SAP HANA Cloud database column store.</td></tr><tr><td>HANAColumnStore</td><td>Support for the SAP HANA database column store, version 2.x. This is the recommended dialect for the SAP HANA database. May work with SAP HANA, version 1.x</td></tr><tr><td>HANARowStore</td><td>Support for the SAP HANA database row store, version 2.x. May work with SAP HANA, version 1.x</td></tr><tr><td>HSQL</td><td>Support for the HSQL (HyperSQL) database</td></tr><tr><td>Informix</td><td>Support for the Informix database</td></tr><tr><td>Ingres</td><td>Support for the Ingres database, version 9.2</td></tr><tr><td>Ingres9</td><td>Support for the Ingres database, version 9.3. May work with newer versions</td></tr><tr><td>Ingres10</td><td>Support for the Ingres database, version 10. May work with newer versions</td></tr><tr><td>Interbase</td><td>Support for the Interbase database.</td></tr><tr><td>JDataStore</td><td>Support for the JDataStore database</td></tr><tr><td>McKoi</td><td>Support for the McKoi database</td></tr><tr><td>Mimer</td><td>Support for the Mimer database, version 9.2.1. May work with newer versions</td></tr><tr><td>MySQL5</td><td>Support for the MySQL database, version 5.x</td></tr><tr><td>MySQL5InnoDB</td><td>Support for the MySQL database, version 5.x preferring the InnoDB storage engine when exporting tables.</td></tr><tr><td>MySQL57InnoDB</td><td>Support for the MySQL database, version 5.7 preferring the InnoDB storage engine when exporting tables. May work with newer versions</td></tr><tr><td>MariaDB</td><td>Support for the MariaDB database. May work with newer versions</td></tr><tr><td>MariaDB53</td><td>Support for the MariaDB database, version 5.3 and newer.</td></tr><tr><td>Oracle8i</td><td>Support for the Oracle database, version 8i</td></tr><tr><td>Oracle9i</td><td>Support for the Oracle database, version 9i</td></tr><tr><td>Oracle10g</td><td>Support for the Oracle database, version 10g</td></tr><tr><td>Pointbase</td><td>Support for the Pointbase database</td></tr><tr><td>PostgresPlus</td><td>Support for the Postgres Plus database</td></tr><tr><td>PostgreSQL81</td><td>Support for the PostgrSQL database, version 8.1</td></tr><tr><td>PostgreSQL82</td><td>Support for the PostgreSQL database, version 8.2</td></tr><tr><td>PostgreSQL9</td><td>Support for the PostgreSQL database, version 9. May work with later versions.</td></tr><tr><td>Progress</td><td>Support for the Progress database, version 9.1C. May work with newer versions.</td></tr><tr><td>SAPDB</td><td>Support for the SAPDB/MAXDB database.</td></tr><tr><td>SQLServer</td><td>Support for the SQL Server 2000 database</td></tr><tr><td>SQLServer2005</td><td>Support for the SQL Server 2005 database</td></tr><tr><td>SQLServer2008</td><td>Support for the SQL Server 2008 database</td></tr><tr><td>Sybase11</td><td>Support for the Sybase database, up to version 11.9.2</td></tr><tr><td>SybaseAnywhere</td><td>Support for the Sybase Anywhere database</td></tr><tr><td>SybaseASE15</td><td>Support for the Sybase Adaptive Server Enterprise database, version 15</td></tr><tr><td>SybaseASE157</td><td>Support for the Sybase Adaptive Server Enterprise database, version 15.7. May work with newer versions.</td></tr><tr><td>Teradata</td><td>Support for the Teradata database</td></tr><tr><td>TimesTen</td><td>Support for the TimesTen database, version 5.1. May work with newer versions</td></tr></tbody></table>

{% hint style="info" %}
See the Hibernate Dialect Section: [https://docs.jboss.org/hibernate/orm/5.4/userguide/html\_single/Hibernate\_User\_Guide.html#database-dialect](https://docs.jboss.org/hibernate/orm/5.4/userguide/html\_single/Hibernate\_User\_Guide.html#database-dialect)
{% endhint %}

### Sample Config

Here is an example configuration from the popular ContentBox Modular CMS application

```cfscript
// THE CONTENTBOX DATASOURCE NAME
this.datasource  = "contentbox";
// ORM SETTINGS
this.ormEnabled  = true;
// cfformat-ignore-start
this.ormSettings = {
	// ENTITY LOCATIONS, ADD MORE LOCATIONS AS YOU SEE FIT
	cfclocation           : [
		// If you create your own app entities
		"models",
		// The ContentBox Core Entities
		"modules/contentbox/models",
		// Custom Module Entities
		"modules_app",
		// Custom Module User Entities
		"modules/contentbox/modules_user"
	],
	// THE DIALECT OF YOUR DATABASE OR LET HIBERNATE FIGURE IT OUT, UP TO YOU TO CONFIGURE.
	dialect              : request.$systemHelper.getSystemSetting( "ORM_DIALECT", "" ),
	// DO NOT REMOVE THE FOLLOWING LINE OR AUTO-UPDATES MIGHT FAIL.
	dbcreate             : "update",
	secondarycacheenabled: request.$systemHelper.getSystemSetting( "ORM_SECONDARY_CACHE", false ),
	cacheprovider        : request.$systemHelper.getSystemSetting( "ORM_SECONDARY_CACHE", "ehCache" ),
	logSQL               : request.$systemHelper.getSystemSetting( "ORM_LOGSQL", false ),
	sqlScript            : request.$systemHelper.getSystemSetting( "ORM_SQL_SCRIPT", "" ),
	// ORM SESSION MANAGEMENT SETTINGS, DO NOT CHANGE
	flushAtRequestEnd    : false,
	autoManageSession    : false,
	// ORM EVENTS MUST BE TURNED ON FOR CONTENTBOX TO WORK DO NOT CHANGE
	eventHandling        : true,
	eventHandler         : "cborm.models.EventHandler",
	// THIS IS ADDED SO OTHER CFML ENGINES CAN WORK WITH CONTENTBOX
	skipCFCWithError     : true,
	// TURN ON FOR Debugging if ORM mappings are not working.
	savemapping          : false
};
```

## Custom Naming Strategy

You can define your own naming convention for table and column names by pointing `this.ormSettings.namingStrategy` to a custom CFC path:

```js
this.ormSettings = {
	// ...
	namingStrategy : "models.orm.UnderscoreNamingStrategy"
}
```

The `UnderscoreNamingStrategy.cfc` component should then define two methods: `getTableName()` and `getColumnName()`:

```js
// models/orm/UnderscoreNamingStrategy.cfc
component{
	function getTableName( string tableName ){
		// funky table name conversion here...
	}

	function getColumnName( string columnName ){
		// funky column name conversion here...
	}
}
```