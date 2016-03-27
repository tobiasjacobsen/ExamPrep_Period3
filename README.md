##Explain, generally, what is meant by a NoSQL database
>A NoSQL (originally referring to "non SQL" or "non relational") database provides a mechanism for storage and retrieval of data which is modeled in means other 
>than the tabular relations used in relational databases. NoSQL databases are increasingly used in big data and real-time web applications.

![alt text](http://dataconomy.com/wp-content/uploads/2014/07/SQL-vs.-NoSQL.png "SQL vs noSQL")

*Sources* <br>
[Wikipedia](https://en.wikipedia.org/wiki/NoSQL)

##Explain Pros & Cons in using a NoSQL database like MongoDB as your data store, compared to a traditional relational SQL Database like MySQL.

###General overview: 
In a traditional relational approach, an article object might be related to a category (an object), a tag (another object), a comment (another object), and so on. 
Relationships between different types of data were specified in the database schema, these relational databases could be queried with a standard Structured Query Language (SQL). <br>
**Cloud computing**: Data has to be spread across multiple servers easily without disruption. In a complex SQL database, this is difficult because many queries require multiple large tables to be joined together to provide a response. 
Executing distributed joins is a very complex problem in relational databases.<br>
**Social media**: SQL databases are extremely efficient at storing structured information, and workarounds or compromises are necessary for storing and querying unstructured data.<br>
**Agile development** methods mean that the database schema needs to change rapidly as demands evolve. SQL databases require their structure to be specified in advance, which means any changes to the information schema require time-consuming ALTER statements to be run on a table.

###Pros and Cons

- (+) Simplicity of design. (data does not have to be normalized. Just save everything you need, in a document, for a specific domain.)
- (+) Some operations faster in NoSQL. (especially when your data needs are "non-relationel in nature - you typically store and request data from the same domain)
- (+) Simpler "horizontal" scaling to clusters of machines. (Just add another machine to extend storage space. Speed will be constant)

- (-) Compromise consistency in favor of availability (CAP theorem).
- (-) No dedicated noSQL-language like SQL and lack of standardized interfaces (it's easier to design an ORM if you have this).
- (-) Huge previous investments in existing relational databases.
- (-) Mostly lack ACID

*Sources* <br>
[Wikipedia NoSQL](https://en.wikipedia.org/wiki/NoSQL) <br>
[Wikipedia CAP Theorem](https://en.wikipedia.org/wiki/CAP_theorem) <br>
[MEAN slides NoSQL and MongoDB](http://js2016.azurewebsites.net/mongoDB/mongo.html#7) <br>
[ACID](https://en.wikipedia.org/wiki/ACID) <br>

##Explain how databases like MongoDB and redis would be classified in the NoSQL world 

###MongoDB
Is a **document oriented** database. Documents are **independent units** which makes performance better (data is read contiguously off disk) and makes it easier to distribute data across multiple servers while preserving its locality. <br>
**Application logic is easier** to write. No need to translate between objects in your application and SQL queries, you can just turn the object model directly into a document. 
(sure, but you have ORM with SQL) <br>
**Unstructured data** can be stored easily, since a document contains whatever keys and values the application logic requires. <br>

###Redis
Redis is an open source, in-memory data structure store, used as database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. **Basically key/value storage**.<br>
Redis typically holds the whole **dataset in memory**, and saves to disk every two seconds.

####Example
```javascript
set users:leto '{"name": leto, "planet": dune, "likes": ["spice"]}'
```<br>
```javascript
get users:leto
```

**Redis as a Session Store**: [MEAN Slides Redis](http://js2016.azurewebsites.net/redis/redis.html#24)

*sources* <br>
[MongoDB](https://www.mongodb.com/document-databases) <br>
[Redis](http://redis.io/topics/introduction) <br>
[Wikipedia Redis](https://en.wikipedia.org/wiki/Redis)<br>

##Explain reasons to add a layer like Mongoose, on top on of a schema-less database like MongoDB
Mongoose is an **ORM-like** tool for MongoDB. Mongoose provides a straight-forward, schema-based solution to model your application data. It includes built-in type casting, validation, query building, business logic hooks and more, out of the box.<br>
Mongoose adds another layer of robustness on top of MongoDB. Write **less code**, **easier to read code** (object modeling) and **schema validation**. <br>
MongoDB is schema-less and Mongoose adds schemas. This might seem counterintuitive at first... but Real life data has (often) **structure** and (often) **types**<br>

*sources* <br>
[mongoose](http://mongoosejs.com/) <br>
[MEAN slides Mongoose](http://js2016.azurewebsites.net/mongoose/mongoose.html#3)

##Explain, using relevant examples, the strategy for querying MongoDB (all CRUD operations) 

```javascript
var getJoke = function (id, callback) {
    var db = getConnection();

    db.collection('jokes').findOne({'_id': new ObjectId(id)}, function (err, data) {
        if (err) {
            callback(err);
        }
        callback(null, data);
    });
};
```

###Refer to the following projects for full examples

DB CRUD: [Github project: MongoEx1../model/joke.js](https://github.com/hardboilr/MongoEx1/blob/master/model/joke.js) <br>

REST CRUD: [Github project: MongoEx1../routes/jokes.js](https://github.com/hardboilr/MongoEx1/blob/master/routes/jokes.js)


##Demonstrate, using a REST-API, how to perform all CRUD operations on a MongoDB 
##Explain the benefits from using Mongoose, and provide an example involving all CRUD operations 
##Explain how redis "fits" into the NoSQL world, and provide an example of how to use it. 
##Explain, using a relevant example, how redis (or a similar) can increase scalability (drastic) for a server using 
server side sessions 
##Explain, using a relevant example, a full MEAN application including relevant test cases to test the REST-API 
(not on the production database) 