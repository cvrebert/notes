(Postgres fixes at least some of these.)

* No first-class list/array support
* Having to manually specify `JOIN` conditions, when very often there's only 1 sensible way to do the JOIN
* SQL's syntax isn't nicely composable.
  * e.g. I can't just tack on another `WHERE` clause to filter things further, the clauses must appear in a specific order, etc.
  * I mean, you could use lost of nested subqueries, but it's fugly and probably doesn't optimize well.
* Quoting of names varies by SQL implementation; e.g. `[MyArbitrarilyNamedTable]` in MS SQL Server vs. `` `MyArbitrarilyNamedTable` `` in MySQL
* Column type definitions default to nullable, implicitly.
* Too easy to accidentally write an unindexed query; should issue a warning which can be upgraded to an error via configuration
* Awkwardness of "backwards" JOINs
* MySQL doesn't default to UTF-8 encoding for strings; it uses Latin-1...
* MySQL doesn't default to UTC timezone
* MySQL has several layers of timezone settings: system, server, and connection timezones
* Audit logging not built-in
* Soft deletion not built-in
