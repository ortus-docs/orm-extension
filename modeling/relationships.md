---
description: Entity relationships let you define an association between two entity types.
---

# Relationships

## Relationships

Every relationship property must define the state of the relationship. In each case, the relationship property is defined in an entity which represents the "left" side of the relationship. If you bring a `Posts` relationship into the `User` entity, then from the `User` entity, the `User` is the left side of the relationship, and `Posts` is the right.

## One To One

A one to one relationship couples a single row on the left side to a single row on the right side:

```js
property name="Contact"
    fieldtype="one-to-one"
    cfc="Contact";
```

One to one relationships can be seen as simply extending the entity with additional information. Since there is no possibility of multiple records per entity instance, it may be worthwhile to set `lazy=false` to fetch the related entity along with any entity load:

```js
property name="Contact"
    fieldtype="one-to-one"
    cfc="Contact"
    lazy="false";
```

## One To Many

A one to many relationship couples a single row on the left side (the "one") to multiple rows on the right side (the "many"):

```js
component entityName="User" persistent="true"{
    property name="posts"
        fieldtype="one-to-many"
        cfc="Post";
}
```

You'll normally want to set `lazy="true"` to (for example) avoid fetching every Post on a User:

```js
property name="posts"
    fieldtype="one-to-many"
    cfc="Post"
    lazy="true";
```

## Many To One

A many to one relationship couples multiple rows on the left side (the "many") to a single row on the right side( the "one"):

```js
component entityName="Post" persistent="true"{
    property name="Authors"
        fieldtype="many-to-one"
        cfc="User";
}
```

Thus, a single Post can have only one Author... but an author (or a User, really) can have many Posts.

## Many To Many

A many to many relationship allows each entity to relate to multiple rows on the opposite side. A good example might be a blog which allows multiple authors for a single blog post. Each blog post can then have multiple authors, and each author has (likely) written multiple blog posts:

```js
component entityName="User" persistent="true"{
    property name="posts"
        fieldtype="many-to-many"
        cfc="Post"
        linktable="user_posts_link";
}
```

The `linktable` attribute is required on a `many-to-many` property to set the locationfor storing join records. You can further alter the storage location via `linkschema` and `linkcatalog`:

```js
property name="posts"
    fieldtype="many-to-many"
    cfc="Post";
    linkschema="blog"
    linkcatalog="dbo";
```

### Singular Name

On many\* relationships like `one-to-many`, `many-to-one`, etc., you'll be manipulating the full set of items via the property name: `hasAuthors()`, `setAuthors()`, etc. However, this plural terminology becomes weird when used on a single item addition or removal, such as `addAuthors( Author )`. For this reason, you can define a `singularName=STRING` attribute to clean up your entity manipulation:

```js
property name="Authors"
    singularName="Author"
    fieldtype="many-to-one"
    cfc="User";
```

### Lazy

Man, you wanna get lazy? How about don't-fetch-the-data-until-you-need-it kinda lazy?

Using `lazy=true`, we can tell Hibernate not to fetch the relational data _unless_ and _until_ a method call such as `Authors()` attempts to load it. This greatly improves performance on page requests which do not need that particular data:

```js
property name="posts"
    fieldtype="one-to-many"
    cfc="Post"
    lazy="true";
```

We can also use `lazy=extra` to only retrieve the rows that we touch. This may work well if we commonly only access a few rows out of the full set of child items:

```js
property name="posts"
    fieldtype="one-to-many"
    cfc="Post"
    lazy="extra";
```

### Relationship Methods

{% hint style="info" %}
This section is missing documentation - would you care to [add it yourself](http://127.0.0.1:5000/s/vcvOjwmew3Y3IdvJ8jNG/guide/relationships/relationship-types/belongsto)?
{% endhint %}
