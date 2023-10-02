# Entities

A persistent entity is a CFML component that is marked as a database entity via the `persistent` annotation upon the component definition:

```js
component persistent="true"{

}
```

You can specify various attributes on the entity via component attributes:

| Attribute             | Type      | Default   | Description                                      |
|-----------------------|-----------|-----------|--------------------------------------------------|
| `persistent`          | `boolean` | `false`   | Mark this component as an ORM entity |
| `entityname`          | `string`  |           | set a custom entity name which is different than the CFC name |
| `table`               | `string`  |           | Specify the database table name |
| `schema`              | `string`  |           | Specify the database schema name. |
| `catalog`             | `string`  |           | Specify the database catalog name. |
| `dynamicinsert`       |           |           | Specifies whether INSERT SQL is to be generated at runtime. Only those columns whose values are not null are included in the SQL. |
| `dynamicinsert`       | `boolean` | `false`   | Specifies whether INSERT SQL is to be generated at runtime. Only those columns whose values are not null are included in the SQL. |
| `dynamicupdate`       | `boolean` | `false`   | Specifies whether UPDATE SQL is to be generated at runtime. Only those columns whose values are not null are included in the SQL. |
| `readonly`            | `boolean` | `false`   | Specify whether table is readonly or not |
| `selectbeforeupdate`  | `boolean` |           | Specify whether Hibernate should never perform an SQL UPDATE unless it is certain that an object is actually modified. In cases when a transient object is associated with a new session using update(), Hibernate performs an extra SQL SELECT to determine if an UPDATE is actually required. |
| `optimisticlock`      | `string`  |           | Determines the locking strategy. It can be any one of: `none`|`version`|`dirty`|`all` |
| `batchsize`           | `integer` |           | An integer value that specifies the number of records to be retrieved at a single instance. |
| `lazy`                | `boolean` | `true`    | Whether loading is to be done lazily or not. |
| `rowid`               | `string`  |           | Specify the row id |
| `discriminatorColumn` | `string`  |           | Use this attribute to define the discriminator column to be used in inheritance mapping |
| `discriminatorValue`  | `string`  |           | Use this attribute to define the discriminator value to be used in inheritance mapping |
| `joinColumn`          | `string`  |           | Define a join column for inheritance mapping |
| `embedded`            | `boolean` |           | Marks CFC as embedded, used when a CFC has an embedded object which also needs to be persisted along with the parent's data |
| `cacheUse`            | `string`  |           | Specify the caching strategy to be used for caching this component's data in the secondary cache: `read-only`|`nonstrict-read-writ    e`|`read-write`|`transactional` |
| `cacheName`           | `string`  |           | Specify the name of the secondary cache |
| `saveMapping`         | `boolean` | `false`   | Specifies whether the generated Hibernate mapping file has to be saved to disk. If you set the value to true, the Hibernate mapping XML file is saved as `{CFC name}.hbm.xml` in the same directory as the CFC. |