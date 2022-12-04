# How to connect  MySQL database in Python

A few weeks ago, I decided to build a phonebook application using Python, and with the help of the Tkinter module, I was able to make a GUI for my application. However, I had a bit of a challenge with storing and manipulating the contacts that I stored.

I used a JSON file to store the contacts, and that came with its own limitations with regard to performing the **CRUD** operations (**CREATE**, **READ**, **UPDATE**, **DELETE**). I knew that the best way around this was to use a database, and in this case, a relational database would be perfect for it. So, I had to learn how to use a database management system (DBMS).

I found out that most of the resources out there felt a bit too technical and difficult for beginners to understand. Hence, I have decided to write this to explain the various concepts and processes relating to how to use a MySQL database with your Python application.

This specific article will focus on how to connect to the MySQL database and query the database successfully through your Python application.

## Install a Python SQL connector module (database adapter)

This is basically the utility that will help you connect your Python application with the SQL database. There are a few options from which you can choose. The five common ones available are:

1.  MySQLdb
    
2.  PyMySQL
    
3.  SuperSQLite
    
4.  Psycopg2
    
5.  QTSQL
    

The good news is that all of these modules rely on the Python database API (DB-API). As such, once connected to them, the code required to communicate with your database is very similar. So, even though these various database adapters enable you to communicate with databases from different vendors (MySQL, SQLite, PostgreSQL, etc).

Let's choose one of these adapters and focus on how to connect to your SQL database through it. Since I used `MySQLdb` for my most recent project, I will go ahead and use that in this tutorial.

### How to install MySQLdb

To install `MySQLdb` and make use of it, you need to have `MySQL` already installed. I am using a virtual machine using `Ubuntu` hence let me work you through how you are going to do that on `Ubuntu` . I believe it will be similar for other Linux distros.

To install `MySQL`, you can run the commands below:

```bash
sudo apt update
sudo apt install mysql-server
```

To install the `MySQLdb` adapter, run the following commands:

```bash
sudo apt-get install python3-dev
sudo apt-get install libmysqlclient-dev
sudo apt-get install zlib1g-dev
sudo pip3 install mysqlclient
```

After installing the requisite modules (which you will do only once on a given machine), the next thing is for you to connect with the database.

## How to connect to MySQL database through Python

To connect to a MySQL database from your Python application, you need to first invoke your connector so that it creates a link between your application and the database. You do this by importing the specific connector module.

In our case, we are using `MySQLdb`, so you have to import the `MySQLdb` module.

```python
import MySQLdb
```

To make it easier for me when working with such modules, I like to assign them an alias, that I will be using throughout my application instead of having to recall the name of the module anytime I want to use it. So, in this case, I will give it an alias called `DB`. As such, the import statement now looks like this:

```python
import MySQLdb as DB
```

After, importing the module, you have to create the actual connection with the help of the `connect` method that comes with the module. This `connect` method takes in the following arguments.

*   Host (`host`)
    
*   Port (`port`)
    
*   Username (`user`)
    
*   Password (`passwd`)
    
*   Database name (`db`)
    

It, therefore, looks like this:

```python
db_connect = DB.connect(host="", port="", user="", passwd="", db="")
```

Assume, you have a MySQL database on your local machine with the name of `bookstore`, username of `ehoneah` and password of `obed123` which is running on localhost with port 3306. The code for connecting to this database will be:

```python
db_connect = DB.connect(host="localhost", port=3306, user="ehoneah", passwd="obed123", db="bookstore")
```

Remember to change the details to the exact details that you used to create your database.

After establishing the connection, you will need to be able to run your SQL queries directly in your Python code. But wait, not so fast...

How will it be possible to write SQL code in Python and expect the Python interpreter to not get confused and not throw errors at you?

To ensure this doesn't happen, the connector that you choose which in our case was `MySQLdb` provides you with a `class` that enables you to write SQL queries in your Python code.

This class is called a `cursor`. You, therefore, have to create an instance of the cursor `class` on your connection. Remember that you assigned the outcome of your database connection to a variable (`db_connect` is what we used above -&gt; ie: connection object). The instance of the cursor depends on the connection object that you created. We will also call the instance of the cursor we are creating `db_cursor`.

The code will therefore look like this:

```python
db_cursor = db_connect.cursor()
```

Now that we have an instance of the cursor class, you can go ahead and execute any sort of SQL query. You do that by calling the `execute` method and passing the SQL statement as its argument.

So, let's assume that our fictitious `bookstore` database has a table called `books`. If we want to select everything from the `books` table, the SQL query will be:

```sql
SELECT * FROM books
```

Hence, in our Python code, we will have something like this:

```python
db_cursor.execute("SELECT * FROM books")
```

In this case, all the selected data will be stored in the cursor object. Hence, to get the data, you would have to fetch the data from that cursor object. The code below will enable you to fetch all the data that was selected.

```python
rows_selected = db_cursor.fetchall()
```

If there is a collection of data returned from your query then you can access each of them with the help of a loop. An example will be:

```python
for row in rows_selected:
    print(row)
```

Now, let's put together all the codes. Here is what it looks like:

```python
# import the mysql connector module
import MySQLdb as DB
# establish a database connection
db_connect = DB.connect(host="localhost", port=3306, user="ehoneah",                  passwd="obed123", db="bookstore")
# create a cursor to enable SQL queries
db_cursor = db_connect.cursor()
# execute SQL code
db_cursor.execute("SELECT * FROM books")
# accessing the data retrieved
rows_selected = db_cursor.fetchall()
for row in rows_selected:
    print(row)
```

There are a few more things and best practices that you need to follow when you are doing these and I may discuss them in subsequent write-ups.

### Conclusion

I hope you got value from reading this, and I look forward to writing more on the topic and sharing some of the insights I discover through using it.

If you enjoyed this content and would like to support me, subscribe to my [YouTube channel](https://youtube.com/@ehoneahobed?sub_confirmation=1) for more educational videos and also follow this [blog](http://hashnode.com/@ehoneahobed).

You can also give me a follow on [Twitter or send me a DM](https://ehoneahobed.com/twitter) and I am will be happy to chat with you.