Relations
=========

As the name suggests, relational database management systems (RDBMSs) conform mostly to what's known as the **relational model**. Relations are a mathematical concept that you can think of (in this context) as a subset of the Cartesian product of some number of sets.

Okay, that wasn't helpful. Let's back up a bit.

Sets
----

A [set](http://en.wikipedia.org/wiki/Set_%28mathematics%29) is a collection of unique objects and does not have any inherent order. Some examples of sets:

- letters in the English alphabet
- positive integers
- students in a class
- ice cream flavors
- latitude numbers
- longitude numbers
- other sets (that is, nested sets)

A subset is just a set that doesn't contain any members not in its parent set. This means a subset could be some selection of elements of the parent set, or a set with no elements (the "empty set"), or the same set as the parent set, but **not** a set with an element that's not in the parent set.

Cartesian product
-----------------

A [Cartesian product](http://en.wikipedia.org/wiki/Cartesian_product) of sets, say, *A* and *B*, is the set of all combinations of each member of *A* and each member of *B*. Each member of the Cartesian product is an ordered [tuple](http://en.wikipedia.org/wiki/Tuple) with one element from each input set. So, if *A* has 8 members and *B* has 11 members, their Cartesian product will have 88 members, each of which is an ordered pair like (*A*-element, *B*-element).

As a more concrete example, think of the game Battleship. The set of rows is letters A through J, and the set of columns is integers 1 through 10. You say your moves as, for instance, "D5" or "A9". The set of all possible moves is the Cartesian product of the set of rows and the set of columns, and its elements are A1, A2, A3, ... J10. You can visualize it as having an element for each square on the board.

Circling back to the definition of relations at the beginning of this section, you could describe certain relations on a Battleship board verbally as "squares in rows above E", "squares in odd-numbered columns in rows H through J", or "squares currently occupied by my aircraft carrier". Each of these sets of squares is a subset of all the squares on the board -- a subset of the Cartesian product of the set of rows and the set of columns.

Databases vs. relations
-----------------------

In the previous section, we described columns as having types, and rows as conforming to the column header. So, from the perspective of relations, the types of columns in a table (text, numbers, dates, and so on) are sets of values the columns are allowed to contain. The Cartesian product of these sets is then the set of all possible rows that could ever be in that table, and the rows actually in the table form a subset of that Cartesian product -- a relation!

This can be a helpful way to reason about database tables, but it doesn't conform perfectly to reality. The most notable example of this is that popular RDBMSs allow duplicate rows, whereas elements in a set are unique.
