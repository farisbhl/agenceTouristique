# MongoDB Essentials for MERN Tourism SaaS Platform

## 1. SQL vs NoSQL

### SQL (Relational Databases)
Examples: MySQL, PostgreSQL

- Data stored in tables
- Structured schema
- Uses rows and columns
- Relations between tables

### NoSQL (MongoDB)

- Document oriented database
- Data stored as **documents**
- Uses **BSON (Binary JSON)**
- Flexible schema
- Easier to scale for modern applications

Example Document:

```js
{
  name: "Ali",
  email: "ali@email.com",
  role: "tourist"
}
```

---

# 2. MongoDB Basic Concepts

### Database
Container for collections.

Example:
```
tourism_platform
```

### Collection
Similar to table.

Examples:

```
users
agencies
trips
bookings
reviews
```

### Document
Single record in a collection.

Example:

```js
{
  title: "Sahara Trip",
  price: 12000,
  duration: 3,
  location: "Tamanrasset"
}
```

---

# 3. MongoDB Basic Commands

### Database

Show databases

```
show dbs
```

Create or switch database

```
use tourismDB
```

Current database

```
db
```

Delete database

```
db.dropDatabase()
```

---

### Collections

Show collections

```
show collections
```

Create collection

```
db.createCollection("trips")
```

Delete collection

```
db.trips.drop()
```

---

# 4. CRUD Operations

CRUD = Create, Read, Update, Delete

---

## Create (Insert)

Insert one document

```js
db.trips.insertOne({
 title: "Sahara Adventure",
 price: 15000
})
```

Insert multiple documents

```js
db.trips.insertMany([
 {title:"Sahara Trip", price:12000},
 {title:"Desert Camping", price:9000}
])
```

---

## Read (Find)

Get all documents

```js
db.trips.find()
```

Find specific document

```js
db.trips.find({price:12000})
```

Find one document

```js
db.trips.findOne({title:"Sahara Trip"})
```

Pretty format

```js
db.trips.find().pretty()
```

---

## Sorting

Ascending

```js
db.trips.find().sort({price:1})
```

Descending

```js
db.trips.find().sort({price:-1})
```

---

## Limit Results

```js
db.trips.find().limit(5)
```

---

## Comparison Operators

Examples:

```
$eq   equal
$ne   not equal
$gt   greater than
$lt   less than
$gte  greater or equal
$lte  less or equal
$in   match values in array
```

Example:

```js
db.trips.find({price:{$gt:10000}})
```

---

# 5. Update Documents

Update one

```js
db.trips.updateOne(
 {title:"Sahara Trip"},
 {$set:{price:14000}}
)
```

Update many

```js
db.trips.updateMany(
 {duration:3},
 {$set:{duration:4}}
)
```

---

# 6. Delete Documents

Delete one

```js
db.trips.deleteOne({title:"Sahara Trip"})
```

Delete many

```js
db.trips.deleteMany({duration:3})
```

---

# 7. MongoDB Connection with Node.js

Install mongoose

```
npm install mongoose
```

Example connection:

```js
const mongoose = require("mongoose");

mongoose.connect("mongodb://localhost:27017/tourismDB")
.then(()=>console.log("Database connected"))
.catch(err=>console.log(err));
```

---

# 8. Mongoose Schema and Model

Schema defines the structure of documents.

Example Trip schema:

```js
const mongoose = require("mongoose");

const tripSchema = new mongoose.Schema({

 title:{
  type:String,
  required:true
 },

 price:{
  type:Number,
  required:true
 },

 duration:Number,

 location:String,

 createdAt:{
  type:Date,
  default:Date.now
 }

});

const Trip = mongoose.model("Trip", tripSchema);

module.exports = Trip;
```

---

# 9. CRUD from Node.js

Create document

```js
const trip = new Trip({
 title:"Sahara Adventure",
 price:15000
})

await trip.save()
```

Read documents

```js
const trips = await Trip.find()
```

Update document

```js
await Trip.updateOne(
 {_id:id},
 {$set:{price:16000}}
)
```

Delete document

```js
await Trip.deleteOne({_id:id})
```

---

# 10. Pagination (Useful for API)

Example:

```js
const {page=1,limit=10} = req.query

const trips = await Trip.find()
.limit(limit)
.skip((page-1)*limit)
```

---

# 11. Why MongoDB for our Project

MongoDB is suitable for the Tourism SaaS platform because:

- flexible schema
- scalable
- easy integration with MERN stack
- good performance for large data
- ideal for modern web applications
