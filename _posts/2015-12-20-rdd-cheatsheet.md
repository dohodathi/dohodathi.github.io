---
title: Relational Database Design Cheatsheet
layout: post
description: "Relational Database Design Cheatsheet"
category: cheatsheet
tags: [sql]
author: hoffendahl
---

## General conventions

* Stick with lower case and underscore **or** CamelCase notation for any database object.
    
```sql
// Use
user_product // or ..
UserProduct
// Don't use
userproduct
USERPRODUCT
```

## Tables

- Use **nouns**.
- Use singular instead of plural.
    + The tablename refers to each **row** in the table.
Use prefixes on tables, where you expect a large number of tables in the database, **more then 100**, Calrify the subject area - of the table, for example HR_ for tables which are **only** used by the HR department.
- Do not use suffixes on tables. Only use them for non-table objects. (See [Suffixes](#Suffixes))
- Independent tables have a standalone name, like product, where dependent tables can have relational assigned names, like `user_product`, where a product only exists when a user exists.

```sql
// Tables
customer
product
HR_employee
```

## Relationships (between tables)

- Use verbs.
    + The relationships between the tables are the Actions that take place between the nouns.
    + The Verb Phrase is important during modelling because it assists in resolving the model, ie. clarifying relationships.
- Use those verbs for foreign keys.

```sql
// Tables
customer
sales_order
// Relation
customer initiates sales_order
// Foreign Key
customer_initiates_sales_order_fk
```

## Attributes

- Use the suffix `_id` on foreign key attributes.
- If you reference a table with mytable_id, use this notation on every other Foreign Key inside your database.
- Do not use prefixes of suffixes on non-foreign-key attributes.
- **Custom rule:** Use the column name title for tables with low column count (id and 1 to 2 further columns).
    + We do not use name for those columns, since "name" is widely used as a reserved keyword on databases. 

| language table | ||
|---|---|---|
|id | country_id | title |


## Schemas

- Open Architecture databases are supposed to be independent of the apps that use them, so **don't use schemas** (on tables) to declare app affiliations.
    + As databases grow, and more than the one app uses them, the naming will remain meaningfulwithout the need of correction.
    + Databases that are completely embedded in a single app are not databases.
    + Name the data elements as data, not the usecase.
- Use schemas wisely, since most modern backend frameworks do not offer native support for database schemas, especially on the huge variety of database systems (e.g. Django 1.8.1, 12/2015).

## Suffixes

- Never use suffixes on tables, but on other database objects like..
    + `_v` View (with the main TableName in front)
    + `_fk` Foreign Key (the constraint name, not the column)
    + `_cac` Cache
    + `_seg` Segment
    + `_tr` Transaction (stored proc or function)
    + `_fn` Function (non-transactional)
- This is really important for debugging error messages, which return the object name of the error source.
