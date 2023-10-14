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