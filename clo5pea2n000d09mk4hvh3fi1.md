---
title: "Databases 101: What every beginner needs to know"
datePublished: Wed Oct 25 2023 12:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clo5pea2n000d09mk4hvh3fi1
slug: databases-101-what-every-beginner-needs-to-know
canonical: https://learninbits.com/databases-101-what-every-beginner-needs-to-know/
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698207034008/4b6b7693-eb9f-4b8d-bdbe-6f5d917ebb4c.png
tags: mysql, databases, sql, rdbms, database-design

---

If you are new to software engineering or web development then the word database may seem like a buzzword to you but there is a reason why it is such a common word among developers at all levels.

Almost every website or web application that you build will be powered by one database or the other. If you are not familiar with what databases are and why they are considered so important, then this post will be a great start for you.

Let's get started by getting to know what it is.

## What is a database

Most websites or web applications that you have used before have content on them and these content should have a place where they are stored. For example, this particular post that you are reading is one of many posts that I have published on my blog. All this content is stored in what we call a database.

Another example I can give you is how social media platforms like Twitter and Facebook work. On those platforms, users post content or upload different types of media like images and videos. All of these would be stored in the databases that are connected to the platform.

**A database can therefore be considered as an organized collection of data**.

An important point to take note of is that all databases are not the same. The structure of the database that powers this blog may be totally different from the one that powers Facebook. The difference in structure of databases is important because when storing data it is important to find out the best way to store them in order to ensure that retrieval of the data can easily be done promptly.

Let me further explain this with a real-life analogy. There are several support markets out there but almost every one of them has a certain way of arranging the items in the shop. Shop owners usually arrange them in a way that they can easily locate each item when needed.

There are other key considerations when it comes to deciding on what kind of structure one should use when storing data in a database. These differences in structure have led to different types of databases. Let's therefore proceed to take a look at some different types of databases out there.

## Types of databases

You will usually hear about two major types of databases (Relational databases and NoSQL databases) but in this post, I will expose you to a third one as well.

1. **Relational Databases:**
    
    These refer to the storage of data in the form of tables. When I say tables, I am referring to ordinary tables that you create in your documents or spreadsheets which are characterized by columns and rows. A single database can have multiple tables.
    
    The columns refer to the fields that are in your data whereas the rows refer to the records that you put in your database. For example, if I create a relational database for a social media platform, I may have tables for users, posts, etc. If we take the users table, we may want to add fields like `full name`, `username`, `bio`, `email address` and many others. These fields will therefore represent the `columns` in that database table.
    
    If a particular user goes ahead and stores their details in this database, you can then save the details under the respective columns in the database. This record that you add is what we are referring to as rows.
    
    Popular examples include MySQL, PostgreSQL and Oracle
    
2. **NoSQL Databases**:
    
    With NoSQL Databases, the data is not stored in a table. There are a couple of different ways in which NoSQL databases can be stored. How data is stored here can be used to describe the type of NoSQL database. The available types include document-based, key-value stores and graph databases. A popular example that you will learn about is MongoDB
    
3. **In-Memory Databases**:
    
    The previous two types of databases that I have talked about store data on the hard disk of the server or computer on which they are created. This type of database on the other hand stores data in the system's main memory rather than the disk therefore ensuring faster access to the data.
    

## Why you need to use a database

There are other ways of storing data like using files, local storage or data structures like arrays in your code so why do you even need to bother using a database?

Databases provide additional benefits that you won't get with the other types of data storage. Some of these include:

* **Data integrity**: Most databases that are available provide mechanisms to ensure that the data you store in them remains consistent and accurate.
    
* **Scalability**: Usually the size of data stored by an application grows with time. For example, the more people sign up for a new platform, the more data it needs to store in the database. Databases are therefore equipped to handle such an increase in load while ensuring smooth performance.
    
* **Data retrieval**: Databases can provide efficient ways to search, sort, and retrieve data when needed.
    
* **Concurrency**: Multiple users can access the data stored in the database simultaneously without any conflicts.
    
* **Security**: Databases have inbuilt security features that enable you to protect sensitive data stored in them.
    

## Key terminologies

Below are a few of the key terminologies that you need to know when working with databases. Note that this is not an exhaustive list of terminologies and we will cater for others in subsequent posts.

* **Schema**: This refers to a blueprint defining the database structure, including tables, columns, and relationships.
    
* **Query**: This refers to a request that you make to retrieve, update, or delete data in the database.
    
* **Primary key**: This refers to a unique identifier for a record in a table.
    
* **Foreign key**: This refers to a field in a given table that links to the primary key of another table which establishes the link between two database tables.
    

## Conclusion

I hope by going through this post, you have now gotten a basic understanding of what databases are and are ready to delve into more content relating to databases. I will be writing more posts on the various types of databases and how to use them. Do well to follow this blog and turn on your notification so you can informed anytime I publish a new post.

You can also connect with me on [Twitter (@ehoneahobed)](https://ehoneahobed.com/twitter) and I will be happy to chat with you.