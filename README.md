#Introduction

The purpose of **bookwerx-core** is to provide an API that supports multi-currency
 bookkeeping, using the good-ole double-entry model, slightly adapted to squeeze 
 in multiple currencies.  It uses [node](https://nodejs.org), [express](http://expressjs.com/), and [mongodb](https://www.mongodb.com/).

Any application that deals with "money" (fiat, precious metals, cryptocoins) will
quickly encounter the need for bookkeeping.  Rolling your own methods are as usual,
 easier said than done, so perhaps  you can save yourself some grief and enjoy **bookwerx-core** instead.

With this API, the user can:

* Perform ordinary CRUD operations on the various bookkeeping objects,
such as accounts and transactions.

* Perform consistency checks.

* Brainwipe and start over.

This API is the minimum necessary to populate your db with bookkeeping information,
ensure that it is internally consistent, and nuke it from orbit and start over if necessary.

A package that provides a web-based front-end using Angular 2 can be found at [bookwerx-ui]
(http://github.com/bostontrader/bookwerx-reporting) and for more sophisticated analysis, 
such as the production of financial reports and graphing, please see 
 [bookwerx-reporting](http://github.com/bostontrader/bookwerx-reporting).



##Getting Started

1. You will need node and npm.

2. You will need git.

3. You will need mongodb.

4. git clone https://github.com/bostontrader/bookwerx-core-express.git

5. From inside the bookwerx-core-express directory: npm install


##Multi-Currencies

This package enables the user to maintain a list of currencies relevant to their app.
Fiat, precious metals, and cryptocoins are three obvious examples of currencies that
this app could easily handle.

The "distributions" of a transaction (the debits and credits part) are all tagged
with a currency and a single transaction can include one or two different
currencies.

Currency exchanges can easily be recorded simply by debiting one currency and
crediting the other.

##Data Analysis

As mentioned earlier, this package merely records the basic bookkeeping objects.
More sophisticated analysis belongs in other packages such as
[bookwerx-reporting](http://github.com/bostontrader/bookwerx-reporting).  "What actually happened" (the transactions) belong here.
But "what does any of this mean" belongs elsewhere.

The ordinary debits==credits rule applies for any transaction that only deals
 with a single currency.  That is a consistency check that belongs with this package.

A transaction that involves two currencies is considered a currency exchange.
Although the actual dr and cr numbers will no longer "balance", if we consider
them to be equivalent amounts then we can compute exchange rate information.
This however is a job for other packages such as [bookwerx-reporting](http://github.com/bostontrader/bookwerx-reporting).

##API Notes
1. All API calls return JSON.
2. Any call that returns JSON containing a key
entitled 'error' did not succeed.  Please scrutinize the
value of 'error' for clues about the problem.
3. Any GET that is successful will return what you expect.
4. Any call that is _not_ GET and _is_ successful will
return {"result":"ok"}
