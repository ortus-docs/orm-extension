---
description: Easily configure Hibernate with CFML
---

# Configuration

The ORM extension can be configured by a struct of settings set in `this.ormSettings` in your main `Application.cfc`:

```js
component{
    this.ORMenabled = true;
    this.ormSettings = {
        // << Here Be ORM Configuration! 🤪 >>
    };
}
```

The full list of available properties are:

<table><thead><tr><th width="258">Setting Name</th><th width="128">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>autoGenMap</code></td><td><code>true</code></td><td>Specifies whether ColdFusion should automatically generate entity mappings for the persistent CFCs. If <code>autogenmap=false</code>, the mapping should be provided in the form of <code>.HBMXML</code> files.</td></tr><tr><td><code>autoManageSession</code></td><td><code>true</code></td><td>Allows the engine to manage the Hibernate session.  It is recommended not to let the engine manage it for you.  <a href="configuration.md#session-management">See more below.</a></td></tr><tr><td><code>cacheConfig</code></td><td><code>true</code></td><td>Specifies the location of the configuration file that the secondary cache provider should use.  This setting is used only when <code>secondaryCacheEnabled=true</code>. See <a href="configuration.md#secondary-cache">Secondary Cache</a> below.</td></tr><tr><td><code>cacheProvider</code></td><td><code>"ehcache"</code></td><td><p>Specifies the cache provider that ORM should use as a secondary cache. The values can be:</p><ul><li><code>Ehcache</code> </li><li><code>ConcurrentHashMap</code> </li><li>The fully qualified name of the class for any other cache provider.</li></ul><p>See <a href="configuration.md#secondary-cache">Secondary Cache</a> below.</p></td></tr><tr><td><code>catalog</code></td><td></td><td>Specifies the default Database Catalog that ORM should use.</td></tr><tr><td><code>cfclocation</code></td><td></td><td></td></tr><tr><td><code>datasource</code></td><td><code>true</code></td><td></td></tr><tr><td><code>dbcreate</code></td><td><code>"none"</code></td><td></td></tr><tr><td><code>dialect</code></td><td></td><td></td></tr><tr><td><code>eventHandling</code></td><td><code>false</code></td><td></td></tr><tr><td><code>eventHandler</code></td><td></td><td></td></tr><tr><td><code>flushAtRequestEnd</code></td><td><code>true</code></td><td></td></tr><tr><td><code>logSQL</code></td><td><code>false</code></td><td></td></tr><tr><td><code>namingstrategy</code></td><td></td><td></td></tr><tr><td><code>ormconfig</code></td><td></td><td></td></tr><tr><td><code>savemapping</code></td><td><code>false</code></td><td></td></tr><tr><td><code>schema</code></td><td></td><td></td></tr><tr><td><code>secondaryCacheEnabled</code></td><td><code>false</code></td><td></td></tr><tr><td><code>skipCFCWithError</code></td><td><code>false</code></td><td></td></tr><tr><td><code>sqlScript</code></td><td></td><td></td></tr><tr><td><code>useDBForMapping</code></td><td><code>false</code></td><td></td></tr></tbody></table>

## Datasource / Database

There are many ORM configuration settings which affect the database connection:

* `catalog`
* `datasource`
* `dbcreate`
* `dialect`

## Event Handling

Hibernate ORM allows reacting to various events in the session lifecycle such as `onPreInsert`, `onPostUpdate`, `onFlush`, etc. To enable listening to these events, set `eventHandling` to `true` and pass a path to the global event handler using `eventHandler`:

```js
this.ormSettings = {
    eventHandling: true,
    eventHandler : "path/to/global/EventHandler.cfc"
};
```

The `EventHandler.cfc` must then contain function definitions matching the ORM events you wish to listen for.

Currently, the available event names are:

* `onFlush`
* `postNew`
* `preLoad`
* `postLoad`
* `preInsert`
* `postInsert`
* `preUpdate`
* `postUpdate`
* `preDelete`
* `onDelete`
* `postDelete`
* `onEvict`
* `onClear`
* `onDirtyCheck`
* `onAutoFlush`

Here's an example of an EventHandler configured for all events:

```js
component {

	public component function init(){
		return this;
	}

	function onFlush( entity ) {
		// Do something upon function call
	}

	function postNew( any entity, any entityName ){
		// Do something upon function call
	}

	function preLoad( entity ){
		// Do something upon function call
	}
	function postLoad( entity ){
		// Do something upon function call
	}

	function preInsert( entity ){
		// Do something upon function call
	}
	function postInsert( entity ){
		// Do something upon function call
	}

	function preUpdate( entity, Struct oldData  ){
		// Do something upon function call
	}
	function postUpdate( entity ){
		// Do something upon function call
	}

	function preDelete( entity ){
		// Do something upon function call
	}	
	function onDelete( entity ) {
		// Do something upon function call
	}
	function postDelete( entity ) {
		// Do something upon function call
	}

	function onEvict() {
		// Do something upon function call
	}
	function onClear( entity ) {
		// Do something upon function call
	}
	function onDirtyCheck( entity ) {
		// Do something upon function call
	}
	function onAutoFlush( entity ) {
		// Do something upon function call
	}
}
```

## Secondary Cache

A secondary cache provider is a class which manages a level of caching that is secondary to Hibernate's main caching context - the Hibernate session. A secondary cache enables longer-running cache contexts, more fine-grained control over cache busting, and other performance-related benefits.

The only setting necessary to enable secondary caching is the `secondaryCacheEnabled` setting:

```js
this.ormSettings = {
    secondaryCacheEnabled : true
};
```

To configure the caching, specify the path to an XML cache configuration file in `cacheConfig`:

```js
this.ormSettings = {
    secondaryCacheEnabled: true,
    cacheConfig          : "./config/ehcache.xml"
};
```

This `ehcache.xml` cache configuration then should look something like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="ehcache.xsd" updateCheck="true" name="default">
    <diskStore path="java.io.tmpdir"/>
        <defaultCache
            maxElementsInMemory="10000" eternal="false"
            timeToIdleSeconds="120" timeToLiveSeconds="120"
            maxElementsOnDisk="10000000" diskExpiryThreadIntervalSeconds="120"
            memoryStoreEvictionPolicy="LRU">
            <persistence strategy="localTempSwap"/>
        </defaultCache>
        <cache
            name="Autos"
            maxElementsInMemory="20"
            overflowToDisk="false"
            eternal="true">
        </cache>
</ehcache>
```

### Alternate Cache Providers Are Unsupported

While there is a `cacheProvider` setting, only EHCache (currently) is supported as a secondary cache provider.

```js
this.ormSettings = {
    secondaryCacheEnabled : true,
    // NOT SUPPORTED!
    cacheProvider : "ConcurrentHashMap"
};
```

Thus, any usage of `cacheProvider` other than `"ehcache"` will be ignored.

## Session Management

## Additional Configuration

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