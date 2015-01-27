Beginning SQL
=============

Relational databases store their information in **tables**, which have rows and columns. Each column has a **name** and a **data type**. The name describes to the programmer or user what data go in the column and acts as a sort of handle to get to the data in the column. The type enforces what can get put into the column, and informs programs of what type the data should be when it's retrieved. Columns are defined upon creation of a table, and while it is possible to add, remove, or change columns, that can be tricky and usually indicates the emergence of an unforeseen application requirement.

A row is a piece of data that conforms to the column header. Each row contains a value under each column that is of the column's type, or a special value called `NULL` that essentially means there's no data in this row for that column. Practical constraints aside, a table can have any number of rows, and they can be added, removed, or changed at will.

Let's look at a table:

```
csci330_tgp=# SELECT * FROM unices;
          distro          | major_version | minor_version |    release_date     
--------------------------+---------------+---------------+---------------------
 FreeBSD                  |             8 |             4 | 2013-06-02 00:00:00
 FreeBSD                  |             9 |             3 | 2014-07-08 00:00:00
 FreeBSD                  |            10 |             1 | 2014-11-06 00:00:00
 Mac OS X                 |            10 |             9 | 2013-10-22 00:00:00
 Mac OS X                 |            10 |            10 | 2014-10-16 00:00:00
 Debian                   |             7 |             0 | 2013-05-04 00:00:00
 Debian                   |             7 |             4 | 2014-02-08 00:00:00
 Debian                   |             7 |             7 | 2014-10-18 00:00:00
 Red Hat Enterprise Linux |             6 |             0 | 2010-11-09 00:00:00
 Red Hat Enterprise Linux |             6 |             5 | 2013-11-21 00:00:00
 Red Hat Enterprise Linux |             6 |             6 | 2014-10-14 00:00:00
 Red Hat Enterprise Linux |             7 |             0 | 2014-06-09 00:00:00
 Ubuntu                   |            12 |             4 | 2012-04-26 00:00:00
 Ubuntu                   |            13 |             4 | 2013-04-25 00:00:00
 Ubuntu                   |            13 |            10 | 2013-10-17 00:00:00
 Ubuntu                   |            14 |             4 | 2014-04-17 00:00:00
 Ubuntu                   |            14 |            10 | 2014-10-23 00:00:00
(17 rows)
```

*A quick note before we go further: the SQL syntax (`SELECT`, `FROM`, and so forth) is case insensitive, though depending on the database system, table names and column names typically aren't. Using all-caps helps the language elements stand out more, but it's just a matter of style preference.*

SELECT and FROM
---------------

The query above is `SELECT * FROM unices` -- before that on the line is the prompt, and after that (the semicolon) indicates the query is done. This is the simplest query in SQL: every query needs a `SELECT` clause and a `FROM` clause. The `SELECT` describes what columns will be in the result, and the `FROM` describes what table the rows and columns in the result are coming from. Here, the table is called `unices` (a plural of "unix", pronounced like "vertices").

The `*` has a special meaning that indicates that all columns in the table will be shown in the result. If we want to just get certain columns, or if we want them returned in a certain order, we can specify them by name:

```
csci330_tgp=# SELECT major_version, minor_version, distro FROM unices;
 major_version | minor_version |          distro          
---------------+---------------+--------------------------
             8 |             4 | FreeBSD
             9 |             3 | FreeBSD
            10 |             1 | FreeBSD
            10 |             9 | Mac OS X
            10 |            10 | Mac OS X
             7 |             0 | Debian
             7 |             4 | Debian
             7 |             7 | Debian
             6 |             0 | Red Hat Enterprise Linux
             6 |             5 | Red Hat Enterprise Linux
             6 |             6 | Red Hat Enterprise Linux
             7 |             0 | Red Hat Enterprise Linux
            12 |             4 | Ubuntu
            13 |             4 | Ubuntu
            13 |            10 | Ubuntu
            14 |             4 | Ubuntu
            14 |            10 | Ubuntu
(17 rows)
```

ORDER BY
--------

You may have noticed that above, the rows got returned in the same order as the last time. In this case, it's just the order the rows got added to the table, but the database could have returned the rows in any arbitrary order it wanted to. If you want to enforce an ordering by sorting on a column, tack an `ORDER BY` on to the end of a query:

```
csci330_tgp=# SELECT distro, major_version, minor_version FROM unices ORDER BY major_version;
          distro          | major_version | minor_version 
--------------------------+---------------+---------------
 Red Hat Enterprise Linux |             6 |             5
 Red Hat Enterprise Linux |             6 |             6
 Red Hat Enterprise Linux |             6 |             0
 Debian                   |             7 |             7
 Debian                   |             7 |             4
 Red Hat Enterprise Linux |             7 |             0
 Debian                   |             7 |             0
 FreeBSD                  |             8 |             4
 FreeBSD                  |             9 |             3
 Mac OS X                 |            10 |            10
 Mac OS X                 |            10 |             9
 FreeBSD                  |            10 |             1
 Ubuntu                   |            12 |             4
 Ubuntu                   |            13 |             4
 Ubuntu                   |            13 |            10
 Ubuntu                   |            14 |             4
 Ubuntu                   |            14 |            10
(17 rows)
```

You can sort by multiple columns in case multiple rows have the same value in a column:

