# Additional questions - SQL

### SQL

#### What does UNION do? What is the difference between UNION and UNION ALL?

UNION merges the contents of two structurally-compatible tables into a single combined table. The difference between UNION and UNION ALL is that UNION will omit duplicate records whereas UNION ALL will include duplicate records.

It is important to note that the performance of UNION ALL will typically be better than UNION, since UNION requires the server to do the additional work of removing any duplicates. So, in cases where is is certain that there will not be any duplicates, or where having duplicates is not a problem, use of UNION ALL would be recommended for performance reasons.

#### List and explain the different types of JOIN clauses supported in ANSI-standard SQL.

ANSI-standard SQL specifies five types of JOIN clauses as follows:

* INNER JOIN (a.k.a. “simple join”): Returns all rows for which there is at least one match in BOTH tables. This is the default type of join if no specific JOIN type is specified.
* LEFT JOIN (or LEFT OUTER JOIN): Returns all rows from the left table, and the matched rows from the right table; i.e., the results will contain all records from the left table, even if the JOIN condition doesn’t find any matching records in the right table. This means that if the ON clause doesn’t match any records in the right table, the JOIN will still return a row in the result for that record in the left table, but with NULL in each column from the right table.
* RIGHT JOIN (or RIGHT OUTER JOIN): Returns all rows from the right table, and the matched rows from the left table. This is the exact opposite of a LEFT JOIN; i.e., the results will contain all records from the right table, even if the JOIN condition doesn’t find any matching records in the left table. This means that if the ON clause doesn’t match any records in the left table, the JOIN will still return a row in the result for that record in the right table, but with NULL in each column from the left table.
* FULL JOIN (or FULL OUTER JOIN): Returns all rows for which there is a match in EITHER of the tables. Conceptually, a FULL JOIN combines the effect of applying both a LEFT JOIN and a RIGHT JOIN; i.e., its result set is equivalent to performing aUNION of the results of left and right outer queries.
* CROSS JOIN: Returns all records where each row from the first table is combined with each row from the second table (i.e., returns the Cartesian product of the sets of rows from the joined tables). Note that a CROSS JOIN can either be specified using the CROSS JOIN syntax (“explicit join notation”) or (b) listing the tables in the FROM clause separated by commas without using a WHERE clause to supply join criteria (“implicit join notation”).

#### Given the following tables, What will be the result of the query below?

        sql> SELECT * FROM runners;

| id | name         | 
|---|---| 
|  1 | John Doe     |  
|  2 | Jane Doe     |  
|  3 | Alice Jones  |  
|  4 | Bobby Louis  |  
|  5 | Lisa Romero  |  

        sql> SELECT * FROM races;

| id | event          | winner_id |  
|---|---|---|
|  1 | 100 meter dash |  2        |  
|  2 | 500 meter dash |  3        |  
|  3 | cross-country  |  2        |  
|  4 | triathalon     |  NULL     |  

        SELECT * FROM runners WHERE id NOT IN (SELECT winner_id FROM races)

Surprisingly, given the sample data provided, the result of this query will be an empty set. The reason for this is as follows: If the set being evaluated by the SQL NOT IN condition contains any values that are null, then the outer query here will return an empty set, even if there are many runner ids that match winner_ids in the races table.

Knowing this, a query that avoids this issue would be as follows:

        SELECT * FROM runners WHERE id NOT IN (SELECT winner_id FROM races WHERE winner_id IS NOT null)
Note, this is assuming the standard SQL behavior that you get without modifying the default ANSI_NULLS setting.

#### Given two tables created and populated as follows, what will the result be from the following query:

        CREATE TABLE dbo.envelope(id int, user_id int);
        CREATE TABLE dbo.docs(idnum int, pageseq int, doctext varchar(100));

        INSERT INTO dbo.envelope VALUES
        (1,1),
        (2,2),
        (3,3);

        INSERT INTO dbo.docs(idnum,pageseq) VALUES
        (1,5),
        (2,6),
        (null,0);


        UPDATE docs SET doctext=pageseq FROM docs INNER JOIN envelope ON envelope.id=docs.idnum
        WHERE EXISTS (
        SELECT 1 FROM dbo.docs
        WHERE id=envelope.id
        );

