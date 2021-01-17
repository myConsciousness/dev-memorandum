# Introduction to SQL

## Summary

SQL, Structured Query Language, is a programming language designed to manage data stored in relational databases. SQL operates through simple, declarative statements. This keeps data accurate and secure, and helps maintain the integrity of databases, regardless of size.

The SQL language is widely used today across web frameworks and database applications. Knowing SQL gives you the freedom to explore your data, and the power to make better decisions. By learning SQL, you will also learn concepts that apply to nearly every data storage system.

The statements covered in this course use SQLite Relational Database Management System (RDBMS). You can also access a glossary of all the SQL commands taught in this course.

## Instructions

Let’s begin by entering a SQL command.

In the code editor, type:

```sql
SELECT * FROM celebs;
```

You will run all of your SQL commands in this course by pressing the Run button at the bottom of the code editor.

Press Run.

**_Result:_**

| id  | name            | age |
| --- | --------------- | --- |
| 1   | Justin Bieber   | 22  |
| 2   | Beyonce Knowles | 33  |
| 3   | Jeremy Lin      | 26  |
| 4   | Taylor Swift    | 26  |

**_Database Schema:_**

| name | type    |
| ---- | ------- |
| id   | INTEGER |
| name | TEXT    |
| age  | INTEGER |
