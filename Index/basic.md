* Indexes support the efficient execution of queries in MongoDB. 
* Without indexes, MongoDB must perform a collection scan, i.e. scan every document in a collection, 
  to select those documents that match the query statement. 
* If an appropriate index exists for a query, MongoDB can use the index to limit the number of documents 
  it must inspect.


* MongoDB creates a unique index on the _id field during the creation of a collection.
* The _id index prevents clients from inserting two documents with the same value for the _id field. 
* You cannot drop this index on the _id field.
* To create an index using the Node.JS driver, use createIndex().
 
        collection.createIndex( { <key and index type specification> }, function(err, result) {
        console.log(result);
        callback(result);
        }

* The following example creates a single key descending index on the name field:

        collection.createIndex( { name : -1 }, function(err, result) {
        console.log(result);
        callback(result);
        }

* The createIndex() method only creates an index if an index of the same specification does not 
  already exist.
  
You can view index names using the `db.collection.getIndexes()` method. You cannot rename an index once created. Instead, you must drop and re-create the index with a new name.

    db.collection.getIndexes()


Index Types
-----------
MongoDB provides a number of different index types to support specific types of data and queries.

* Single Fiels Indexes
* Compound Indexes
* MultiKey Indexes
* Text Indexes
* Wildcard Indexes
* 2d Indexes
* 2dsphere Indexes
* geoHaystack Indexes
* Hashed Indexes

Single Field Indexes
--------------------
MongoDB provides complete support for indexes on any field in a collection of documents. By default, all collections have an index on the _id field, and applications and users may add additional indexes to support important queries and operations.

This document describes ascending/descending indexes on a single field.

The following operation creates an ascending index on the score field of the records collection:

    db.records.createIndex( { score: 1 } )
    
<b>Create an Index on an Embedded Field:</b>

The following operation creates an index on the location.state field:

    db.records.createIndex( { "location.state": 1 } )

Compound Indexes
----------------


