---
title: "Querying relational databases in Python"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Relational database 101
* Import packages and functions   
* Create the database engine   
* Connect to the engine   
* Query the database   
* Save query results to a DataFrame   
* Close the connection

### Queries
* SELECT
* WHERE
* JOIN 
* ORDER BY


```python
# Import packages
from sqlalchemy import create_engine
import pandas as pd

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Execute query and store records in DataFrame: df
df = pd.read_sql_query('SELECT * FROM PlaylistTrack INNER JOIN Track on PlaylistTrack.TrackId = Track.TrackId WHERE Milliseconds < 250000', engine)

# Print head of DataFrame
print(df.head())
```

       PlaylistId  TrackId  TrackId              Name  AlbumId  MediaTypeId  \
    0           1     3390     3390  One and the Same      271            2   
    1           1     3392     3392     Until We Fall      271            2   
    2           1     3393     3393     Original Fire      271            2   
    3           1     3394     3394       Broken City      271            2   
    4           1     3395     3395          Somedays      271            2   
    
       GenreId Composer  Milliseconds    Bytes  UnitPrice  
    0       23     None        217732  3559040       0.99  
    1       23     None        230758  3766605       0.99  
    2       23     None        218916  3577821       0.99  
    3       23     None        228366  3728955       0.99  
    4       23     None        213831  3497176       0.99  



```python
# Open engine in context manager
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    rs = con.execute('SELECT Title, Name FROM Album INNER JOIN Artist ON Album.ArtistID = Artist.ArtistID')
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()

# Print head of DataFrame df
print(df.head())

```

                                       Title       Name
    0  For Those About To Rock We Salute You      AC/DC
    1                      Balls to the Wall     Accept
    2                      Restless and Wild     Accept
    3                      Let There Be Rock      AC/DC
    4                               Big Ones  Aerosmith


Note 4 lines of code from context manager can be condensed to one line of code from `Pandas`

# Educational intro below

### Import packages


```python
# import necessary module
from sqlalchemy import create_engine
import pandas as pd
```

### Create a database engine

Creating the first SQL engine. You'll create an engine to connect to the SQLite database `Chinook.sqlite`

`'sqlite:///Northwind.sqlite'` is called the connection string to the SQLite database `Chinook.sqlite`


```python
# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')
```

### What are the tables in the database?


```python
# Save the table names to a list: table_names
table_names = engine.table_names()

# Print the table names to the shell
print(table_names)

```

    ['Album', 'Artist', 'Customer', 'Employee', 'Genre', 'Invoice', 'InvoiceLine', 'MediaType', 'Playlist', 'PlaylistTrack', 'Track']


### Query database and close engine connection 
The Hello World of SQL queries, `SELECT`, in order to retrieve all columns of the table `Album` in the Chinook database. The query `SELECT *` selects all columns.


```python
# Open engine connection: con
con = engine.connect()

# Perform query: rs
rs = con.execute('SELECT * FROM Album')

# Save results of the query to DataFrame: df
df = pd.DataFrame(rs.fetchall())

# Set the proper names of the columns
df.columns = rs.keys()

# Close connection
con.close()

# Print head of DataFrame df
print(df.head())
```

       AlbumId                                  Title  ArtistId
    0        1  For Those About To Rock We Salute You         1
    1        2                      Balls to the Wall         2
    2        3                      Restless and Wild         2
    3        4                      Let There Be Rock         1
    4        5                               Big Ones         3


### Customize the query and use context manager

Customize your query in order to:

* Select specified columns from a table  
* Select a specified number of rows  
* Import column names from the database table 


```python
# Open engine in context manager
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    rs = con.execute('SELECT LastName, Title FROM Employee')
    df = pd.DataFrame(rs.fetchmany(3))
    df.columns = rs.keys()

# Print the length of the DataFrame df
print(len(df))

# Print the head of the DataFrame df
print(df.head())
```

    3
      LastName                Title
    0    Adams      General Manager
    1  Edwards        Sales Manager
    2  Peacock  Sales Support Agent


### Filtering your database records using SQL's WHERE


```python
# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Open engine in context manager
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    rs = con.execute('SELECT * FROM Employee WHERE EmployeeId >= 6')
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()

# Print the head of the DataFrame df
print(df.head())
```

       EmployeeId  LastName FirstName       Title  ReportsTo            BirthDate  \
    0           6  Mitchell   Michael  IT Manager          1  1973-07-01 00:00:00   
    1           7      King    Robert    IT Staff          6  1970-05-29 00:00:00   
    2           8  Callahan     Laura    IT Staff          6  1968-01-09 00:00:00   
    
                  HireDate                      Address        City State Country  \
    0  2003-10-17 00:00:00         5827 Bowness Road NW     Calgary    AB  Canada   
    1  2004-01-02 00:00:00  590 Columbia Boulevard West  Lethbridge    AB  Canada   
    2  2004-03-04 00:00:00                  923 7 ST NW  Lethbridge    AB  Canada   
    
      PostalCode              Phone                Fax                    Email  
    0    T3B 0C5  +1 (403) 246-9887  +1 (403) 246-9899  michael@chinookcorp.com  
    1    T1K 5N8  +1 (403) 456-9986  +1 (403) 456-8485   robert@chinookcorp.com  
    2    T1H 1Y8  +1 (403) 467-3351  +1 (403) 467-8772    laura@chinookcorp.com  


### Ordering your SQL records with ORDER BY


```python
# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Open engine in context manager
with engine.connect() as con:
    rs = con.execute('SELECT * FROM Employee ORDER BY BirthDate')
    df = pd.DataFrame(rs.fetchall())

    # Set the DataFrame's column names
    df.columns = rs.keys()

# Print head of DataFrame
print(df.head())

```

       EmployeeId  LastName FirstName                Title  ReportsTo  \
    0           4      Park  Margaret  Sales Support Agent        2.0   
    1           2   Edwards     Nancy        Sales Manager        1.0   
    2           1     Adams    Andrew      General Manager        NaN   
    3           5   Johnson     Steve  Sales Support Agent        2.0   
    4           8  Callahan     Laura             IT Staff        6.0   
    
                 BirthDate             HireDate              Address        City  \
    0  1947-09-19 00:00:00  2003-05-03 00:00:00     683 10 Street SW     Calgary   
    1  1958-12-08 00:00:00  2002-05-01 00:00:00         825 8 Ave SW     Calgary   
    2  1962-02-18 00:00:00  2002-08-14 00:00:00  11120 Jasper Ave NW    Edmonton   
    3  1965-03-03 00:00:00  2003-10-17 00:00:00         7727B 41 Ave     Calgary   
    4  1968-01-09 00:00:00  2004-03-04 00:00:00          923 7 ST NW  Lethbridge   
    
      State Country PostalCode              Phone                Fax  \
    0    AB  Canada    T2P 5G3  +1 (403) 263-4423  +1 (403) 263-4289   
    1    AB  Canada    T2P 2T3  +1 (403) 262-3443  +1 (403) 262-3322   
    2    AB  Canada    T5K 2N1  +1 (780) 428-9482  +1 (780) 428-3457   
    3    AB  Canada    T3B 1Y7   1 (780) 836-9987   1 (780) 836-9543   
    4    AB  Canada    T1H 1Y8  +1 (403) 467-3351  +1 (403) 467-8772   
    
                          Email  
    0  margaret@chinookcorp.com  
    1     nancy@chinookcorp.com  
    2    andrew@chinookcorp.com  
    3     steve@chinookcorp.com  
    4     laura@chinookcorp.com  


### Pandas for SQL Queries


```python

```
