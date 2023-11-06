1. Create a database and a Movies table

+----+-------------------+---------+-------------+------------+--------+
| ID | Title             | Runtime | Genre       | IMDB_Score | Rating |
+----+-------------------+---------+-------------+------------+--------+
|  1 | Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
|  2 | Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
|  3 | Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
|  4 | Waltz With Bashir |      90 | Documentary |        8.0 | R      |
|  5 | Spaceballs        |      96 | Comedy      |        7.1 | PG     |
|  6 | Monsters Inc.     |      92 | Animation   |        8.1 | G      |
+----+-------------------+---------+-------------+------------+--------+

2. Add two more movies of your choosing to the table.
   
INSERT INTO Movies (Title, Runtime, Genre, IMDB_Score, Rating)
VALUES
    ('Drumline', 120, 'Drama', 6.8, 'PG-13'),
    ('Love Don''t Cost A Thing', 96, 'Romance', 5.2, 'PG-13');

   +----+-------------------------+---------+-------------+------------+--------+
| ID | Title                   | Runtime | Genre       | IMDB_Score | Rating |
+----+-------------------------+---------+-------------+------------+--------+
|  1 | Howard the Duck         |     110 | Sci-Fi      |        4.6 | PG     |
|  2 | Lavalantula             |      83 | Horror      |        4.7 | TV-14  |
|  3 | Starship Troopers       |     129 | Sci-Fi      |        7.2 | PG-13  |
|  4 | Waltz With Bashir       |      90 | Documentary |        8.0 | R      |
|  5 | Spaceballs              |      96 | Comedy      |        7.1 | PG     |
|  6 | Monsters Inc.           |      92 | Animation   |        8.1 | G      |
|  7 | Drumline                |     120 | Drama       |        6.8 | PG-13  |
|  8 | Love Don't Cost A Thing |      96 | Romance     |        5.2 | PG-13  |
+----+-------------------------+---------+-------------+------------+--------+

3. Create a query to find all movies in the Sci-Fi genre.

SELECT * FROM Movies WHERE Genre = 'Sci-Fi';
+----+-------------------+---------+--------+------------+--------+
| ID | Title             | Runtime | Genre  | IMDB_Score | Rating |
+----+-------------------+---------+--------+------------+--------+
|  1 | Howard the Duck   |     110 | Sci-Fi |        4.6 | PG     |
|  3 | Starship Troopers |     129 | Sci-Fi |        7.2 | PG-13  |
+----+-------------------+---------+--------+------------+--------+

4. Create a query to find all films that scored at least a 6.5 on IMDB

SELECT * FROM Movies WHERE IMDB_Score >= 6.5;
+----+-------------------+---------+-------------+------------+--------+
| ID | Title             | Runtime | Genre       | IMDB_Score | Rating |
+----+-------------------+---------+-------------+------------+--------+
|  3 | Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
|  4 | Waltz With Bashir |      90 | Documentary |        8.0 | R      |
|  5 | Spaceballs        |      96 | Comedy      |        7.1 | PG     |
|  6 | Monsters Inc.     |      92 | Animation   |        8.1 | G      |
|  7 | Drumline          |     120 | Drama       |        6.8 | PG-13  |
+----+-------------------+---------+-------------+------------+--------+

5. For parents who have young kids, but who don't want to sit through long children's movies, create a query to find all of the movies rated G or PG that are less than 100 minutes long.

SELECT * FROM Movies WHERE Rating IN ('G', 'PG') AND Runtime < 100;
+----+---------------+---------+-----------+------------+--------+
| ID | Title         | Runtime | Genre     | IMDB_Score | Rating |
+----+---------------+---------+-----------+------------+--------+
|  5 | Spaceballs    |      96 | Comedy    |        7.1 | PG     |
|  6 | Monsters Inc. |      92 | Animation |        8.1 | G      |
+----+---------------+---------+-----------+------------+--------+

6. Create a query to show the average runtimes of movies scoring below a 7.5 on imdb, grouped by their respective genres.

