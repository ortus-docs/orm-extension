# Entities

A persistent entity is a CFML component that is marked as a database entity via the `persistent` annotation upon the component definition:

```js
component persistent="true"{

}
```

By default, the entity name will be the CFC file name - minus the file extension, of course. We can modify the entity name via the `entityname` annotation:

```js
component persistent="true" entityname="Author" {

}
```

And the table name via the `table` annotation:

```js
component persistent="true" entityname="Author" table="authors" {

}
```

Here's the full list of available annotations for a persistent component:

<table data-full-width="true"><thead><tr><th width="235">Attribute</th><th width="111">Type</th><th width="107">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>persistent</code></td><td><code>boolean</code></td><td><code>false</code></td><td>Mark this component as an ORM entity</td></tr><tr><td><code>entityname</code></td><td><code>string</code></td><td></td><td>Set a custom entity name which is different than the CFC name</td></tr><tr><td><code>table</code></td><td><code>string</code></td><td></td><td>Specify the database table name</td></tr><tr><td><code>schema</code></td><td><code>string</code></td><td></td><td>Specify the database schema name.</td></tr><tr><td><code>catalog</code></td><td><code>string</code></td><td></td><td>Specify the database catalog name.</td></tr><tr><td><code>dynamicinsert</code></td><td></td><td></td><td>Specifies whether INSERT SQL is to be generated at runtime. Only those columns whose values are not null are included in the SQL.</td></tr><tr><td><code>dynamicinsert</code></td><td><code>boolean</code></td><td><code>false</code></td><td>Specifies whether INSERT SQL is to be generated at runtime. Only those columns whose values are not null are included in the SQL.</td></tr><tr><td><code>dynamicupdate</code></td><td><code>boolean</code></td><td><code>false</code></td><td>Specifies whether UPDATE SQL is to be generated at runtime. Only those columns whose values are not null are included in the SQL.</td></tr><tr><td><code>readonly</code></td><td><code>boolean</code></td><td><code>false</code></td><td>Specify whether table is readonly or not</td></tr><tr><td><code>selectbeforeupdate</code></td><td><code>boolean</code></td><td></td><td>Specify whether Hibernate should never perform an SQL UPDATE unless it is certain that an object is actually modified. In cases when a transient object is associated with a new session using update(), Hibernate performs an extra SQL SELECT to determine if an UPDATE is actually required.</td></tr><tr><td><code>optimisticlock</code></td><td><code>string</code></td><td></td><td>Determines the locking strategy. It can be any one of: <code>none</code></td></tr><tr><td><code>batchsize</code></td><td><code>integer</code></td><td></td><td>An integer value that specifies the number of records to be retrieved at a single instance.</td></tr><tr><td><code>lazy</code></td><td><code>boolean</code></td><td><code>true</code></td><td>Whether loading is to be done lazily or not.</td></tr><tr><td><code>rowid</code></td><td><code>string</code></td><td></td><td>Specify the row id</td></tr><tr><td><code>discriminatorColumn</code></td><td><code>string</code></td><td></td><td>Use this attribute to define the discriminator column to be used in inheritance mapping</td></tr><tr><td><code>discriminatorValue</code></td><td><code>string</code></td><td></td><td>Use this attribute to define the discriminator value to be used in inheritance mapping</td></tr><tr><td><code>joinColumn</code></td><td><code>string</code></td><td></td><td>Define a join column for inheritance mapping</td></tr><tr><td><code>embedded</code></td><td><code>boolean</code></td><td></td><td>Marks CFC as embedded, used when a CFC has an embedded object which also needs to be persisted along with the parent's data</td></tr><tr><td><code>cacheUse</code></td><td><code>string</code></td><td></td><td>Specify the caching strategy to be used for caching this component's data in the secondary cache: <code>read-only</code></td></tr><tr><td><code>cacheName</code></td><td><code>string</code></td><td></td><td>Specify the name of the secondary cache</td></tr><tr><td><code>saveMapping</code></td><td><code>boolean</code></td><td><code>false</code></td><td>Specifies whether the generated Hibernate mapping file has to be saved to disk. If you set the value to true, the Hibernate mapping XML file is saved as <code>{CFC name}.hbm.xml</code> in the same directory as the CFC.</td></tr></tbody></table>
