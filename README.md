# MongoDB

It is a NoSQL DB that stores data in _flexible_, _JSON_ like documents, making it easy to scale and handle large volumes of unstructured data.

- It was first released in 2009.

> MongoDB stores data in **collections** and **documents**.

### Collection

- It is a group of mongoDB **documents**.
- Like a SQL Table

### Documents

- It is a set **key-value** pairs.
- Like a SQL Row

### Fields

- A key value pair within a document.
- Like a SQL column.

> **_MongoDB_** ==> **_Collections_** ==> **_Documents_** ==> **_field_**

example: _students_ : _collection_

```json
[
    {
        name: "Ankit",
        age: 22,
        course: B.tech
    }
    {
        name: "Rohan",
        age: 21,
        course: "BBA"
    }
    {
        name: "Deepak",
        age: 23,
        course: "BCA"
    }
]
```

# SQL vs NoSQL

### Scalablity

- **NoSQL**: _Horizontally_ scalable by adding more servers and distributing the loads to multiple servers.

- **SQL**: Veritcally scalable by adding more resources to the single server. which has limits and costly

### Flexablity

- **NoSQL**: Schema-less design, provides more flexiblity. More flexible.

- **SQL**: Requires a predefined schema. Less flexible

### Performance

- **NoSQL**: High speed read write operations making it ideal real time processing and analytics.

- **SQL**: It suffer from slower read/write operations when dealing with very large data set due to ACID transactions.

### On Basis of Structure

- **NoSQL**: Ideal for unstructured data.

- **SQL**: Ideal for structured data.

# Working with MonogDB

#### To open the monogDB shell, use below command:

```shell
mongosh
```

#### To check available databases:

```shell
show dbs
```

#### To CREATE the database

```shell
use databaseName
```

#### To DELETE the database

```shell
db.dropDatabase()
```

#### To DELETE the collection

```shell
db.collectionName.drop()
```

#### To CREATE collections and insert data on DB

```shell
db.collectionName.insertOne({name:"Ankit", age:"22"})
```

#### To INSERT data collections

```js
db.collectionName.insertOne({ name: "Ankit", age: "22" });
```

#### To READ data

```shell
db.collectionName.find()
```

# CRUD Operations

#### CREATE

1. **insertOne()**

```shell
db.cars.insertOne({ "brand": "Mahindra", "model": "Thar", "features": ["touch screen", "reverse camera", "airbags"]})
```

2. **insertMany()**

```js
db.cars.insertMany([
  {
    brand: "Mahindra",
    model: "Thar",
    features: ["touch screen", "reverse camera", "airbags"],
  },
  {
    brand: "Toyota",
    model: "Fortuner",
    features: ["4WD", "cruise control", "hill assist", "touch screen"],
  },
  {
    brand: "Hyundai",
    model: "Creta",
    features: ["sunroof", "airbags", "bluetooth", "wireless charging"],
  },
  {
    brand: "Maruti Suzuki",
    model: "Brezza",
    features: ["keyless entry", "reverse camera", "ABS", "infotainment system"],
  },
  {
    brand: "Kia",
    model: "Seltos",
    features: ["air purifier", "LED headlamps", "sunroof", "ambient lighting"],
  },
]);
```

> Note: Nested document can also be used to store data.

---

#### READ

1. find()

- It will return all the documents of that particular collection.

```shell
# db.collectionName.find()
carDealership> db.cars.find()  # with no condition

# with condition
carDealership> db.cars.find({"brand" : "Mahindra"})

```

2. findOne()

- It return only one document from top most item from collection.

```shell
db.collectionName.findOne()
```

---

#### UPDATE

1. **updateOne()**

```shell
# syntax
db.collectionName.updateOne({condition}, {updation})

# example 1 :fupdating model
db.cars.updateOne(
    {"model" : "Thar"}, # condition checked
    {$set: {"model" : "Scorpio"}} # updation
)

# example 2 : adding color field
db.cars.updateOne(
    {"model" : "Thar"}, # condition checked
    {$push: {"color" : "Black"}} # updation
)

# example 3 : removing color value from field
db.cars.updateOne(
    {"model" : "Thar"}, # condition checked
    {$pull: {"color" : "Black"}} # updation
)

# example 3 : removing entire color field
db.cars.updateOne(
    {"model" : "Thar"}, # condition checked
    {$unset: {"color" : "Black"}} # updation
)

```

- `$set` : is used to set the new/updated values.

- `$unset` : used to remove field from document.

- `$push` : used to add new field to the document.

- `$pull` : used to remove values from document.

2. **updateMany()**

- It is used to update multiple documents at same time.

```shell
# example 1 : adding color field to document
db.cars.updateMany(
    {"features" : "reverse camera"}, # condi
    {$set: {"color" : "Black"}} # updation
)

# example 2: updating arrays of document
db.cars.updateMany(
    {"model" : "Scorpio"},
    {$push: {features: {$each:["Sunroof", "Automatic gear", "4X4"]}}}
)

# example 3: To set all the values of document
db.cars.updateMany(
    {}, # condition (All document)
    {$set: {color: "Black"}} # updation
)

```

- `$upsert` : It is a combination of insert and update. if no matching document will there, then in that case it create a new document.

