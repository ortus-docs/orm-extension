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

## Transaction Commit

## Transaction Savepoint

Savepoints are not *currently* supported on ORM transactions.

{% hint style="info" %}
Looking for ORM savepoint support? [Contact our Support team to consider sponsoring this feature](https://www.ortussolutions.com/products/orm-extension#support).
{% endhint %}