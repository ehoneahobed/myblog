# Mongoose Made Simple: A Beginner's Guide to Getting Started

As I stated in my previous article, I started learning about the MERN stack some few days ago and as I always advocate for, I learned it by building real life projects. One of the technologies that you will hear about if you have chosen to learn the MERN stack is `mongoose`.

What is it and what is its role in the MERN stack? For those who do not know yet, MERN is an acronym for `MongoDB`, `Express`, `React JS`, and `Node JS.` You would have realized that the stack didn't have `mongoose` in there so why is it necessary to learn it if you choose to learn this stack?

Well, that is the purpose of this article. I will explain what it is, why you need it, and how to use it to make your life easier when working with this stack.

## What is Mongoose

Have you heard of NoSQL databases before? One of the most popular NoSQL databases out there is MongoDB. However, for a beginner or even with some Pros, working with a database like MongoDB isn't easy at all.

To make it easier, a library called Mongoose was created. This abstracts and simplifies most of the complex things that one expects to do with a database.

It enables you to model your application's data and manipulate the data through the models that you create. As such, it is known as an "**Object Data Modeling (ODM)"** library.

It also handles a lot of the tasks associated with managing a NoSQL database such as data validation and formatting, for you.

## Why use Mongoose

As explained above, Mongoose makes working with MongoDB easy and abstracts a lot of the difficult aspects. As such, it provides a lot of advantages, and most people working with MongoDB and Node.js love to use it for these advantages.

1. It simplifies data modeling (You will observe that for yourself soon)
    
2. It improves productivity (Spend less time but achieve more)
    
3. It handles data validation for you
    

## How to install Mongoose

You require Node.js and npm (the package manager for Node.js) in order to install Mongoose on your computer.

Assuming you have node installed, you can go ahead to install Mongoose using the following npm command:

```javascript
npm install mongoose
```

By running the command above, you will have Mongoose installed and added to your project's dependencies.

This can also be achieved with the use of the `--save` flag, which will also add it to your project's dependencies in the `package.json` file:

```javascript
npm install --save mongoose
```

After installing Mongoose on your computer and adding it to your project's dependencies, you can use it by requiring it in any of the files where you would want to interact with your MongoDB database. One of these files is likely to be your `server.js` file or `index.js` file depending on the naming convention you choose to go with.

If you are using the MVC (Model Controller View) architecture for your app, then you may need to require it in all your models. Use the command below to require Mongoose in your script:

```javascript
const mongoose = require('mongoose');
```

## Connecting to a MongoDB database using Mongoose

Once we have required the Mongoose module in our application, we can use its `connect` method to connect to your MongoDB database. You will, however, first need to get your MongoDB database connection string.

Let's assume your connection string is `mongodb://localhost/testdb`. You can just go ahead and pass the string to the `connect` method.

Since the connection is an asynchronous process and may take some time, you will usually want to check that it was able to connect successfully before opening up your app to listen on a port to ensure that your server is able to receive and respond to requests.

You may also want to capture any errors and log them so that you are always informed about the state of your connection. An example is illustrated below.

```javascript
// requiring Mongoose module
const mongoose = require('mongoose');
// connecting to db
mongoose.connect('mongodb://localhost/testdb')
.then(() => {
    // listen for requests
    app.listen(5000, () => {
    console.log(`Connected successfully to the database and listening on port 5000`)});
})
.catch((error) => {
    console.log(error);
})
```

It is, however, not advisable to directly put your MongoDB connection string in your code. This is because your connection string will usually contain your `username` and `password` and exposing this in your code means people can easily find it and get access to your database when you upload your codes to online repositories like GitHub.

It is thus advisable to store your connection string as an environment variable and access it as such. An example using an environment variable named `MONGODB_URI` will look like:

```javascript
// requiring Mongoose module
const mongoose = require('mongoose');
// connecting to db
mongoose.connect(process.env.MONGODB_URI)
.then(() => {
    // listen for requests
    app.listen(5000, () => {
    console.log(`Connected successfully to the database and listening on port 5000`)});
})
.catch((error) => {
    console.log(error);
})
```

Also, you may be getting some deprecation warnings depending on the version of `Mongoose` that you are using. To prevent these from showing up, you have to set your `strictQuery` value. You can do that by putting this line of code `mongoose.set('strictQuery', false);` right above your Mongoose connection code. You may also need to set `useNewUrlParser` and `useUnifiedTopology` to true. The example below incorporates all of those.