```
csci330_tgp=# SELECT distro, major_version, minor_version FROM unices ORDER BY major_version, minor_version;
          distro          | major_version | minor_version 
--------------------------+---------------+---------------
 Red Hat Enterprise Linux |             6 |             0
 Red Hat Enterprise Linux |             6 |             5
 Red Hat Enterprise Linux |             6 |             6
 Red Hat Enterprise Linux |             7 |             0
 Debian                   |             7 |             0
 Debian                   |             7 |             4
 Debian                   |             7 |             7
 FreeBSD                  |             8 |             4
 FreeBSD                  |             9 |             3
 FreeBSD                  |            10 |             1
 Mac OS X                 |            10 |             9
 Mac OS X                 |            10 |            10
 Ubuntu                   |            12 |             4
 Ubuntu                   |            13 |             4
 Ubuntu                   |            13 |            10
 Ubuntu                   |            14 |             4
 Ubuntu                   |            14 |            10
(17 rows)
```

To reverse sorting order, put `DESC` after the column name you're `ORDER`ing `BY`:

```
csci330_tgp=# SELECT distro, major_version, minor_version FROM unices ORDER BY major_version DESC, minor_version DESC;
          distro          | major_version | minor_version 
--------------------------+---------------+---------------
 Ubuntu                   |            14 |            10
 Ubuntu                   |            14 |             4
 Ubuntu                   |            13 |            10
 Ubuntu                   |            13 |             4
 Ubuntu                   |            12 |             4
 Mac OS X                 |            10 |            10
 Mac OS X                 |            10 |             9
 FreeBSD                  |            10 |             1
 FreeBSD                  |             9 |             3
 FreeBSD                  |             8 |             4
 Debian                   |             7 |             7
 Debian                   |             7 |             4
 Debian                   |             7 |             0
 Red Hat Enterprise Linux |             7 |             0
 Red Hat Enterprise Linux |             6 |             6
 Red Hat Enterprise Linux |             6 |             5
 Red Hat Enterprise Linux |             6 |             0
(17 rows)
```

You can even `ORDER BY` columns that are in the table in your `FROM` clause, but haven't been `SELECT`ed:

```
csci330_tgp=# SELECT distro, major_version, minor_version FROM unices ORDER BY release_date DESC;
          distro          | major_version | minor_version 
--------------------------+---------------+---------------
 FreeBSD                  |            10 |             1
 Ubuntu                   |            14 |            10
 Debian                   |             7 |             7
 Mac OS X                 |            10 |            10
 Red Hat Enterprise Linux |             6 |             6
 FreeBSD                  |             9 |             3
 Red Hat Enterprise Linux |             7 |             0
 Ubuntu                   |            14 |             4
 Debian                   |             7 |             4
 Red Hat Enterprise Linux |             6 |             5
 Mac OS X                 |            10 |             9
 Ubuntu                   |            13 |            10
 FreeBSD                  |             8 |             4
 Debian                   |             7 |             0
 Ubuntu                   |            13 |             4
 Ubuntu                   |            12 |             4
 Red Hat Enterprise Linux |             6 |             0
(17 rows)
```

LIMIT
-----

To only return the first *n* rows, use `LIMIT`:

```
csci330_tgp=# SELECT distro, major_version, minor_version FROM unices ORDER BY release_date DESC LIMIT 5;
          distro          | major_version | minor_version 
--------------------------+---------------+---------------
 FreeBSD                  |            10 |             1
 Ubuntu                   |            14 |            10
 Debian                   |             7 |             7
 Mac OS X                 |            10 |            10
 Red Hat Enterprise Linux |             6 |             6
(5 rows)
```

WHERE
-----

The `WHERE` clause is extremely important to know. It's how you specify what rows should be in the result set based on their column values, so in that sense, it acts like a filter. Here's a query with a simple `WHERE`:

```
csci330_tgp=# SELECT * FROM unices WHERE distro = 'FreeBSD';
 distro  | major_version | minor_version |    release_date     
---------+---------------+---------------+---------------------
 FreeBSD |             8 |             4 | 2013-06-02 00:00:00
 FreeBSD |             9 |             3 | 2014-07-08 00:00:00
 FreeBSD |            10 |             1 | 2014-11-06 00:00:00
(3 rows)
```

That query only returned rows where, you guessed it, the "distro" field was "FreeBSD". Let's do a more complex one:

```
csci330_tgp=# SELECT * FROM unices WHERE release_date > '2014-01-01' AND (major_version > minor_version + 5 OR distro != 'Ubuntu');
          distro          | major_version | minor_version |    release_date     
--------------------------+---------------+---------------+---------------------
 FreeBSD                  |             9 |             3 | 2014-07-08 00:00:00
 FreeBSD                  |            10 |             1 | 2014-11-06 00:00:00
 Mac OS X                 |            10 |            10 | 2014-10-16 00:00:00
 Debian                   |             7 |             4 | 2014-02-08 00:00:00
 Debian                   |             7 |             7 | 2014-10-18 00:00:00
 Red Hat Enterprise Linux |             6 |             6 | 2014-10-14 00:00:00
 Red Hat Enterprise Linux |             7 |             0 | 2014-06-09 00:00:00
 Ubuntu                   |            14 |             4 | 2014-04-17 00:00:00
(8 rows)
```

It's a bit of a silly query, but it illustrates some features:

- Equality/inequality tests (`=`, `!=`, `<`, `>`, `<=`, `>=`)
- Boolean logic (`AND`, `OR`)
- Grouping (parentheses)
- Simple arithmetic

Your turn
---------

- Translate the above queries into normal English.
- Think of some queries (in English) you could run on the table in this section, and translate them into SQL.
