CSCI 330: The Good Parts
========================

Databases are used *everywhere*. Their ubiquity and significance are convincing enough to most computer science students that they realize that database skills will help them get ahead. However, official database curricula occasionally miss the mark as far as inspiring confidence, providing context, and ensuring competence go.

The name of this project is a nod to *[JavaScript: The Good Parts](http://shop.oreilly.com/product/9780596517748.do)*, which is an excellent (and short) book. People who aren't terribly fond of JS tend to conclude that the book's brevity is because there aren't enough good parts in the language to make the book bigger. Another possible reason is that the book focuses on being concise and conveying the relevant information needed to write good code in JS. 

The instructional text in this project is likely to be brief for both of those reasons as well. Our scope will exclude many of the more regrettable portions of the canonical course while including more material that fits a 21st century perspective. Our goal is to provide our peers with direly-needed guidance and perspectives on modern databases in a readable, understandable manner.

**Pull requests, issues, reviews, suggestions, and other contributions are extremely welcome.**

Targets
-------

**General**:
- Interesting, sane examples
- Projects with real-world applications
- Build practical confidence before moving to more arcane topics
- Promote full-spectrum confidence about databases -- from installing dependencies, to writing code, to hitting F5 in your browser and not seeing errors
- Don't ignore security
- Explain *why* one would use a feature/strategy/system, rather than presenting options without context
- Prefer a link to official documentation and a brief summary here, rather than rehashing the entire documentation here

**Relational databases**:
- Simple SQL intro (`SELECT`, `FROM`, `WHERE`, `ORDER BY`, ...)
- Brief description of relations, and their role in modern RDBMSs
    - Things that real databases allow but relations don't (i.e. duplicate rows)
- Creating and modifying databases/tables/schemas
    - Column types and constraints
    - The `DROP` idiom, and `DROP` versus `DELETE`
- Composing more complex queries with `WITH` and nested queries
- Tables as sets, and how/why to do set operations
- Joins, and how to avoid doing them by hand
- Aggregates, and `GROUP BY`/`HAVING`
- Good design
    - Views
    - Normalization
    - Foreign keys, primary keys, and enforcement of constraints
    - Indexing
- Basic administration/ops
    - Setup
    - Security
    - Reliability/ACID
- ORM systems like SQLAlchemy
- Systems, and their cool features/advantages:
    - SQLite
    - Postgres (jsonb type blurring the lines between relational and non-relational)

**Non-relational databases**
- What on earth is NoSQL?
    - Different categories of non-relational DBs: document, key-value store, wide column, graph, others?
    - Use cases, advantages/disadvantages, CAP theorem, BASE
- Systems, and their cool features/advantages:
    - Mongo
    - Redis
    - Cassandra
    - Neo4J

**Projects**
- At least one project suggestion for each of the relational or non-relational systems mentioned
- This project doesn't have real assignments used in real classes, so they can go on people's public GitHub accounts!
