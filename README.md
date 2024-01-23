# Python_MySQL_RentalCarUTM
An Assigment Netwrok Programing using Python MySQL  - Foreign Keys &amp; Relating Tables

## Creating table 
There will be 3 table using a foreign key relationship involves a parent table that holds the initial column values, and a child table with column values that reference the parent column values. A foreign key constraint is defined on the child table. 

table that propose create is User_Information, Milage_Car, User_TimeRent_IN/OUT

```
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
mycursor.execute("CREATE TABLE User_Information (namae varchar(50) NOT NULL, created datetime NOT NULL, gender ENUM('M', 'F') NOT NULL, id int PRIMARY KEY NOT NULL AUTO_INCREMENT)")

# Committing the changes
db.commit()

# Closing the database connection
db.close()
```