```javascript
// requiring Mongoose module
const mongoose = require('mongoose');
// connecting to db
mongoose.set('strictQuery', false);
mongoose.connect(process.env.MONGODB_URI, {useNewUrlParser: true, useUnifiedTopology: true})
.then(() => {
    // listen for requests
    app.listen(5000, () => {
    console.log(`Connected successfully to the database and listening on port 5000`)});
})
.catch((error) => {
    console.log(error);
})
```

Now that we have successfully connected to our MongoDB database through Mongoose, we can proceed to create models for manipulating our database.

## How to define a Mongoose Model

To do that, we first need to create a `Schema` for our data. This refers to the structure of the data in a MongoDB collection. It involves telling your database the names of the fields that each document is going to have and the type of data expected for each field, as well as any other constraints.

To create a schema in Mongoose, you will need to require the Mongoose module and use the `mongoose.Schema` constructor.

### How to create a Mongoose Schema

Let's say you are creating a `Schema` for a blog collection in your MongoDB database, you will have to approach it as illustrated below:

```javascript
const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({
  title: String,
  author: String,
  category: String,
});
```

In the above example, we are saying that our post collection will be made up of three fields (`title`, `author`, `category`) and each of these fields will only take in `strings`. Any type of data provided like `numbers` will not be accepted. Do you remember when I told you that Mongoose does the validation for you? Yeah, this is what I was referring to.

You can also set some constraints, like making particular fields required or unique. An example containing such constraints will also look like this:

```javascript
const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({
  title: { type: String, required: true, unique: true },
  author: String,
  category: String,
});
```

In most cases, too, you may want to add timestamps marking when the data was created and when it was updated and store them in the database. Even though you can approach them just like any of the above fields, there is an easy way around it. Remember that Mongoose helps to boost your productivity, do less but get more (hahaha...)

The easiest way to add time timestamps to your database collection is to add another object `{ timestamps: true }` as a second argument to the `mongoose.Schema()` constructor. That will look like the example below:

```javascript
const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({
  title: { type: String, required: true, unique: true },
  author: String,
  category: String,
}, { timestamps: true });
```

Once you have defined your schema, you can use it to create a Mongoose model, which allows you to perform CRUD (**C**reate, **R**ead, **U**pdate, **D**elete) operations on the collection. For example, you might use the Post model to create new documents, find existing documents, update existing documents, or delete documents from the collection.

### How to create a Mongoose model

After creating the schema, use the `mongoose.model()` function to compile the schema into a model. Below is an example for the `postSchema` we created above.

```javascript
const Post = mongoose.model('Post', postSchema);
```

One thing to note about the syntax above is that the first argument passed to the `mongoose.model()` function should be the singular form of the name of your database collection.

This means that when the above code is used and models are operated on, a collection known as `posts` will be created in your database if it doesn't already exist.

The complete code for generating the model (including the schema) will now be like this:

```javascript
const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({
  title: { type: String, required: true, unique: true },
  author: String,
  category: String,
}, { timestamps: true });

const Post = mongoose.model('Post', postSchema);
```

You will have to export the model to be able to use it in other parts of your application. In such cases, your last line should look like this:

```javascript
module.exports = mongoose.model('Post', postSchema);
```

## How to perform CRUD operations on Mongoose Models

Mongoose models provide several methods that allow you to perform CRUD (create, read, update, delete) operations on a MongoDB collection.

### Creating documents with Mongoose Models

There are multiple ways that you can create a new document with the help of a Mongoose model but the easiest way is to use `.create()` method on a model to create a new document in a MongoDB collection.

The `.create()` method is a shortcut for **creating** and **saving** a new document in a single operation. It creates a new document, inserts it into the database, and returns the document to you.

NB: If you exported your model and are going to be using it in a file different from where you created it, then you will need to require the model.

```javascript
const Post = require('../models/postModel');

const createPost = async (req, res) => {
    const {title, author, category} = req.body; 
    try {
        const post = await Post.create({title, author, category});
        res.status(200).json(post); 
    } catch (error) {
        res.status(400).json({error:error.message});
    }
}
```

The implementation of the function above may depend on how you are architecting your app. In some instances, you will not create a separate function like I have here but just add it as an anonymous function in your route. It is totally up to you but let's focus on the Mongoose part for now.

What we did above was to make sure we and access to the Mongoose Model we created earlier by requiring it and calling it `Post.`

The next thing to take note of is that we called the `create()` method on the model and pass an object containing the data to be stored in the database. The data in it is derived from the body of the `http` or `https` request. Remember that you can equally hard code it into it if you want.

```javascript
const post = Post.create({title, author, category});
```

```javascript
const post = Post.create(
  {
    title: 'My first Blog post',
    author: 'Ehoneah Obed',
    category: 'Health'
  });
```

By doing that, the data will be stored inside the database and the document will then be returned if everything was successful.

