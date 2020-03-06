# Transact SQL


```sql
-- Changing the db context
USE master
GO

-- CRUD operations
CREATE DATABASE Demo
GO

USE Demo
GO

-- dbo reffers to database owner
CREATE TABLE dbo.Person (
  PersonId     UNIQUEIDENTIFIER             NOT NULL       PRIMARY KEY default NEWID(),
  FirstName    VARCHAR(128)    NOT NULL,
  LastName    VARCHAR(128)    NOT NULL,
  IdCode VARCHAR(25)
)
GO

DROP TABLE dbo.Person
GO

INSERT INTO dbo.Person(FirstName, LastName) VALUES ('Foo', 'Bar')
GO

DELETE FROM dbo.Person WHERE FirstName = 'Foo';
GO

UPDATE Person SET Name='Fido' where Name like 'Foo'
GO

SELECT Person where LastName = 'Bar'
GO

```
`More complext featues in MSSQL (Views & Procedures)`
```sql
-- Creating VIEWS

CREATE VIEW vw_Persons  
   AS  
   SELECT FirstName, LastName, Age FROM Person;  
GO

SELECT * FROM vw_Persons;  
GO   

-- Creating a procedure
CREATE PROCEDURE pr_Names @PAge money  
   AS  
   BEGIN  
      -- The print statement returns text to the user  
      PRINT 'People older than ' + CAST(@PAge AS varchar(10));  
      -- A second statement starts here  
      SELECT FirstName, LastName, Age FROM vw_Persons  
            WHERE Age > @PAge;  
   END  
GO

EXECUTE pr_Names 17;  
GO
```



### Useful links
- [Temporal keys](https://docs.microsoft.com/en-us/sql/relational-databases/tables/temporal-tables?view=sql-server-ver15)
- [Tutorial on TSQL](https://docs.microsoft.com/en-us/sql/t-sql/lesson-1-creating-database-objects?view=sql-server-ver15)

- [About "GO" command](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/sql-server-utilities-statements-go?view=sql-server-ver15)
- [Transact-SQL Syntax Conventions](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql?view=sql-server-ver15)