The result of the query will be as follows:

        idnum  pageseq  doctext  
        1      5        5  
        2      6        6  
        NULL   0        NULL  
The EXISTS clause in the above query is a red herring. It will always be true since ID is not a member of dbo.docs. As such, it will refer to the envelope table comparing itself to itself!

The idnum value of NULL will not be set since the join of NULL will not return a result when attempting a match with any value of envelope.

#### Given these contents of the Customers table; here is a query written to return the list of customers not referred by Jane Smith. What will be the result of the query? Why? What would be a better way to write it?

        Id	Name			ReferredBy
        1	John Doe		NULL
        2	Jane Smith		NULL
        3	Anne Jenkins	2
        4	Eric Branford	NULL
        5	Pat Richards	1
        6	Alice Barnes	2

        SELECT Name FROM Customers WHERE ReferredBy <> 2;

Although there are 4 customers not referred by Jane Smith (including Jane Smith herself), the query will only return one: Pat Richards. All the customers who were referred by nobody at all (and therefore have NULL in their ReferredBy column) don’t show up. But certainly those customers weren’t referred by Jane Smith, and certainly NULL is not equal to 2, so why didn’t they show up?

SQL Server uses three-valued logic, which can be troublesome for programmers accustomed to the more satisfying two-valued logic (TRUE or FALSE) most programming languages use. In most languages, if you were presented with two predicates: ReferredBy = 2 and ReferredBy <> 2, you would expect one of them to be true and one of them to be false, given the same value of ReferredBy. In SQL Server, however, if ReferredBy is NULL, neither of them are true and neither of them are false. Anything compared to NULL evaluates to the third value in three-valued logic: UNKNOWN.

The query should be written in one of two ways:

        SELECT Name FROM Customers WHERE ReferredBy IS NULL OR ReferredBy <> 2
…or:

        SELECT Name FROM Customers WHERE ISNULL(ReferredBy, 0) <> 2; -- (Or COALESCE() )
Watch out for the following, though!

        SELECT Name FROM Customers WHERE ReferredBy = NULL OR ReferredBy <> 2
This will return the same faulty set as the original. Why? We already covered that: Anything compared to NULL evaluates to the third value in the three-valued logic: UNKNOWN. That “anything” includes NULL itself! That’s why SQL Server provides the IS NULL and IS NOT NULL operators to specifically check for NULL. Those particular operators will always evaluate to true or false.

Even if a candidate doesn’t have a great amount of experience with SQL Server, diving into the intricacies of three-valued logic in general can give a good indication of whether they have the ability learn it quickly or whether they will struggle with it.

#### Considering the database schema displayed in the SQLServer-style diagram below, write a SQL query to return a list of all the invoices. For each invoice, show the Invoice ID, the billing date, the customer’s name, and the name of the customer who referred that customer (if any). The list should be ordered by billing date.

Invoices  
| Column Name | Data Type | Allow Nulls |  
|---|---|---|  
|Id|int|no|  
|BillingDate|date|no|  
|CustomerId|int|no|  

Customers  
| Column Name | Data Type | Allow Nulls |  
|---|---|---|  
|Id|int|no|
|Name|nvarchar(50)|no|
|RefferedBy|int|yes|  

        SELECT i.Id, i.BillingDate, c.Name, r.Name AS ReferredByName
        FROM Invoices i
        LEFT JOIN Customers c ON i.CustomerId = c.Id
        LEFT JOIN Customers r ON c.ReferredBy = r.Id
        ORDER BY i.BillingDate;

#### Assume a schema of Emp ( Id, Name, DeptId ) , Dept ( Id, Name). If there are 10 records in the Emp table and 5 records in the Dept table, how many rows will be displayed in the result of the following SQL query?

        Select * From Emp, Dept

