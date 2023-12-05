---
description: Learn transaction management with the ORM Extension
---

# Transactions

A transaction is any discrete unit of work used to pool database queries and statements to execute at once. This helps us to prevent a failed update from leaving the database in a broken state.

To denote a transaction, we wrap it in the `transaction{}` tag:

```js
transaction{
    // queries go here
}
```

The transaction will automatically commit (persist) at the end of the transaction block.

## Transaction Rollback

{% hint style="info" %}
This section is missing documentation - would you care to [add it yourself](transactions.md)?
{% endhint %}

## Transaction Commit

{% hint style="info" %}
This section is missing documentation - would you care to [add it yourself](transactions.md)?
{% endhint %}

## Transaction Savepoint

Savepoints are not _currently_ supported on ORM transactions.

{% hint style="info" %}
Looking for ORM savepoint support? [Contact our Support team to consider sponsoring this feature](https://www.ortussolutions.com/products/orm-extension#support).
{% endhint %}
