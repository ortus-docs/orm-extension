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

## Event Handling

## Secondary Cache

## Session Management

## Logging
