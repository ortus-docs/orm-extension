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

## EntityLoad

## EntityLoadByExample

## EntityLoadByPK

EntityLoadByPK allows you to instantiate an entity using the row identified by a primary key:

```js
var theUser = entityLoadByPk( "User", url.userID );
```

A third argument, `unique`, is documented *but not implemented* in either the Lucee Hibernate extension or the Ortus ORM Extension.

## EntityMerge

## EntityNameArray

EntityNameArray returns an array of all mapped entity names for the CFML application:

```js
var entityTypes = entityNameArray();
```

EntityNameArray accepts no arguments.

## EntityNameList

True to its name, EntityNameList returns a string list of all mapped entity names for the CFML application:

```js
var entityTypes = entityNameList();
```

You can pass a string delimiter value as the first argument, if you don't like commas:

```js
var entityTypes = entityNameList( "|" );
```

## EntityNew

## EntityReload

## EntitySave

## EntityToQuery

## IsValidDatasource

## ORMClearSession

## ORMCloseAllSessions

## ORMCloseSession

## ORMEvictCollection

## ORMEvictEntity

## ORMEvictQueries

## ORMExecuteQuery

## ORMFlush

## ORMGetSession

## ORMGetSessionFactory

## ORMQueryExecute

## ORMReload