SELECT Genre, AVG(Runtime) AS AvgRuntime FROM Movies WHERE IMDB_Score < 7.5 GROUP BY Genre;
+---------+------------+
| Genre   | AvgRuntime |
+---------+------------+
| Sci-Fi  |   119.5000 |
| Horror  |    83.0000 |
| Comedy  |    96.0000 |
| Drama   |   120.0000 |
| Romance |    96.0000 |
+---------+------------+

7. There's been a data entry mistake; Starship Troopers is actually rated R, not PG-13. Create a query that finds the movie by its title and changes its rating to R.

UPDATE Movies SET Rating = 'R' WHERE Title = 'Starship Troopers';
+----+-------------------------+---------+-------------+------------+--------+
| ID | Title                   | Runtime | Genre       | IMDB_Score | Rating |
+----+-------------------------+---------+-------------+------------+--------+
|  1 | Howard the Duck         |     110 | Sci-Fi      |        4.6 | PG     |
|  2 | Lavalantula             |      83 | Horror      |        4.7 | TV-14  |
|  3 | Starship Troopers       |     129 | Sci-Fi      |        7.2 | R      |
|  4 | Waltz With Bashir       |      90 | Documentary |        8.0 | R      |
|  5 | Spaceballs              |      96 | Comedy      |        7.1 | PG     |
|  6 | Monsters Inc.           |      92 | Animation   |        8.1 | G      |
|  7 | Drumline                |     120 | Drama       |        6.8 | PG-13  |
|  8 | Love Don't Cost A Thing |      96 | Romance     |        5.2 | PG-13  |
+----+-------------------------+---------+-------------+------------+--------+

8. Show the ID number and rating of all of the Horror and Documentary movies in the database. Do this in only one query.

SELECT ID, Rating FROM Movies WHERE Genre IN ('Horror', 'Documentary');
+----+--------+
| ID | Rating |
+----+--------+
|  2 | TV-14  |
|  4 | R      |
+----+--------+

9. This time let's find the average, maximum, and minimum IMDB score for movies of each rating.

SELECT Rating, AVG(IMDB_Score) AS AvgScore, MAX(IMDB_Score) AS MaxScore, MIN(IMDB_Score) AS MinScore
FROM Movies GROUP BY Rating;
+--------+----------+----------+----------+
| Rating | AvgScore | MaxScore | MinScore |
+--------+----------+----------+----------+
| PG     |  5.85000 |      7.1 |      4.6 |
| TV-14  |  4.70000 |      4.7 |      4.7 |
| R      |  7.60000 |      8.0 |      7.2 |
| G      |  8.10000 |      8.1 |      8.1 |
| PG-13  |  6.00000 |      6.8 |      5.2 |
+--------+----------+----------+----------+

10. That last query isn't very informative for ratings that only have 1 entry. Use a HAVING COUNT(*) > 1 clause to only show ratings with multiple movies showing.

SELECT Rating, COUNT(*) AS MovieCount FROM Movies GROUP BY Rating HAVING MovieCount > 1;
+--------+------------+
| Rating | MovieCount |
+--------+------------+
| PG     |          2 |
| R      |          2 |
| PG-13  |          2 |
+--------+------------+

11. Make the movie list more child-friendly. Delete all entries that have a rating of R. Remember to record your queries in a README.md file

DELETE FROM Movies WHERE Rating = 'R';
+----+-------------------------+---------+-----------+------------+--------+
| ID | Title                   | Runtime | Genre     | IMDB_Score | Rating |
+----+-------------------------+---------+-----------+------------+--------+
|  1 | Howard the Duck         |     110 | Sci-Fi    |        4.6 | PG     |
|  2 | Lavalantula             |      83 | Horror    |        4.7 | TV-14  |
|  5 | Spaceballs              |      96 | Comedy    |        7.1 | PG     |
|  6 | Monsters Inc.           |      92 | Animation |        8.1 | G      |
|  7 | Drumline                |     120 | Drama     |        6.8 | PG-13  |
|  8 | Love Don't Cost A Thing |      96 | Romance   |        5.2 | PG-13  |
+----+-------------------------+---------+-----------+------------+--------+

Remember to record your queries in a README.md file before the last two commands below

