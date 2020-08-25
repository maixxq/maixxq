---
title: SQL Queries for analysing dataset
date: 2020-12-23 00:00:00
excerpt: This is the first homework assignment from CMU Database Systems. The motivation for this is to understand what is SQL and how it is being used. A bike sharing data from five cities in the Bay Area is used for this homework.
type: post
blog: true
---

Desire outcome of this homework is to 1) learn basic and some advanced SQL features, and 2) get familiar with using a full-featured DBMS engine, SQLite. All credits to CMU and many thanks to Prof Andy Pavlo for making this possible. 

## Database VS Database System
> A database is an organized collection of structured information, or data, typically stored electronically in a computer system. A database is usually controlled by a database management system (DBMS). Together, the data and the DBMS, along with the applications that are associated with them, are referred to as a database system, often shortened to just database. ————— Oracle

Basically, database is a home for data. It is a place where data is being stored which can be accessed by other people. Each data item is stored in a field and the combination of fields is called a table. For example, every field in an user table represents the data about each users. A database management system (DBMS) is a collection of programs that allows users to build and maintain databases. DBMS serves as an environment to retrieve and store data efficiently. Some of the popular database management system are MySQL, Oracle and MongoDB.

## Data Models
> High-level conceptual data models provide concepts for presenting data in ways that are close to the way people perceive data. ————— ADRIENNE WATT & NELSON ENG

Entity relationship model is a typical data model which draws key concepts such as entities, attributes and relationships. An entity is a noun while the attributes are the properties the entity entails. A relationship represents the interaction between entities. Other types of record-based logical data models are the network data models and hierarchical data models. 

## Homework 1 Attempt
Peeking into the database with `.tables` command, there are three tables in total, namely station, trip and weather.

### Schema in SQL
Running the `.schema $TABLE_NAME` command on sqlite3 terminal shows the structure of the tables such as the existing attributes and the primary and foreign keys.

#### Question 1 Sample: Count the number of cities. 
SQL query and expected output:
```
select count(distinct(city)) from station;
5
```
#### Question 2: Count the number of stations in each city.
My naive attempt is to first find what cities are in this table, then count the number of stations in each city.

```js
sqlite> select distinct(city) from station

San Jose
Redwood City
Mountain View
Palo Alto
San Francisco

sqlite> select count(city) from station where city = 'San Jose';
16
sqlite> select count(city) from station where city = 'Redwood City';
7
sqlite> select count(city) from station where city = 'San Francisco';
35
sqlite> select count(city) from station where city = 'Mountain View';
7
sqlite> select count(city) from station where city = 'Palo Alto';
5

```
But in order to print city name and number of stations. Sort by number of stations (increasing), and break ties by city name (increasing), the correct way to do it is as follow

```js
sqlite> select city, count(station_id) as num from station group by city order by num asc, city asc;
// and to break ties 
Palo Alto|5
Mountain View|7
Redwood City|7
San Jose|16
San Francisco|35
```

#### Question 3: Find the percentage of trips in each city.
