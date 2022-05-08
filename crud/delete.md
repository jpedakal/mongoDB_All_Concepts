Delete All Documents
---------------------------------------------------------------------------------------------------------
To delete all documents from a collection, pass an empty filter document {} to the 
db.collection.deleteMany() method.

The following example deletes all documents from the inventory collection:

  db.inventory.deleteMany({});


Delete All Documents that Match a Condition
---------------------------------------------------------------------------------------------------------
To delete all documents that match a deletion criteria, pass a filter parameter to the deleteMany() 
method.

The following example removes all documents from the inventory collection where the status field
equals "A":

  db.inventory.deleteMany({ status : "A" });


Delete Only One Document that Matches a Condition
---------------------------------------------------------------------------------------------------------
To delete at most a single document that matches a specified filter (even though multiple documents may
 match the specified filter) use the db.collection.deleteOne() method.

The following example deletes the first document where status is "D":

  db.inventory.deleteOne( { status: "D" } );
