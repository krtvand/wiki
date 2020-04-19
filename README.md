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

#### Read Committed

Read committed is a very popular isolation level. It is the default setting in Oracle 11g, PostgreSQL, SQL Server 2012, MemSQL, and many other databases

It makes two guarantees:
 - When reading from the database, you will only see data that has been committed (no dirty reads).
 - When writing to the database, you will only overwrite data that has been committed (no dirty writes).
 
 *Dirty reads* - Imagine a transaction has written some data to the database, but the transaction has not yet committed or aborted. Can another transaction see that uncommitted data? If yes, that is called a dirty read.

*Dirty writes* - For example, in car sales website on which two people, Alice and Bob, are simultaneously trying to buy the same car. Buying a car requires two database writes: the listing on the website needs to be updated to reflect the buyer, and the sales invoice needs to be sent to the buyer. In the case of Figure 7-5, the sale is awarded to Bob (because he performs the winning update to the listings table), but the invoice is sent to Alice (because she performs the winning update to the invoices table).

##### Implementing read committed
preventing *dirty writes* - most commonly, databases  by using row-level locks.
# TODO preventing *dirty reads* - most databases prevent dirty reads using the approach illustrated in
Figure 7-4: for every object that is written, the database remembers both the old com‐
mitted value and the new value set by the transaction that currently holds the write
lock. While the transaction is ongoing, any other transactions that read the object are
simply given the old value. Only when the new value is committed do transactions
switch over to reading the new value.


## SOLID principles

### I - interface segregation. 

Robert C. Martin defined as 
> Clients should not be forced to depend upon interfaces that they do not use.

detail explanation: https://stackify.com/interface-segregation-principle/

example where principle violated:
```python
class CoffeeMachine:
  def brewFilterCoffee():
  def brewEspresso():
  def addGroundCoffee():
  
class BasicCoffeeMachine(CoffeeMachine):
  def brewEspresso():
    raise NotAllowed()
  def brewFilterCoffee():
    do job
    
class EspressoCoffeeMachine(CoffeeMachine):
  def brewEspresso():
    do job
    
  def brewFilterCoffee():
    raise NotAllowed()
  
```
The problem is that the CoffeeMachine interface will change if the signature of the brewFilterCoffee method of the BasicCoffeeMachine method changes. That will also require a change in the EspressoMachine class and all other classes that use the EspressoMachine, even so, the brewFilterCoffee method doesn’t provide any functionality and they don’t call it.
