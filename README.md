# mongodb-command
reference : https://www.mongodb.com/docs/mongodb-shell/run-commands/

# get started with  mongosh

## start mongosh
```bash
mongosh
```
and hit enter
## To display the database you are using, type db:

```bash
db
```
## To list the databases available to the user, use the helper show dbs.

```bash
show dbs
```

## To switch databases,
```bash
use <database>
```

## To create a new database

```bash
use <database>
```
## To terminate a running command or query in mongosh, press Ctrl + C:
```bash
press Ctrl + C
```

# CRUD operations create, read, update, and delete documents.
## Insert Documents

The MongoDB shell provides the following methods to insert documents into a collection:`

    - To insert a single document, use `db.collection.insertOne().`
    If the document does not specify an _id field, MongoDB adds the _id field with an ObjectId value to the new document.
    insertOne() returns a document that includes the newly inserted document's _id field value.
    ```bash
    db.movies.insertOne({title: "The lion king", year: 2018})
    ```

    -  To insert multiple documents, use `db.collection.insertMany().`
    db.collection.insertMany() can insert multiple documents into a collection. Pass an array of documents to the method. If the documents do not specify an _id field, MongoDB adds the _id field with an ObjectId value to each document.

    ```bash
 db.movies.insertOne([{title: "The lion king", year: 2018}, {title: "The lion king 2", year: 2019}])
    ```
    insertMany() returns a document that includes the newly inserted documents' _id field values.

## Read (Query) Documents
Use the db.collection.find() method in the MongoDB Shell to query documents in a collection.
-  Read All Documents in a Collection

To read all documents in the collection, pass an empty document as the query filter parameter to the find method.
```bash
// swich to db : use <database>
db.movies.find()
```

-    Specify Equality Condition
  Lest you return all movies that their year is `2019`, to do this you will need to specify a condition as `{<field>:<value>}` in the `.find()` method's object

```bash
db.movies.find({<year>:<value>})
that is : db.movies.find({year: 2019})
```

-    Specify Conditions Using Query Operators

Use [query operators](https://www.mongodb.com/docs/manual/reference/operator/query/#query-selectors) in a query filter document to perform more complex comparisons and evaluations. Query operators in a query filter document have the following form:
`{ <field1>: { <operator1>: <value1> }, ... }`
```bash

use <database>
db.movies.find( { rated: { $in: [ "PG", "PG-13" ] } } )
// his reads : return all movies from the <database> collection which are either `rated` `PG or PG-13`
```
The  Query Selectors are categoriesed into Comparison, Logical, Element, Evaluation, Geospatial, Array , Bitwise
We also have Projection Operators, Miscellaneous Operators

- Read single document usinf findOne() method
  ```bash
  db.accounts.findOne( { <filed>: <value> } )
  ````
## Update Documents
The MongoDB shell provides the following methods to update documents in a collection:
To update a document, MongoDB provides update operators, such as $set, to modify field values.

To use the update operators, pass to the update methods an update document of the form:
```bash
{
  <update operator>: { <field1>: <value1>, ... },
  <update operator>: { <field2>: <value2>, ... },
  ...
}
```
    -    To update a single document, use db.collection.updateOne().
    Update a Single Document
Use the `db.collection.updateOne()` method to update the first document that matches a specified filter.
```bash
// Using the [Update operator](https://www.mongodb.com/docs/manual/reference/operator/update/). $set add the filed if it is noit there if it is there it will update the vslue
 db.movies.updateOne({"title":"The lion king"}, {$set: {rating: 4}})
```
```bash
db.movies.updateOne({"title":"Fast and furios"}, {$set:{title:"Fast and furious"}})
```
when using the document Id to look it up before updating , ensure you pass the id in ObjectId( )method beacuse Mongodb store _id as an ObjectId not string
```bash
db.movies.updateOne({_id:ObjectId("67c2f41307676864f60a61b7")}, {$set:{title:"Fast and furious2"}})
```
    -    To update multiple documents, use db.collection.updateMany().
Use the `db.collection.updateMany()` to update all documents that match a specified filter.
    -    To replace a document, use db.collection.replaceOne().
    To replace the entire content of a document except for the _id field, pass an entirely new document as the second argument to db.collection.replaceOne().

## Delete Documents

The MongoDB shell provides the following methods to delete documents from a collection:
    -    To delete multiple documents, `use db.collection.deleteMany()`.
To delete all documents from a collection, pass an empty filter document {} to the 
```bash
db.movies.deleteMany({})
```
If you want to delete all documents from a large collection, dropping with the db.collection.drop()
Delete All Documents that Match a Condition
`db.movies.deleteMany( { title: "Titanic" } )`
    -    To delete a single document, `use db.collection.deleteOne()`.
    To delete at most a single document that matches a specified filter (even though multiple documents may match the specified filter) use the db.collection.deleteOne() method.
    ```bash
    db.movies.deleteOne( { cast: "Brad Pitt" } )
    ```