---

#### DELETE

1. **deleteOne()**

```shell
db.collectionName({condition})

# example -1
db.cars.deleteOne(
    {_id: '6714e0f6f5ac09ada30eeec7'}
)

```

2. **deleteMany()**

```shell
db.collectionName.deleteMany({condition})

# example -1
db.cars.deleteMany({features: "airbags"})


```

# Data Types

- MonogDB stores data in **BSON** (Binary JSON) fromat.
- BSON includes all json datatypes and adds more.
- Choosing the correct data types is crucial for efficient storeage and quering.

1. `ObjectID` : (Act as Primary key, it is set by monogDB itself)

```shell
_id: ObjectId('6714e0f6f5ac09ada30eeec7'),
```

2. `String` : To store characters and strings.

```shell
firstName : "Ankit"
```

3. `Integer` : To store numerical values

```shell
rating: 5
```

4. `Double` : To store decimal values

5. `Boolean` : True/false

6. `Array` : To store multiple values

7. `Object/Embedded Document` :

8. `Date` :

```shell
db.cars.updateOne(
    {model: "City"},
    {$set: {launchedDate: new Date()}}
)
# O/P
launchedDate : ISODate("2024-08-21T14:23:00z")
```

9. `Null` :

```shell
middleName : null,
```

10. `Timestamp` : To store the timestamp values

```shell
ts : Timestamp(123453536,1),
```

# MongoDB Operators

### 1. Comparison Operators

1. `$gt` : **greater than**

```shell
db.cars.find({"horsepower": {$gt:390}})
```

2. `$gte` : greater than equal to

```shell
db.cars.find({"horsepower": {$gte:390}})
```

3. `$lt` : **less than**

```shell
db.cars.find({"horsepower": {$lt:300}})
```

4. `$lte` : **less than equal to**

```shell
db.cars.find({"horsepower": {$lte:300}})
```

5. `$ne` : **not equal to**

```shell
# Not eaul to : return all values that are not equal
db.cars.find({"horsepower": {$ne:300}})
```

#### Searching multiple values using array

6. `$in` : **in**, mathces values specified in an array

```shell
db.cars.find({"horsepower": {$in:[300,400]}})
```

7. `$nin` : **not in**

```shell
# opposite of in
db.cars.find({"horsepower": {$nin:[300,400]}})
```

### 2. Logical Operators

1. `AND` : Both condition must be true

```shell
db.cars.find({$and: [
    {fuel_type: "Electric"},
    {year : 2023}]}
)
```

2. `OR` : Any one condition needs to be true

```shell
db.cars.find({$or: [
    {fuel_type: "Electric"},
    {fuel_type:"Gasoline"}]}
)

```

3. `NOR` : Not of Both condition

```shell
db.cars.find({$nor: [
    {fuel_type: "Electric"},
    {fuel_type:"Gasoline"}]}
)

```

4. `NOT` : Not of the specified condition.

## Element operator

In MongoDB, the `$exists` operator is used to query documents based on whether a field exists or not, while the `$type` operator is used to query based on the type of a field.

### 1. **`$exists` Operator**

The `$exists` operator is used to match documents that contain (or do not contain) a specific field.

#### Syntax:

```javascript
{ field: { $exists: <boolean> } }
```

- `true`: If the field exists.
- `false`: If the field does not exist.

#### Example:

To find documents where the field `age` exists:

```javascript
db.collection.find({ age: { $exists: true } });
```

To find documents where the field `age` does **not** exist:

```javascript
db.collection.find({ age: { $exists: false } });
```

### 2. **`$type` Operator**

The `$type` operator is used to match documents where the field is of a specific BSON type.

#### Syntax:

```javascript
{ field: { $type: <type> } }
```

- `<type>`: The BSON data type you want to check for (e.g., `string`, `int`, `array`, etc.).

#### Example:

To find documents where the `age` field is of type `int`:

```javascript
db.collection.find({ age: { $type: "int" } });
```

Here’s a quick list of common BSON data types:

- `double`: 1
- `string`: 2
- `object`: 3
- `array`: 4
- `int`: 16
- `boolean`: 8
- `date`: 9

You can combine these operators in queries to make more complex searches based on the existence and type of fields.

### 3. Array operators

1. `$size` : return all documents that match specified array size.

```javascript
db.collection.find({ hobbies: { $size: 4 } });
```

2. `$all` : return all documents that match specified pattern.

```javascript
db.collection.find({ hobbies: { $all: ["play", "read"] } });
```

### 4. Cursor operators
1. **count** : `find().count()`

2. **skip**: `find().skip()` - used to skip documents of starting

3. **sort**: `find().sort("name":1)` -1 for descending
```javascript
db.cars.find().sort({year:1})
```

4. **limit** : `find().limit(5)`

# Aggregate Framework
It is powerful framework for complex operations like **filtring**, **grouping**, **sorting**, **reshaping**, and **summarizing** data in a flexible way via ***pipeline***.

Aggregation in MongoDB is a powerful feature that enables developers to perform complex data transformations and computations on collections of documents. By utilizing the aggregation framework, users can efficiently group, filter, and manipulate data to generate summarized results.



