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

## Code SQL Beta
The code establishes a MySQL database connection, creates tables for user information, car mileage, and rental duration. It inserts sample data, retrieves and prints information from the tables, and then commits the changes to the database. The program ensures proper newline formatting for clearer output in the terminal.

```
# -*- coding: utf-8 -*-
"""
Created on Tue Jan 23 23:36:10 2024
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

users = [("Ali", "M"),
         ("Kamal", "M"),
         ("Siti", "F")]

CarStatus = [("Corola", "50KM"),
             ("Axia", "7KM"),
             ("Kancil", "80KM")]

Time_Rent = [("6:00 AM", "1:00 PM"),
             ("10:00 AM", "3:00 PM"),
             ("11:00 AM", "7:00 PM")]

# Creating a cursor
mycursor = db.cursor()

# Creating the database if it does not exist
mycursor.execute("CREATE DATABASE IF NOT EXISTS Rental2_Car_UTM")

# Connecting to the specified database
db = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="",
    database="Rental2_Car_UTM"
)

# Creating the tables
mycursor = db.cursor()

Q1 = mycursor.execute("CREATE TABLE User_Information (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, user varchar(50) NOT NULL, created datetime NOT NULL, gender ENUM('M', 'F') NOT NULL)")
Q2 = mycursor.execute("CREATE TABLE Mileage (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, CarSelect ENUM('Corola', 'Kancil', 'Axia') NOT NULL ,Mileage varchar(50) NOT NULL)")
Q3 = mycursor.execute("CREATE TABLE Duration_Rent (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, `Time IN` varchar(50) NOT NULL, `Time OUT` varchar(50) NOT NULL)")

mycursor.execute(Q1)
mycursor.execute(Q2)
mycursor.execute(Q3)



print("Table Availble")
# Showing the tables
mycursor.execute("SHOW TABLES")
for x in mycursor:
    print(x)
    

##SEND TO SQL
# Inserting data into User_Information table
Q4 = "INSERT INTO User_Information (user, gender) VALUES (%s, %s)"
mycursor.executemany(Q4, users)

# Inserting data into Mileage table
Q5 = "INSERT INTO Mileage (CarSelect, Mileage) VALUES (%s, %s)"
mycursor.executemany(Q5, CarStatus)

# Inserting data into Duration_Rent table
Q6 = "INSERT INTO Duration_Rent (`Time IN`, `Time OUT`) VALUES (%s, %s)"
mycursor.executemany(Q6, Time_Rent)


# Fetch data from the "User_Information" table
mycursor.execute("SELECT * FROM User_Information")
USR_INFO = mycursor.fetchall() 

mycursor.execute("SELECT * FROM Duration_Rent")
DUR = mycursor.fetchall() 

mycursor.execute("SELECT * FROM Mileage")
Milage = mycursor.fetchall() 

print("\nUser Information")
for x in USR_INFO:
    print(x)
    
print("\nDuration_Rent") 
for x in DUR:
    print(x)  

print("\nCar Status") 
for x in Milage:
    print(x)


# Committing the changes
db.commit()

# Closing the database connection
db.close()
```
![Table](https://github.com/faisalhazry/Python_MySQL_RentalCarUTM/assets/121289405/a7160af0-c28a-4444-aed2-9d57feebeff2)

![image](https://github.com/faisalhazry/Python_MySQL_RentalCarUTM/assets/121289405/8cffb20d-1e2a-4c39-9eff-38097143c146)


# Server code 
```
# -*- coding: utf-8 -*-
"""
Created on Wed Jan 24 14:56:43 2024

@author: USER
"""

# -*- coding: utf-8 -*-
"""
Created on Tue Jan 23 23:36:10 2024
@author: USER
"""

import mysql.connector
import socket
from datetime import datetime
import pickle

# Function to handle client requests
def handle_client(client_socket):
    data = client_socket.recv(4096)
    # Assuming the data sent is a dictionary containing users, CarStatus, and Time_Rent
    received_data = pickle.loads(data)
    
    # Extracting data
    users = received_data.get('users', [])
    CarStatus = received_data.get('CarStatus', [])
    Time_Rent = received_data.get('Time_Rent', [])
    
    
    
    
    # Your SQL code to insert data into tables
    Q4 = "INSERT INTO User_Information (user, gender) VALUES (%s, %s)"
    mycursor.executemany(Q4, users)

    Q5 = "INSERT INTO Mileage (CarSelect, Mileage) VALUES (%s, %s)"
    mycursor.executemany(Q5, CarStatus)

    Q6 = "INSERT INTO Duration_Rent (`Time IN`, `Time OUT`) VALUES (%s, %s)"
    mycursor.executemany(Q6, Time_Rent)

    # Committing the changes
    db.commit()
    
    
    
    

    # Fetching data and displaying it
    mycursor.execute("SELECT * FROM User_Information")
    USR_INFO = mycursor.fetchall()

    mycursor.execute("SELECT * FROM Duration_Rent")
    DUR = mycursor.fetchall()

    mycursor.execute("SELECT * FROM Mileage")
    Milage = mycursor.fetchall()
    
    
    
    
    

    print("\nUser Information")
    for x in USR_INFO:
        print(x)

    print("\nDuration_Rent")
    for x in DUR:
        print(x)

    print("\nCar Status")
    for x in Milage:
        print(x)

    # Sending a response to the client
    client_socket.send("Data received and stored successfully".encode())
    client_socket.close()
    
    
    
    
    


# Establishing connection without specifying the database
db = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="",
)

# Creating a cursor
mycursor = db.cursor()

# Creating the database if it does not exist
mycursor.execute("CREATE DATABASE IF NOT EXISTS Rental2_Car_UTM")

# Connecting to the specified database
db = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="",
    database="Rental2_Car_UTM"
)

# Creating the tables
mycursor = db.cursor()



# Uncoment for first time creation datra base
'''
Q1 = mycursor.execute("CREATE TABLE User_Information (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, user varchar(50) NOT NULL, created datetime NOT NULL, gender ENUM('M', 'F') NOT NULL)")
Q2 = mycursor.execute("CREATE TABLE Mileage (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, CarSelect ENUM('Corola', 'Kancil', 'Axia') NOT NULL ,Mileage varchar(50) NOT NULL)")
Q3 = mycursor.execute("CREATE TABLE Duration_Rent (id int PRIMARY KEY NOT NULL AUTO_INCREMENT, `Time IN` varchar(50) NOT NULL, `Time OUT` varchar(50) NOT NULL)")

#mycursor.execute(Q1)
#mycursor.execute(Q2)
#mycursor.execute(Q3)
'''

# Creating the TCP server
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('localhost', 1234))
server.listen(5)

print("Server is listening for incoming connections...")

while True:
    client_socket, addr = server.accept()
    print(f"Accepted connection from {addr}")
    handle_client(client_socket)

```

# Client code
```
import socket
import pickle

# Input user data from the terminal
user_name = input("Enter user name: ")
user_gender = input("Enter user gender (M/F): ")

# Input car status data from the terminal
car_model = input("Enter car model (Corola/Kancil): ")
mileage = input("Enter mileage: ")

# Input time rent data from the terminal
time_in = input("Enter time in (YYYY-MM-DD HH:mm:ss): ")
time_out = input("Enter time out (YYYY-MM-DD HH:mm:ss): ")

# Create a dictionary with the input data
data_to_send = {
    'users': [(user_name, user_gender)],
    'CarStatus': [(car_model, mileage)],
    'Time_Rent': [(time_in, time_out)]
}

# Serializing the data using pickle
serialized_data = pickle.dumps(data_to_send)

# Creating a socket and connecting to the server
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(('localhost', 1234))

# Sending the serialized data to the server
client_socket.send(serialized_data)

# Receiving the response from the server
response = client_socket.recv(4096)
print(response.decode())

# Closing the socket
client_socket.close()
```





