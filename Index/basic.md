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
