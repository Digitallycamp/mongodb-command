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