### Reading documents using Mongoose Models

o read documents from a MongoDB collection using a Mongoose model, you can use the `.find()` method.

The `.find()` method retrieves all documents that match the specified query criteria. If no query criteria is specified, it returns all documents in the collection.

```javascript
const post = Post.find();
```

Without any arguments, the code above will return all post documents available in the database. To select just one item or a specific group of items, you would have to pass some arguments to the find method.

For example, if I want it to get only documents with `author` to be `Ehoneah Obed`, the code will be like this:

```javascript
const post =Post.find({ author: 'Ehoneah Obed' }
```

### Deleting documents through Mongoose Models

To delete documents from a MongoDB collection using a Mongoose model, you can use the `.deleteOne()` or `.deleteMany()` method.

The `.deleteOne()` method deletes the first document that matches the specified query criteria. The `.deleteMany()` method deletes all documents that match the specified query criteria.

```javascript
// Delete one document
Post.deleteOne({ title: 'My First Blog Post' });

// Delete many documents
Post.deleteMany({ author: 'Ehoneah Obed' });
```

In Mongoose, you can also use the `.findOneAndDelete()` method to delete a single document from a collection.

The `.findOneAndDelete()` method finds the first document that matches the specified query criteria and deletes it, returning the deleted document to you.

```javascript
// Delete one document
Post.findOneAndDelete({ title: 'My First Blog Post' });
```

### Updating documents using Mongoose Model

To update a document in a MongoDB collection using a Mongoose model, you can use the `.updateOne()` or `.updateMany()` method.

The `.updateOne()` method updates the first document that matches the specified query criteria. The `.updateMany()` method updates all documents that match the specified query criteria.

In Mongoose, you can also use the `.findOneAndUpdate()` method to update a single document in a collection.

The `.findOneAndUpdate()` method finds the first document that matches the specified query criteria, updates it, and returns the updated document to you.

#### Extra Info -&gt; Not so basic

## Model methods and statics explained

These are additional but helpful aspects of using Mongoose. You can ignore it for now and come back to it later.

In Mongoose, you can define model methods and statics to add custom functionality to your models. By default, there are a lot of functionalities that are available for use on any Mongoose model. But sometimes, you may want to create a specific functionality and that is when methods and statics become necessary.

### Model methods in Mongoose

Model methods are instance methods that are available on documents returned from queries. For example, you might define a `fullName` method on a `User` model that concatenates the `firstName` and `lastName` fields of a user document.

To define a model method in Mongoose, you can use the `.method()` function on the schema. Here is an example of how you might define a `fullName` model method:

```javascript
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
});

userSchema.methods.fullName = function() {
  return this.firstName + ' ' + this.lastName;
};
```

You can then call the `fullName` method on a user document like this:

```javascript
const user = User.findOne({ _id: 123 });
console.log(user.fullName());
```

### Model Statics in Mongoose

Model statics are static methods that are available on the model itself. For example, you might define a `findByFullName` static method on a `User` model that finds a user by their full name.

To define a model static in Mongoose, you can use the `.static()` function on the schema. Here is an example of how you might define a `findByFullName` model static:

```javascript
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
});

userSchema.statics.findByFullName = function(name) {
  const fullName = name.split(' ');
  const firstName = fullName[0];
  const lastName = fullName[1];
  return this.findOne({ firstName, lastName });
};
```

You can then call the `findByFullName` static method on the `User` model like this:

```javascript
const user = User.findByFullName('John Smith');
console.log(user);
```

### Note for readers who are totally new to NoSQL databases but familiar with SQL databases:

In a traditional SQL database, a **table** is made up of **rows** and **columns**, where each **column** represents a **different piece of data** and each **row** represents a **unique record**.

In a NoSQL database like MongoDB, the equivalent of a **table** is a **collection**, and the equivalent of a **row** is a **document**.

However, unlike a SQL table, a **MongoDB collection does not have a fixed set of columns**. Instead, each document in the collection can have a different set of fields (also known as **properties**).

## Conclusion

I am really excited to explore more about the MERN stack and use it to build a lot more projects. As I keep learning and discovering new things, I will continue to share them with you through this blog, my YouTube channel, and on Twitter as well. If you don't want to miss any of them or want to connect with me personally or support me in any way or form, then take any or all of these 3 actions.

1. Subscribe to this [**blog or follow the blog**](http://hashnode.com/@ehoneahobed)
    
2. Subscribe to my [**YouTube Channel**](https://youtube.com/@ehoneahobed)
    
3. Follow me on [**Twitter and send me a DM**](https://ehoneahobed.com/twitter) (I long to hear from you)