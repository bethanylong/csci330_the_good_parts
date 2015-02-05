Adding and modifying data in tables
===================================

So far, we've created schemas and looked at (`SELECT`ed) the data they hold, but we haven't actually manipulated the data yet. That's what we'll learn in this section.

INSERT
------

Use `INSERT` to add a row to a table:

```
csci330_tgp=# INSERT INTO unices (distro, major_version, minor_version, release_date) VALUES ('Research Unix', 7, NULL, '1979-01-01')
csci330_tgp=# INSERT INTO unices (distro, major_version, minor_version, release_date) VALUES ('CSRG BSD', 4, 3, '1986-06-01')
csci330_tgp=# INSERT INTO unices (distro, major_version, minor_version, release_date) VALUES ('AT&T System V', 4, 0, '1988-10-18')
```

The first set of parentheses specifies columns, and the second set gives the values under those respective columns. As long as the schema accomodates doing so (such as with `DEFAULT` values), you don't have to explicitly `INSERT` into every column.

UPDATE
------

DELETE
------