The query will result in 50 rows as a “cartesian product” or “cross join”, which is the default whenever the ‘where’ clause is omitted.

#### Given two tables created as follows; Write a query to fetch values in table test_a that are and not in test_b without using the NOT keyword.

        create table test_a(id numeric);

        create table test_b(id numeric);

        insert into test_a(id) values
        (10),
        (20),
        (30),
        (40),
        (50);

        insert into test_b(id) values
        (10),
        (30),
        (50);

In SQL Server, PostgreSQL, and SQLite, this can be done using the except keyword as follows:

        select * from test_a
        except
        select * from test_b;

MySQL does not support the except function. However, there is a standard SQL solution that works in all of the above engines, including MySQL:

        select a.id
        from test_a a
        left join test_b b on a.id = b.id
        where b.id is null;

#### Given a table TBL with a field Nmbr that has rows with the following values:

1, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1

Write a query to add 2 where Nmbr is 0 and add 3 where Nmbr is 1.

This can be done as follows:

        update TBL set Nmbr = case when Nmbr = 0 then Nmbr+2 else Nmbr+3 end;

#### Write a SQL query to find the 10th highest employee salary from an Employee table. Explain your answer.

(Note: You may assume that there are at least 10 records in the Employee table.)

PostreSQL uses the LIMIT keyword, as follows:

        SELECT Salary FROM
        (
            SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 10
        ) AS Emp ORDER BY Salary LIMIT 1;

-- or --  

        SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET 9;

#### Write a SQL query using UNION ALL (not UNION) that uses the WHERE clause to eliminate duplicates. Why might you want to do this?

You can avoid duplicates using UNION ALL and still run much faster than UNION DISTINCT (which is actually same as UNION) by running a query like this:

SELECT * FROM mytable WHERE a=X UNION ALL SELECT * FROM mytable WHERE b=Y AND a!=X
The key is the AND a!=X part. This gives you the benefits of the UNION (a.k.a., UNION DISTINCT) command, while avoiding much of its performance hit.

#### Given the following tables:

        SELECT * FROM users;

        user_id  username
        1        John Doe                                                                                            
        2        Jane Don                                                                                            
        3        Alice Jones                                                                                         
        4        Lisa Romero

        SELECT * FROM training_details;

        user_training_id  user_id  training_id  training_date
        1                 1        1            "2015-08-02"
        2                 2        1            "2015-08-03"
        3                 3        2            "2015-08-02"
        4                 4        2            "2015-08-04"
        5                 2        2            "2015-08-03"
        6                 1        1            "2015-08-02"
        7                 3        2            "2015-08-04"
        8                 4        3            "2015-08-03"
        9                 1        4            "2015-08-03"
        10                3        1            "2015-08-02"
        11                4        2            "2015-08-04"
        12                3        2            "2015-08-02"
        13                1        1            "2015-08-02"
        14                4        3            "2015-08-03"
Write a query to to get the list of users who took the a training lesson more than once in the same day, grouped by user and training lesson, each ordered from the most recent lesson date to oldest date.

        SELECT
            u.user_id,
            username,
            training_id,
            training_date,
            count( user_training_id ) AS count
        FROM users u JOIN training_details t ON t.user_id = u.user_id
        GROUP BY u.user_id,
                username,
                training_id,
                training_date
        HAVING count( user_training_id ) > 1
        ORDER BY training_date DESC;


        user_id  username      training_id  training_date             count
        4        Lisa Romero   2            August, 04 2015 00:00:00  2
        4        Lisa Romero   3            August, 03 2015 00:00:00  2
        1        John Doe      1            August, 02 2015 00:00:00  3
        3        Alice Jones   2            August, 02 2015 00:00:00  2

#### What is an execution plan? When would you use it? How would you view the execution plan?

