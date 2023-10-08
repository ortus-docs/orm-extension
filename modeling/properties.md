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

## Common Property Annotations

| Attribute     | Type      | Description                                                                                |
|---------------|-----------|-------------------------------------------------------------------------------------------|
| `persistent`  | `boolean` | Define this property as a persistent property. If `false`, this property will be completely ignored in Hibernate / the ORM extension. |
| `name`        | `string`  | Property name                                                                             |
| `default`     | `string`  | Default value for the property. This only reaches the CFML engine, and *does not affect creation of the entity table.* |
| `column`      | `string`  | Table column where the property value is stored.                                          |
| `dbDefault`   | `string`  | Set the default value for the property.                                                   |

Make sure you quote datetime `dbdefault` values to avoid invalid date errors in MySQL:

```js
property
    name     ="createdOn"
    ormtype  ="datetime"
    dbdefault="'2016-10-10'";
```



## Property Types

There are several "type" concepts and annotations you may need to use to keep the proper format when persisting or retrieving table data. While these may look similar, they are not equivalent.

| Attribute     | Examples                      | Description                                                                                |
|---------------|-------------------------------|-------------------------------------------------------------------------------------------|
| `type`        | `date`,`numeric`              | CFML data type                                                                            |
| `fieldtype`   | `column`,`id`, `one-to-many`  | Denote a special type of field, like an identifier or relationship field.                 |
| `ormType`     | `big_decimal`,`timestamp`     | Data type for the database value.                                                         |
| `sqlType`     | `nvarchar`                    | A vendor-specific SQL type used for table creation only. This can normally be ignored.    |

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

## Generator Annotations

| Attribute     | Type                  | Description                                                                                |
|---------------|-----------------------|--------------------------------------------------------------------------------------------|
| `generator`   | `string`              | One of `increment`,`identity`,`native`,`seqhilo`,`uuid`,`guid`,`select`,`foreign`, `assigned` |
| `params`      | `struct`, `string`    | `{ "table: "uuid_table", column: "uuid_value_column" }` |
| `sequence`    | `string`              | |
| `selectkey`   | `string`              | Only used with `generator=select`. Specify the select key to use when selecting sequence values from the database.|
| `generated`   | `string`              | `always`, `insert`, `never`. |

## Validation

| Attribute        | Type       | Description                                                                                |
|------------------|------------|--------------------------------------------------------------------------------------------|
| `insert`         | `boolean`  | Allow inserting values to new rows. |
| `update`         | `boolean`  | Allow value updates on existing rows. |
| `notnull`        | `boolean`  | Specify a not-null constraint. |
| `uniquekey`      | `string`   | Specify a key name for a unique constraint. Useful for defining a unique constraint across multiple columns. |
| `unique`         | `boolean`  | Specify a unique constraint. Default `false`.|
| `validateParams` | `string`   | *Not currently supported* |
| `validate`       | `string`   | *Not currently supported* |

## Collection Modifiers

These property annotations are used when setting `fieldtype="collection"` and `collectiontype` is either `struct` or `map`.

| Attribute     | Type                         | Description                                                                                |
|---------------|-------------------------------|-------------------------------------------------------------------------------------------|
| `structkeycolumn` | `string` ||
| `structkeytype` | `string` ||
| `elementtype` | `string` ||
| `elementcolumn` | `string` ||

## Relationship Modifiers

| Attribute             | Type                | Description                                                                                |
|-----------------------|---------------------|--------------------------------------------------------------------------------------------|
| `table`               | `string`            | Define the table where the foreign items are stored. |
| `lazy`                | `boolean`, `string` | Define a lazy association retrieval type. One of `true`, `false`, `extra`. |
| `inverse`             | `boolean`           | Specify that the association "owner" is referenced and managed on the opposite entity - not this current entity. |
| `inversejoincolumn`   | `string`            | Specify the join column on the associated entity. For `inverse` associations only. |
| `linkschema`          | `string`            | Specify the schema name of the link table |
| `linkcatalog`         | `string`            | Specify the catalog name of the link table |
| `linktable`           | `string`            | Specify the name of the link table |
| `missingRowIgnored`   | `boolean`           | Do not throw an error if a foreign key has no match in the foreign entity |
| `fkcolumn`            | `string`            | |
| `orderby`             | `string`            | |
| `fetch`               | `string`            | |
| `cascade`             | `string`            | |
| `constrained`         | `boolean`           | Only valid for `one-to-one` relationships. [See Hibernate 3.3 Mapping Documentation](https://docs.jboss.org/hibernate/core/3.3/reference/en/html/mapping.html#mapping-declaration-onetoone) |
| `optimisticLock`      | `boolean`           | Enable optimistic locking on this association. One of `all`, `dirty`, `version`, `none`. |
| `mappedby`            | `string`            | Specify the property on the association that maps to this entity. |
| `cfc`                 | `string`            | Specify the CFC location of the foreign entity. |
| `joinColumn`          | `string`            | Join the foreign entity on this column in this entity. |
| `where`               | `string`            | Arbitrary SQL where clause for the relation. |
| `singularname`        || *Not currently supported* |

## Other

| Attribute      | Type      | Description                                                                                |
|----------------|-----------|--------------------------------------------------------------------------------------------|
| `scale`        | `integer` ||
| `length`       | `integer` ||
| `precision`    | `integer` ||
| `formula`      | `string`  | Define this property as a computed property by using a SQL query to determine the property value. Formula properties cannot be modified. |
| `index`        | `string`  | Key name for a property value index. |
| `cacheUse`     | `string`  | Define a cache type to use for this property. One of `read-only`, `nonstrict-read-write`, `read-write`, or `transactional`. |
| `cacheName`    | `string`  | Set the name of the cache to use for this property. |
| `unSavedValue` | `string`  | Set a value to use for newly instantiated objects. |

## Formula Property

```js
property name="totalPosts"
    ormType="integer"
    formula="(
        SELECT COUNT(*)
        FROM posts
        WHERE posts.FK_user = id
    )";
```