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