An execution plan is basically a road map that graphically or textually shows the data retrieval methods chosen by the SQL server’s query optimizer for a stored procedure or ad hoc query. Execution plans are very useful for helping a developer understand and analyze the performance characteristics of a query or stored procedure, since the plan is used to execute the query or stored procedure.

In many SQL systems, a textual execution plan can be obtained using a keyword such as EXPLAIN, and visual representations can often be obtained as well. In Microsoft SQL Server, the Query Analyzer has an option called “Show Execution Plan” (located on the Query drop down menu). If this option is turned on, it will display query execution plans in a separate window when a query is run.

#### List and explain each of the ACID properties that collectively guarantee that database transactions are processed reliably.

ACID (Atomicity, Consistency, Isolation, Durability) is a set of properties that guarantee that database transactions are processed reliably. They are defined as follows:

* Atomicity. Atomicity requires that each transaction be “all or nothing”: if one part of the transaction fails, the entire transaction fails, and the database state is left unchanged. An atomic system must guarantee atomicity in each and every situation, including power failures, errors, and crashes.
* Consistency. The consistency property ensures that any transaction will bring the database from one valid state to another. Any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof.
* Isolation. The isolation property ensures that the concurrent execution of transactions results in a system state that would be obtained if transactions were executed serially, i.e., one after the other. Providing isolation is the main goal of concurrency control. Depending on concurrency control method (i.e. if it uses strict - as opposed to relaxed - serializability), the effects of an incomplete transaction might not even be visible to another transaction.
* Durability. Durability means that once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors. In a relational database, for instance, once a group of SQL statements execute, the results need to be stored permanently (even if the database crashes immediately thereafter). To defend against power loss, transactions (or their effects) must be recorded in a non-volatile memory.

#### Given a table dbo.users where the column user_id is a unique numeric identifier, how can you efficiently select the first 100 odd user_id values from the table?

(Assume the table contains well over 100 records with odd user_id values.)

        SELECT user_id FROM dbo.users WHERE user_id % 2 = 1 ORDER BY user_id LIMIT 100

#### How can you select all the even number records from a table? All the odd number records?

To select all the even number records from a table:

        Select * from table where id % 2 = 0 
To select all the odd number records from a table:

        Select * from table where id % 2 != 0

### What are the NVL and the NVL2 functions in SQL? How do they differ?

Both the NVL(exp1, exp2) and NVL2(exp1, exp2, exp3) functions check the value exp1 to see if it is null.

With the NVL(exp1, exp2) function, if exp1 is not null, then the value of exp1 is returned; otherwise, the value of exp2 is returned, but case to the same data type as that of exp1.

With the NVL2(exp1, exp2, exp3) function, if exp1 is not null, then exp2 is returned; otherwise, the value of exp3 is returned.

#### What is the difference between the WHERE and HAVING clauses?

When GROUP BY is not used, the WHERE and HAVING clauses are essentially equivalent.

However, when GROUP BYis used:

The WHERE clause is used to filter records from a result. The filtering occurs before any groupings are made.
The HAVING clause is used to filter values from a group (i.e., to check conditions after aggregation into groups has been performed).

#### What will be the output of the below query, given an Employee table having 10 records?

        BEGIN TRAN
        TRUNCATE TABLE Employees
        ROLLBACK
        SELECT * FROM Employees

This query will return 10 records as TRUNCATE was executed in the transaction. TRUNCATE does not itself keep a log but BEGIN TRANSACTION keeps track of the TRUNCATE command.

#### Suppose we have a Customer table containing the following data; 

        CustomerID  CustomerName
        1           Prashant Kaurav
        2           Ashish Jha
        3           Ankit Varma
        4           Vineet Kumar
        5           Rahul Kumar

Write a single SQL statement to concatenate all the customer names into the following single semicolon-separated string: Prashant Kaurav; Ashish Jha; Ankit Varma; Vineet Kumar; Rahul Kumar

In PostgreSQL one can also use this syntax to achieve the fully correct result:

        SELECT array_to_string(array_agg(CustomerName), '; '::text) 
        FROM Customer