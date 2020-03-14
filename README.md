# wiki
Knowledge base


## Transactions


### ACID
ACID (Atomicity, Consistency, Isolation, and Durability) - acronym for safety guarantees provided by transactions. Mostly a marketing term, because it doesn't describe certain requierments.

*Atomicity* - If an error occurs halfway through a sequence of writes, the transaction should be aborted, and the writes made up to that point should be discarded. In other words, the database saves you from having to worry about partial failure, by giving an all-or-nothing guarantee. By contrast, in the context of ACID, atomicity is not about concurrency. It does not describe what happens if several processes try to access the same data at the same time, because that is covered under the letter I, for isolation

*Consistency* - The idea of ACID consistency is that you have certain statements about your data (invariants) that must always be true—for example, in an accounting system, credits and debits across all accounts must always be balanced.

*Isolation* - Concurrently running transactions shouldn’t interfere with each other. For example, if one transaction makes several writes, then another transaction should see either all or none of those writes, but not some subset.

*Durability* - is the promise that once a transaction has committed successfully, any data it has written will not be forgotten, even if there is a hardware fault or the database crashes.

### Isolation levels

####Read Committed####

It makes two guarantees:
 - When reading from the database, you will only see data that has been committed (no dirty reads).
 - When writing to the database, you will only overwrite data that has been committed (no dirty writes).
