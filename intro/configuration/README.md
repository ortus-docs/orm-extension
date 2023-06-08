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

<table><thead><tr><th width="258">Setting Name</th><th width="128">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>autoGenMap</code></td><td><code>true</code></td><td>Specifies whether ColdFusion should automatically generate entity mappings for the persistent CFCs. If <code>autogenmap=false</code>, the mapping should be provided in the form of <code>.HBMXML</code> files.</td></tr><tr><td><code>autoManageSession</code></td><td><code>true</code></td><td>Allows the engine to manage the Hibernate session. It is recommended not to let the engine manage it for you.  <br><br>Use <code>transaction</code> blocks in order to demarcate your regions that should start, flush and end a transaction.<br><br><a href="https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#transactions">https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#transactions</a></td></tr><tr><td><code>cacheConfig</code></td><td><code>true</code></td><td>Specifies the location of the configuration file that the secondary cache provider should use. This setting is used only when <code>secondaryCacheEnabled=true</code>. See <a href="./#secondary-cache">Secondary Cache</a> below.</td></tr><tr><td><code>cacheProvider</code></td><td><code>"ehcache"</code></td><td><p>Specifies the cache provider that ORM should use as a secondary cache. The values can be:</p><ul><li><code>Ehcache</code></li><li><code>ConcurrentHashMap</code></li><li>The fully qualified name of the class for any other cache provider.</li></ul><p>See <a href="./#secondary-cache">Secondary Cache</a> below.</p></td></tr><tr><td><code>catalog</code></td><td></td><td>Specifies the default Database Catalog that ORM should use.</td></tr><tr><td><code>cfclocation</code></td><td><code>empty</code></td><td><p>Specifies the directory (or array of directories) that should be used to search for persistent CFCs to generate the mapping. </p><p></p><p><strong>Always specify it or pay a performance startup price.</strong></p><p></p><p><strong>Important:</strong></p><p>If it is not set, the extension looks at the application directory, its sub-directories, and its mapped directories to search for persistent CFCs.</p></td></tr><tr><td><code>datasource</code></td><td><code>application.datasource</code></td><td>This setting defines the data source to be utilized by the ORM.  If not used, defaults to the <code>this.datasource</code> in the <code>Application.cfc</code></td></tr><tr><td><code>dbcreate</code></td><td><code>none</code></td><td><ul><li><code>update</code> : Creates the database according to your ORM model.  It only does incremental updates. It will never remove tables, indexes, etc.</li><li><code>dropcreate</code> : Same as above but it destroys the database if it has ny content and recreates it every time the ORM is reloaded.</li><li><code>none</code> : Does not change the database at all.</li></ul></td></tr><tr><td><code>dialect</code></td><td><code>autodiscover</code></td><td>The dialect to use for your database. By default Hibernate will introspect the datasource and try to figure it out.  See the dialects section below.<br><br>You can also use the fully Java qualified name of the class.</td></tr><tr><td><code>eventHandling</code></td><td><code>false</code></td><td>If true, then it enables the ORM event callbacks in entities and globally via the <code>eventHandler</code></td></tr><tr><td><code>eventHandler</code></td><td></td><td>The CFC path of the CFC that will manage the global ORM events.</td></tr><tr><td><code>flushAtRequestEnd</code></td><td><code>true</code></td><td>Specifies if an orm flush should be called automatically at the end of a request.  In our opinion this SHOULD never be true.  A database persistence should be done via <code>transaction</code> tags and good transaction demarcation.</td></tr><tr><td><code>logSQL</code></td><td><code>false</code></td><td>Specifies if the SQL queries should be logged to the console.</td></tr><tr><td><code>namingstrategy</code></td><td><code>default</code></td><td>Defines the database standard and naming convention.<br><br>- <code>default</code> : Uses the table or column names as is<br>- <code>smart</code> : This strategy changes the logical table or column name to uppercase.<br>- <code>CFC PATH</code> : Use your own CFC to determine naming.<br><br>Please see the <a href="naming-strategies.md">Naming Strategy</a> Section</td></tr><tr><td><code>ormconfig</code></td><td></td><td>The path to a custom Hibernate configuration file:<br><br>- hibernate.properties<br>- hibernate.cfc.xml<br><br>Please see <a href="custom-hibernate-config.md">Custom Hibernate Config</a></td></tr><tr><td><code>savemapping</code></td><td><code>false</code></td><td>If enabled, the ORM will create the Hibernate mapping XML (<code>*.hbmxml</code>) files alongside the entities.  This is great for debugging your entities and relationships.</td></tr><tr><td><code>schema</code></td><td></td><td>The default database schema to use</td></tr><tr><td><code>secondaryCacheEnabled</code></td><td><code>false</code></td><td>Enable the secondary cache or not. See our <a href="../../usage/caching.md">Caching</a> section.</td></tr><tr><td><code>skipCFCWithError</code></td><td><code>false</code></td><td>If <code>true</code>, then the ORM will ignore CFCs that have compile time errors in them.  Use <code>false</code> to throw exceptions.</td></tr><tr><td><code>sqlScript</code></td><td></td><td>Path to a SQL script file that will be executed after the ORM is initialized.  A great way to seed a database.</td></tr><tr><td><code>useDBForMapping</code></td><td><code>true</code></td><td><p>Specifies whether the database has to be inspected to identify the missing information required to generate the Hibernate mapping. </p><p></p><p>The database is inspected to get the column data type, primary key and foreign key information.</p></td></tr></tbody></table>



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



