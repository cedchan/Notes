## Terminology

>[!definition]
>
>|Term|Definition|
>|-|-|
>|Name|Main label of a table|
>|Column/attribute|Headers in the table|
>|Row/tuple|Values for each attribute|
>|Schema| the name and columns|
>|Degree/arity|Number of attributes|
>|Cardinality| Number of rows|
>|Key|Minimal subset of attributes that uniquely identify each tuple|
>|Foreign key|An attribute that references another table|
>|Constraints|Semantic assertions about valid database instances|

Each table has a **name** and **columns** (**attributes**). Together, these form the **schema**, which changes slowly. The number of attributes is the **degree** or **arity** of the table.

Entries in the table are called **rows** or **tuples**. They're also **instances** of the table, and tend to change quickly. **Cardinality** is the number of rows in the current instance.

The schema may also be known as the **intension** of the table while the instances are the **extension.**

Each table must have a **key**, which consists of one or more columns that have unique values. These keys must be minimal. That is, they are a set of attributes that can uniquely identify a tuple (minimally).

Multiple tables may have attributes that link to one another (e.g., account number in an "accounts" table and a "deposit" table). **Foreign keys** reference an attribute in another table. If all foreign keys can be found in the referenced table, we have **referential integrity**.

## Structured Query Language (SQL)

SQL is separated into the **DML** (data manipulation language) and **DDL** (data definition language)

```
```