12. Delete the Movies Table

DROP TABLE IF EXISTS Movies;

13. Delete the Database

DROP DATABASE IF EXISTS MovieDatabase;


GROUP A WORK
Three new Queries

1. Longest Movie by Genre
SELECT Genre, Title, Runtime
FROM Movies
WHERE (Genre, Runtime) IN (SELECT Genre, MAX(Runtime) FROM Movies GROUP BY Genre);
+-----------+-------------------------+---------+
| Genre     | Title                   | Runtime |
+-----------+-------------------------+---------+
| Sci-Fi    | Howard the Duck         |     110 |
| Horror    | Lavalantula             |      83 |
| Comedy    | Spaceballs              |      96 |
| Animation | Monsters Inc.           |      92 |
| Drama     | Drumline                |     120 |
| Romance   | Love Don't Cost A Thing |      96 |
+-----------+-------------------------+---------+

2. Highest IMDB by Genre
SELECT Genre, Title, IMDB_Score
FROM Movies
WHERE (Genre, IMDB_Score) IN (SELECT Genre, MAX(IMDB_Score) FROM Movies GROUP BY Genre);
+-----------+-------------------------+------------+
| Genre     | Title                   | IMDB_Score |
+-----------+-------------------------+------------+
| Sci-Fi    | Howard the Duck         |        4.6 |
| Horror    | Lavalantula             |        4.7 |
| Comedy    | Spaceballs              |        7.1 |
| Animation | Monsters Inc.           |        8.1 |
| Drama     | Drumline                |        6.8 |
| Romance   | Love Don't Cost A Thing |        5.2 |
+-----------+-------------------------+------------+

3. Amount of Movies in Each Genre
SELECT Genre, COUNT(*) AS MovieCount FROM Movies GROUP BY Genre;
+-----------+------------+
| Genre     | MovieCount |
+-----------+------------+
| Sci-Fi    |          1 |
| Horror    |          1 |
| Comedy    |          1 |
| Animation |          1 |
| Drama     |          1 |
| Romance   |          1 |
+-----------+------------+

4. Create table
CREATE TABLE IF NOT EXISTS Actors (
    ActorID INT AUTO_INCREMENT PRIMARY KEY,
    ActorName VARCHAR(100) UNIQUE
);

INSERT INTO Actors (ActorName) VALUES
    ('Nick Cannon'),
    ('Denzel Washington'),
    ('Michael B. Jordan'),
    ('Will Smith'),
    ('Jamie Foxx');
---------+-------------------+
| ActorID | ActorName         |
+---------+-------------------+
|       2 | Denzel Washington |
|       5 | Jamie Foxx        |
|       3 | Michael B. Jordan |
|       1 | Nick Cannon       |
|       4 | Will Smith        |
+---------+-------------------+









Chapter 1 Notes:

Structured Query Language (SQL): A specialized language for managing and querying relational databases.

Declarative Language: Focuses on what data to retrieve rather than how to retrieve it.

Relational Database Management System (RDBMS): Software to manage relational databases.

Tables: Data is organized into tables with rows and columns.

Relationships: Connections between tables define relationships.

CRUD Operations:
Create (C): Create databases, tables, and records.
Read (R): Retrieve data using the SELECT statement.
Update (U): Modify existing data with the UPDATE statement.
Delete (D): Remove records using the DELETE statement.

CREATE DATABASE: Statement to create a new database.

CREATE TABLE: Define the structure of a table, including column names and data types.

INSERT INTO: Add new records (rows) into a table.

SELECT: Retrieve data using the SELECT statement.

Primary Key: A unique identifier for each record in a table.

Foreign Key: A reference to a primary key in another table.



Database relationships define how data in one table is related to data in another table within a Relational Database Management System (RDBMS).

The term "Relational" in RDBMS refers to the use of tables with relations, and relationships are established using keys.

Types of Database Relationships:
One-to-One (1:1): Each data in one table relates to only one data in another table.
One-to-Many (1:M): One data in one table relates to multiple data in another table.
Many-to-Many (M:M): Multiple data in one table relate to multiple data in another table.



