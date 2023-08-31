


```sql
SELECT Contact.name
FROM Contact, With, Event
WHERE Contact.cid = With.cid
AND With.eid = Event.eid AND Event.desc = 'biking'
```

## Quizzes

### Quiz 1.1.1: What is a database?
1. Which of the following statements concerning databases is false
	1. SQL ... 
	2. NoSQL ... 
	3. **A relational data model is dependent on data structure and implementation**

### Quiz 1.1.2:
1. The benefits of using a database management system (DBMS) include which of the following? Select all that apply.
	1. Users must understand how data is stored and indexed to query the data
	2. **Queries on the database can be scaled up efficiently with the use of a DBMS**
	3. **DBMSs maintain consistency while supporting concurrent operations**
