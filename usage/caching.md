---
description: Improve your database performance with secondary caching in Hibernate ORM.
---

# Caching

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

## Configure Each Entity Cache

Notice how our `ehcache.xml` defines a default cache configuration?

```xml
<defaultCache
    maxElementsInMemory="10000" eternal="false"
    timeToIdleSeconds="120" timeToLiveSeconds="120"
    maxElementsOnDisk="10000000" diskExpiryThreadIntervalSeconds="120"
    memoryStoreEvictionPolicy="LRU">
    <persistence strategy="localTempSwap"/>
</defaultCache>
```

We highly recommend adding a cache configuration for each cacheable entity. This will help you optimize caching, and will silence error logs like the below:

```
WARN: HHH90001006: Missing cache[default-update-timestamps-region] was created on-the-fly. The created cache will use a provider-specific default configuration: make sure you defined one. You can disable this warning by setting 'hibernate.cache.ehcache.missing_cache_strategy' to 'create'
```

Here's a quick example. Say we have an `Autos.cfc` persistent component with caching enabled:

```js
component persistent="true" cacheUse="true"{
    // persistent properties...
}
```

For this entity, we'll want to create a `<cache></cache>` entry with a `name` attribute that matches the entity name OR our `cacheName` component annotation:

```xml
<cache
    name="Autos"
    maxElementsInMemory="20"
    overflowToDisk="false"
    eternal="true">
</cache>
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