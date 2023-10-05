# Properties

Entity properties are how we map table columns to CFML object values. You can specify an entity property by setting `persistent="true"` on any `property` inside a persistent CFML component:

```js
component persistent="true"{
    property name="name" type="string" persistent="true";
}
```

By default, all properties inside a `persistent=true` component are assumed to be persistent as well. Thus, we can skip the `persistent=true` annotation for brevity:

```js
component persistent="true"{
    property name="name" type="string";
}
```

## Property Types

There are several "type" concepts and annotations you may need to use to keep the proper format when persisting or retrieving table data. While these may look similar, they are not equivalent.

| Attribute     | Usage                         | Examples                                                                                  |
|---------------|-------------------------------|-------------------------------------------------------------------------------------------|
| `type`        | `date`,`numeric`              | CFML data type                                                                            |
| `fieldtype`   | `column`,`id`, `one-to-many`  | Denote a special type of field, like an identifier or relationship field.                 |
| `ormType`     | `big_decimal`,`timestamp`     | Data type for the database value.                                                         |
| `sqlType`     |                               | A vendor-specific SQL type used for table creation only. This can normally be ignored.    |

## Field Type

The `fieldtype` attribute allows you to define the behavior and purpose of this property:

```js
property
    name="userID"
    fieldtype="id"
    type="string";
```

There are several options for the `fieldtype` value:

* `column` - By far the most common, this is the default behavior of every field.
* `id` - Notes this field as the primary key or part of the a composite key.
* `collection` - Denote a collection of items - this could represent a struct, an array
* `version` - Denote a version field, useful for [optimistic locking](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) on an entity
* `timestamp` - Denote a timestamp field
* `one-to-one` - Denote a [one-to-one relationship](relationships.md#one-to-one)
* `one-to-many` - Denote a [one-to-many relationship](relationships.md#one-to-many)
* `many-to-one` - Denote a [many-to-one relationship](relationships.md#many-to-one)
* `many-to-many` - Denote a [many-to-many relationship](relationships.md#many-to-many)
* `primary` - Not currently used.

## Common Property Annotations

* `persistent`
* `name`
* `type`
* `default`
* `fieldtype`
* `ormType`
* `column`
* `sqlType`
* `dbDefault`

## Generator Annotations

* `generator`
* `sequence`
* `selectkey`
* `params`
* `generated`

## Validation

* `unique`
* `uniquekey`
* `notnull`
* `validate`
* `validateParams`

## Collection Modifiers

These property annotations are used when setting `fieldtype="collection"` and `collectiontype` is either `struct` or `map`.

* `elementcolumn`
* `elementtype`
* `structkeytype`
* `structkeycolumn`

## Relationship Modifiers

* `inversejoincolumn`
* `linkschema`
* `linkcatalog`
* `linktable`
* `missingRowIgnored`
* `inverse`
* `fkcolumn`
* `orderby`
* `fetch`
* `cascade`
* `constrained`
* `optimisticLock`
* `mappedby`
* `cfc`
* `joinColumn`
* `where`
* `singularname` - *Not currently supported*

## Other

* `scale`
* `length`
* `precision`
* `update`
* `insert`
* `formula`
* `index`
* `lazy`
* `cacheUse`
* `unSavedValue`
* `table`