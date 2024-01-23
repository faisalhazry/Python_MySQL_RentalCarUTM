# Python_MySQL_RentalCarUTM
An Assigment Netwrok Programing using Python MySQL  - Foreign Keys &amp; Relating Tables

## Creating table 
There will be 3 table using a foreign key relationship involves a parent table that holds the initial column values, and a child table with column values that reference the parent column values. A foreign key constraint is defined on the child table. 

table that propose create is User_Information, Milage_Car, User_TimeRent_IN/OUT

```
# -*- coding: utf-8 -*-
"""
Created on Tue Jan 23 20:00:25 2024

@author: USER
"""

import mysql.connector 
from datetime import datetime

# Establishing connection without specifying the database
db = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="",
)

# Creating a cursor
mycursor = db.cursor()

# Creating the database if it does not exist
mycursor.execute("CREATE DATABASE IF NOT EXISTS Rental_Car_UTM")

# Connecting to the specified database
db = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="",
    database="Rental_Car_UTM"
)

# Creating the table
mycursor = db.cursor()
mycursor.execute("CREATE TABLE User_Information (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, user varchar(50) NOT NULL, created datetime NOT NULL, gender ENUM('M', 'F') NOT NULL)")
mycursor.execute("CREATE TABLE Milage (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, CarSelect ENUM('Corolo', 'Kancil', 'Axia') NOT NULL ,Milage varchar(50) NOT NULL)")
mycursor.execute("CREATE TABLE Duration_Rent (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, `Time IN` varchar(50) NOT NULL, `Time OUT` varchar(50) NOT NULL)")

# Committing the changes
db.commit()

# Closing the database connection
db.close()

```
![image](https://github.com/faisalhazry/Python_MySQL_RentalCarUTM/assets/121289405/fe9e51be-b0fa-4507-95f4-90938b42a510)


## Python Insert SQL
This code connects to a MySQL database and inserts a record into the "User_Information" table.
```
# -*- coding: utf-8 -*-
"""
Created on Tue Jan 23 22:25:28 2024

@author: USER
"""

import mysql.connector 
from datetime import datetime

# Connecting to the specified database
db = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="",
    database="Rental_Car_UTM"
)

mycursor= db.cursor()

mycursor.execute("INSERT INTO User_Information (user, created, gender) VALUES(%s, %s, %s)", ("Kamal", datetime.now(), "M"))

db.commit()
```
![image](https://github.com/faisalhazry/Python_MySQL_RentalCarUTM/assets/121289405/d69051df-df6e-408d-b714-f7dfd5a2b14e)

## Excute list table in python 
This code connects to a MySQL database and retrieves user information for genders 'F' and 'M'.
```
import mysql.connector 
from datetime import datetime

# Connecting to the specified database
db = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="",
    database="Rental_Car_UTM"
)

mycursor = db.cursor()

# Execute the first query for 'F'
mycursor.execute("SELECT id, user FROM User_Information WHERE gender = 'F'")
result_f = mycursor.fetchall()

# Execute the second query for 'M'
mycursor.execute("SELECT id, user FROM User_Information WHERE gender = 'M'")
result_m = mycursor.fetchall()


# Show tables in the database
mycursor.execute("SHOW TABLES")
tables = mycursor.fetchall()



# Fetch data from the "User_Information" table
mycursor.execute("SELECT * FROM User_Information")
Q1 = mycursor.fetchall()



# Print the list of tables
print("Tables in the database:")
for table in tables:
    print(table)

# Print the list of tables
print("Tables in user_information:")
for table in Q1:
    print(Q1)


# Print the results
print("Gender 'F':", result_f)
print("Gender 'M':", result_m)
```
![image](https://github.com/faisalhazry/Python_MySQL_RentalCarUTM/assets/121289405/8416d8f9-bc7f-47dd-abf4-e176a2500ad1)

## Creating linked table
In the provided code, three SQL queries use the execute method to create tables in a MySQL database. The FOREIGN KEY constraint establishes a link between tables, ensuring referential integrity by referencing a primary key in another table. This maintains consistency and relationships between tables in a relational database.
```
Q1 = mycursor.execute("CREATE TABLE User_Information (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, user varchar(50) NOT NULL, created datetime NOT NULL, gender ENUM('M', 'F') NOT NULL)")
Q2 = mycursor.execute("CREATE TABLE Milage (userId int PRIMARY KEY, FOREIGN KEY(userId) REFERENCES User_Information(id), CarSelect ENUM('Corola', 'Kancil', 'Axia') NOT NULL ,Milage varchar(50) NOT NULL)")
Q3 = mycursor.execute("CREATE TABLE Duration_Rent (userId int PRIMARY KEY,FOREIGN KEY(userId) REFERENCES User_Information(id), `Time IN` varchar(50) NOT NULL, `Time OUT` varchar(50) NOT NULL)")
```


