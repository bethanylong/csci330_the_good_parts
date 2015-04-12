Aggregate functions
===================

RDBMSs provide a set of functions that can be computed over selected columns.
These are often used to compute statistics like average, minimum, and maximum
values::

    csci330_tgp=# SELECT avg(major_version) AS major, avg(minor_version) AS minor FROM unices;                                              
           major        |       minor        
    --------------------+--------------------
     9.3529411764705882 | 4.7647058823529412
    (1 row)

    csci330_tgp=# SELECT max(major_version) AS major, max(minor_version) AS minor FROM unices;                                              
     major | minor 
    -------+-------
        14 |    10
    (1 row)

    csci330_tgp=# SELECT min(major_version) AS major, min(minor_version) AS minor FROM unices;                                              
     major | minor 
    -------+-------
         6 |     0
    (1 row)

*Note: the AS after these column names wrapped in aggregate functions gives the
new name of the column in the result set.*

Aggregate functions apply after filtering with WHERE::

    csci330_tgp=# SELECT avg(major_version) AS major, avg(minor_version) AS minor FROM unices WHERE distro = 'Ubuntu';
            major        |       minor        
    ---------------------+--------------------
     13.2000000000000000 | 6.4000000000000000
    (1 row) 

Aggregates within buckets: GROUP BY
-----------------------------------

What if you don't want to compute statistics over all rows, but just rows that
share some value in a column? Well, you *could* run a query for each,
restricting the rows with ``WHERE some_column = 'some_value'``, but that would
be unpleasant.

Thankfully, this use case is what ``GROUP BY`` is for. This is an incredibly
powerful clause that separately computes aggregate functions for rows sharing
values in the column ``GROUP BY`` is given. The result has a row for each of
those values. The, ahem, *technical term* is "buckets".

::

    csci330_tgp=# SELECT distro, max(major_version) AS major, max(minor_version) AS minor FROM unices GROUP BY distro;                      
              distro          | major | minor 
    --------------------------+-------+-------
     FreeBSD                  |    10 |     4
     Debian                   |     7 |     7
     Red Hat Enterprise Linux |     7 |     6
     Mac OS X                 |    10 |    10
     Ubuntu                   |    14 |    10
    (5 rows)

Filtering after aggregating: HAVING
-----------------------------------

Sometimes, it's nice to have the option to filter results after a ``GROUP BY``.
*But wait*, you ask. *Isn't filtering what WHERE is for?* Actually, remember
that ``GROUP BY`` and aggregate functions happen after the ``WHERE`` clause. If,
for example, you were calculating the average of some column then doing a
``GROUP BY`` on another column, using ``WHERE`` for filtering would change the
set of values the average was computed over! Here's an example of a similar
situation::

    csci330_tgp=# SELECT distro, max(major_version) AS major, max(minor_version) AS minor FROM unices GROUP BY distro HAVING max(major_version) <= 8;                                                                                                                               
              distro          | major | minor 
    --------------------------+-------+-------
     Debian                   |     7 |     7
     Red Hat Enterprise Linux |     7 |     6
    (2 rows)

The ``HAVING`` clause in the above query filtered the results after the maximum
was computed. What if we (erroneously) tried to use ``WHERE`` to do the same
thing?

::

    csci330_tgp=# SELECT distro, max(major_version) AS major, max(minor_version) AS minor FROM unices WHERE major_version <= 8 GROUP BY distro;                                                                                                                                       
              distro          | major | minor 
    --------------------------+-------+-------
     FreeBSD                  |     8 |     4
     Debian                   |     7 |     7
     Red Hat Enterprise Linux |     7 |     6
    (3 rows)

In this case, the maximum was computed over rows that were already less than or
equal to 8 -- which is probably neither super helpful nor exactly what someone
writing this query would be expecting.
