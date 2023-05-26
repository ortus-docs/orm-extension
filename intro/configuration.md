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

|Setting Name|Default|Description|
|---|---|---|
|`autoGenMap`|`true`||
|`autoManageSession`|`true`||
|`cacheConfig`|`true`||
|`cacheProvider`|`"ehcache"`||
|`catalog`|||
|`cfclocation`|||
|`datasource`|`true`||
|`dbcreate`|`"none"`||
|`dialect`|||
|`eventHandling`|`false`||
|`eventHandler`|||
|`flushAtRequestEnd`|`true`||
|`logSQL`|`false`||
|`namingstrategy`|||
|`ormconfig`|||
|`savemapping`|`false`||
|`schema`|||
|`secondaryCacheEnabled`|`false`||
|`skipCFCWithError`|`false`||
|`sqlScript`|||
|`useDBForMapping`|`false`||


## Datasource / Database

## Event Handling

## Secondary Cache

## Session Management

## Logging
