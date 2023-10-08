---
description: All about entity identifiers, from primary keys, and generators to composite keys and field types.
---

# Identifiers

Identifier properties are denoted via `fieldtype="id"`.

We highly recommend disabling updates on identifier properties via `update="false"`:

```js
property name="id"
            fieldtype="id"
            ormtype="string"
            generator="assigned"
            update="false";
```

## Common Generator Types

### Assigned Generator

The Assigned generator is the default identifier generator type, and simply allows the application (your CFML) to assign identifier values prior to insertion. You can think of this as `generator=none`.

> lets the application assign an identifier to the object before save() is called. This is the default strategy if no <generator> element is specified. - _[Hibernate 3.3 mapping reference docs](https://docs.jboss.org/hibernate/core/3.3/reference/en/html/mapping.html#mapping-declaration-id-generator)_

```js
property name="id"
            fieldtype="id"
            generator="assigned"
            update="false";
```

Assigned generators will commonly use [a `preInsert()` event listener](../usage/events.md#entity-event-handler) to assign the identifer value:

```js
function preInsert( entity ){
    setId( createUUID() );
}
```

### Select Generator

A select generator will attempt to select the next identifier value from the specified `selectKey` column:

> retrieves a primary key, assigned by a database trigger, by selecting the row by some unique key and retrieving the primary key value. - _[Hibernate 3.3 mapping reference docs](https://docs.jboss.org/hibernate/core/3.3/reference/en/html/mapping.html#mapping-declaration-id-generator)_

```js
property name="userID"
            fieldtype="id"
            generator="select"
            selectKey="ssn"
            update="false";
```

### UUID Generator

The UUID generator uses Hibernate's uuid generator under the hood:

> uses a 128-bit UUID algorithm to generate identifiers of type string that are unique within a network (the IP address is used). The UUID is encoded as a string of 32 hexadecimal digits in length. - _[Hibernate 3.3 mapping reference docs](https://docs.jboss.org/hibernate/core/3.3/reference/en/html/mapping.html#mapping-declaration-id-generator)_

```js
property name="userID"
            fieldtype="id"
            generator="uuid"
            update="false";
```

### Increment Generator

The Increment generator uses a simple incrementing value to create identifiers. Do not use in concurrent applications, as the values may no longer be unique.

> Generates identifiers of type long, short or int that are unique only when no other process is inserting data into the same table. Do not use in a cluster. - _[Hibernate 3.3 mapping reference docs](https://docs.jboss.org/hibernate/core/3.3/reference/en/html/mapping.html#mapping-declaration-id-generator)_

```js
property name="userID"
            fieldtype="id"
            generator="guid"
            update="false";
```