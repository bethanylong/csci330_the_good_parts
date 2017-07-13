.. highlight:: sql

Adding and modifying data in tables
===================================

So far, we've created schemas and looked at the data they hold, but we haven't
actually manipulated the data yet. That's what we'll learn in this section.

INSERT
------

Use ``INSERT`` to add a row to a table::

    csci330_tgp=# INSERT INTO unices (distro, major_version, minor_version, release_date) VALUES ('Research Unix', 7, NULL, '1979-01-01')
    csci330_tgp=# INSERT INTO unices (distro, major_version, minor_version, release_date) VALUES ('CSRG BSD', 4, 3, '1986-06-01')
    csci330_tgp=# INSERT INTO unices (distro, major_version, minor_version, release_date) VALUES ('AT&T System V', 4, 0, '1988-10-18')

The first set of parentheses specifies columns, and the second set gives the
values under those respective columns. As long as the schema accomodates doing
so (such as with ``DEFAULT`` values), you don't have to explicitly ``INSERT``
into every column::

    csci330_tgp=# INSERT INTO unices (distro, major_version, release_date) VALUES ('Research Unix', 7, '1979-01-01')

UPDATE
------

Use ``UPDATE`` to modify rows that already exist.

::

    csci330_tgp=# UPDATE unices SET minor_version = 0 WHERE distro = 'Research Unix' AND major_version = 7;
    csci330_tgp=# UPDATE unices SET distro = 'Ooboontoo' WHERE distro = 'Ubuntu';

The targeting (so to speak) for ``UPDATE`` is based on the ``WHERE`` clause:
the ``UPDATE`` will modify all rows where the ``WHERE`` clause applies. If you
have an ``UPDATE`` without a ``WHERE``, it'll modify all the rows in the table!

DELETE
------

Use ``DELETE`` to destroy rows.

::

    csci330_tgp=# DELETE FROM unices WHERE release_date < '2014-01-01';
    csci330_tgp=# DELETE FROM unices WHERE distro = 'Mac OS X' OR distro = 'Red Hat Enterprise Linux';

Just like ``UPDATE``, if you don't provide a ``WHERE`` with your ``DELETE``,
you'll destroy all the rows in the table!
