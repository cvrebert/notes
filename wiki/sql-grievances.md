(Postgres fixes at least some of these. I've only had hands-on experience with MySQL.)

* No first-class list/array support
  * [SQLAlchemy workaround](http://docs.sqlalchemy.org/en/latest/orm/extensions/orderinglist.html)
* Having to manually specify `JOIN` conditions, when very often there's only 1 sensible way to do the JOIN
* SQL's syntax isn't nicely composable.
  * e.g. I can't just tack on another `WHERE` clause to filter things further, the clauses must appear in a specific order, etc.
  * I mean, you could use lots of nested subqueries, but it's fugly and probably doesn't optimize well.
* Quoting of names varies by SQL implementation; e.g. `[MyArbitrarilyNamedTable]` in MS SQL Server vs. `` `MyArbitrarilyNamedTable` `` in MySQL
* Column type definitions default to nullable, implicitly.
* Too easy to accidentally write an unindexed query; should issue a warning which can be upgraded to an error via configuration
  * [Coping mechanism](http://danbirken.com/quicktip/2014/04/16/improve-developer-habits-with-db-diagnostisc.html)
* Awkwardness of "backwards" JOINs
* MySQL doesn't default to UTF-8 encoding for strings; it uses Latin-1...
* MySQL doesn't default to UTC timezone
* MySQL has several layers of timezone settings: system, server, and connection timezones
* [Terrible choices: MySQL](http://blog.ionelmc.ro/2014/12/28/terrible-choices-mysql/)
* [MySQL? Choose something else.](http://grimoire.ca/mysql/choose-something-else)
* Audit logging not built-in
* Soft deletion not built-in
* Trailing/leading spaces in text fields
* Trees are kinda cumbersome
  * However: [Representing Trees in PostgreSQL](https://woss.name/articles/representing-trees-in-postgresql/) ([HN](https://news.ycombinator.com/item?id=8642035))
* SQL is not the last word in databases
  * [Immutable databases and automatic caching](http://blog.confluent.io/2015/03/04/turning-the-database-inside-out-with-apache-samza/)
