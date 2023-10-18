# Built-In Functions

The Ortus ORM Extension offers a number of CFML functions for loading and manipulating entities as well as managing the ORM session:

* [Built-In Functions](#built-in-functions)
  * [EntityDelete](#entitydelete)
  * [EntityLoad](#entityload)
  * [EntityLoadByExample](#entityloadbyexample)
  * [EntityLoadByPK](#entityloadbypk)
  * [EntityMerge](#entitymerge)
  * [EntityNameArray](#entitynamearray)
  * [EntityNameList](#entitynamelist)
  * [EntityNew](#entitynew)
  * [EntityReload](#entityreload)
  * [EntitySave](#entitysave)
  * [EntityToQuery](#entitytoquery)
  * [IsValidDatasource](#isvaliddatasource)
  * [ORMClearSession](#ormclearsession)
  * [ORMCloseAllSessions](#ormcloseallsessions)
  * [ORMCloseSession](#ormclosesession)
  * [ORMEvictCollection](#ormevictcollection)
  * [ORMEvictEntity](#ormevictentity)
  * [ORMEvictQueries](#ormevictqueries)
  * [ORMExecuteQuery](#ormexecutequery)
  * [ORMFlush](#ormflush)
  * [ORMGetSession](#ormgetsession)
  * [ORMGetSessionFactory](#ormgetsessionfactory)
  * [ORMQueryExecute](#ormqueryexecute)
  * [ORMReload](#ormreload)

## EntityDelete

`EntityDelete` allows you to delete the row associated with an instantiated entity from the database:

```js
entityDelete( myEntity );
```

Only a single argument is accepted - the entity to delete - and the deletion is not persisted until the session is flushed.

```js
entityDelete( myEntity );
// entity (row) still exists in the database.
ormFlush();
// entity (row) is now wiped from the database.
```

**Returns: `null`**

## EntityLoad

**Returns: `Array`|`Component`|`null`**

## EntityLoadByExample

**Returns: `Array`|`Component`|`null`**

## EntityLoadByPK

`EntityLoadByPK()` allows you to instantiate an entity using the row identified by a primary key:

```js
var theUser = entityLoadByPk( "User", url.userID );
```

A third argument, `unique`, is documented *but not implemented* in either the Lucee Hibernate extension or the Ortus ORM Extension.

**Returns: `Component`|`null`**

## EntityMerge

`EntityMerge()` will merge a "detached" entity (meaning, not connected to any open session) back into the session.

For example, running `ormClearSession()` will detach all loaded entities from the session. If you then make changes to an entity via a setter and run `ormFlush()`, those entity modifications will not be persisted unless you first merge the entity back to the session:

```js
var detachedAutoEntity = entityLoadByPK( "Auto", "12345" );

// make a change but don't save it
detachedAutoEntity.setModel( "Fusion" );

// clear session - will "detach" the entity
ormClearSession();

// "merge" it back to the session
var merged = entityMerge( detachedAutoEntity );

// changes should be reflected in the new entity
expect( merged.getModel() ).toBe( "Fusion" );
```

**Returns: `Component`**

## EntityNameArray

`EntityNameArray()` returns an array of all mapped entity names for the CFML application:

```js
var entityTypes = entityNameArray();
```

EntityNameArray accepts no arguments.

**Returns: `Array`**

## EntityNameList

True to its name, EntityNameList returns a string list of all mapped entity names for the CFML application:

```js
var entityTypes = entityNameList();
```

You can pass a string delimiter value as the first argument, if you don't like commas:

```js
var entityTypes = entityNameList( "|" );
```

**Returns: `string`**

## EntityNew

The `entityNew()` method allows you to create a new instance of a known entity type:

```js
var myCar = entityNew( "Auto" );
```

You can also pass a struct of properties to populate into the entity:

```js
var myCar = entityNew( "Auto", {
  make : "Ford",
  model : "Fusion",
  id : createUUID()
} );
```

Note that if you try to populate a property which does not exist, you will get an error:

```js
var myCar = entityNew( "Auto", {
    make : "Ford",
    model : "Fusion",
    propThatDoesntExist : "abc"
} );
```

This will throw an error: `component [Auto] has no function with name [setPROPTHATDOESNTEXIST]`

**Returns: `Component`**

## EntityReload

`entityReload()` will reload or refresh the entity state from the database. Local, unpersisted modifications will be replaced with database values.

Here's a quick example:

```js
var myCar = entityLoadByPK( "Auto", "12345" );

// make a change but don't save it
myCar.setModel( "Revuelto" );

// reload the entity
entityReload( myCar );

// our local changes should be replaced with the DB value
expect( myCar.getModel() ).toBe( "Aventador" );
```

**Returns: `null`**

## EntitySave

`EntitySave()` is how you save entity modifications. The changes will not persist to the database until `ormFlush()` is called:

```js
var myCar = entityNew( "Auto", {
  make : "Ford",
  model : "Fusion",
  id : createUUID()
} );
entitySave( myCar );
ormFlush();
```

EntitySave accepts an optional boolean parameter, `forceInsert`, which will tell Hibernate to skip the entity existence check and insert the entity:

```js
var myCar = entityNew( "User", {
  username : "Johnny.Appleseed",
  password : "McinT0sh"
} );
entitySave( myCar, true );
```

Most of the time this will be unnecessary.

**Returns: `null`**

## EntityToQuery

**Returns: `Query`**

## IsValidDatasource

**Returns: `Boolean`**

## ORMClearSession

**Returns: `null`**

## ORMCloseAllSessions

**Returns: `null`**

## ORMCloseSession

**Returns: `null`**

## ORMEvictCollection

**Returns: `null`**

## ORMEvictEntity

**Returns: `null`**

## ORMEvictQueries

**Returns: `null`**

## ORMExecuteQuery

**Returns: `Array`|`Struct`|`any`**

## ORMFlush

**Returns: `null`**

## ORMGetSession

**Returns: `Session`**

## ORMGetSessionFactory

**Returns: `SessionFactory`**

## ORMQueryExecute

Alias for `ORMExecuteQuery()`. 

Added in `v6.4.0` (unreleased, version number subject to change.) - [5600833](https://github.com/Ortus-Solutions/extension-hibernate/commit/5600833a78f432dc07618895b65b0f3da46474b1)

**Returns: `Array`|`Struct`|`any`**

## ORMReload

**Returns: `null`**
