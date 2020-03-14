# wiki
Knowledge base


## Transactions


### ACID
ACID (Atomicity, Consistency, Isolation, and Durability) - acronym for safety guarantees provided by transactions. Mostly a marketing term, because it doesn't describe certain requierments.

*Atomicity* - Sequence of related queries applied all together or nothing. By contrast, in the context of ACID, atomicity is not about concurrency. It does not describe what happens if several processes try to access the same data at the same time, because that is covered under the letter I, for isolation

*Consistency* - The idea of ACID consistency is that you have certain statements about your data (invariants) that must always be true—for example, in an accounting system, credits and debits across all accounts must always be balanced.

*Isolation* - concurrently executing transactions are isolated from each other: they cannot step on each other’s toes.

*Durability* - is the promise that once a transaction has committed successfully, any data it has written will not be forgotten, even if there is a hardware fault or the database crashes.
