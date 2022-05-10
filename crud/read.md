Select All Documents in a Collection
----------------------------------------------------------------------------------------------------
To select all documents in the collection, pass an empty document as the query filter parameter 
to the find method. The query filter parameter determines the select criteria.

    db.inventory.find({});


Specify Equality Condition
---------------------------------------------------------------------------------------------------
The following example selects from the inventory collection all documents where the status equals "D"

    db.inventory.find({ status: "D" });


Specify Conditions Using Query Operators
---------------------------------------------------------------------------------------------------
The following example retrieves all documents from the inventory collection where status equals 
either "A" or "D"

    db.inventory.find( { status: { $in: [ "A", "D" ] } } );


$in --> Operator


Specify AND Conditions
----------------------------------------------------------------------------------------------------
The following example retrieves all documents in the inventory collection where the status equals "A" 
and qty is less than ($lt) 30

    db.inventory.find( { status: "A", qty: { $lt: 30 } } );


Specify OR Conditions
-----------------------------------------------------------------------------------------------------
The following example retrieves all documents in the collection where the status equals "A" or qty is 
less than ($lt) 30

    db.inventory.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } );


Specify AND as well as OR Conditions
------------------------------------------------------------------------------------------------------
In the following example, the compound query document selects all documents in the collection where the 
status equals "A" and either qty is less than ($lt) 30 or item starts with the character p

    db.inventory.find( {
         status: "A",
         $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
    } );

Match an Embedded/Nested Document
--------------------------------------------------------------------------------------------------------
For example, the following query selects all documents where the field size equals the document 
{ h: 14, w: 21, uom: "cm" }

    db.inventory.find( { size: { h: 14, w: 21, uom: "cm" } } )


Query on Nested Field
--------------------------------------------------------------------------------------------------------
The following example selects all documents where the field uom nested in the size field equals "in":

    db.inventory.find( { "size.uom": "in" } );

    db.inventory.find( { "size.h": { $lt: 15 }, "size.uom": "in", status: "D" } );


Match an Array
--------------------------------------------------------------------------------------------------------
The following example queries for all documents where the field tags value is an array with exactly two 
elements, "red" and "blank", in the specified order:

    db.inventory.find( { tags: ["red", "blank"] } );


If, instead, you wish to find an array that contains both the elements "red" and "blank", without 
regard to order or other elements in the array, use the $all operator:

    db.inventory.find( { tags: { $all: ["red", "blank"] } } );


Query an Array for an Element
-------------------------------------------------------------------------------------------------------
The following example queries for all documents where tags is an array that contains the string "red" 
as one of its elements:

    db.inventory.find( { tags: "red" } );


Query an Array with Compound Filter Conditions on the Array Elements
--------------------------------------------------------------------------------------------

To project name and price details from product collection.

    db.product.find( {}, { name: 1, price: 1 } );

To project name and price details and exclude "_id" from product collection.

    db.product.find( {}, { _id:0, name: 1, price: 1 } );
    
Query for an Element by the Array Index Position
-----------------------------------------------------
Using dot notation, you can specify query conditions for an element at a particular index or position of the array. The array uses zero-based indexing.
The following example queries for all documents where the second element in the array dim_cm is greater than 25:

    db.inventory.find( { "dim_cm.1": { $gt: 25 } } )
    
Query an Array by Array Length
-------------------------------
Use the $size operator to query for arrays by number of elements. For example, the following selects documents where the array tags has 3 elements.

    db.inventory.find( { "tags": { $size: 3 } } )
    
Query an Array with Compound Filter Conditions on the Array Elements
--------------------------------------------------------------------
The following example queries for documents where the dim_cm array contains elements that in some combination satisfy the query conditions; e.g., one element can satisfy the greater than 15 condition and another element can satisfy the less than 20 condition, or a single element can satisfy both:

    db.inventory.find( { dim_cm: { $gt: 15, $lt: 20 } } )
    
Query for an Array Element that Meets Multiple Criteria
--------------------------------------------------------
Use $elemMatch operator to specify multiple criteria on the elements of an array such that at least one array element satisfies all the specified criteria.
The following example queries for documents where the dim_cm array contains at least one element that is both greater than ($gt) 22 and less than ($lt) 30:

    db.inventory.find( { dim_cm: { $elemMatch: { $gt: 22, $lt: 30 } } } )
    
Query for a Document Nested in an Array
---------------------------------------
The following example selects all documents where an element in the instock array matches the specified document:

    db.inventory.find( { "instock": { warehouse: "A", qty: 5 } } )
    
Specify a Query Condition on a Field Embedded in an Array of Documents
---------------------------------------------------------------------
If you do not know the index position of the document nested in the array, concatenate the name of the array field, with a dot (.) and the name of the field in the nested document.

The following example selects all documents where the instock array has at least one embedded document that contains the field qty whose value is less than or equal to 20:

    db.inventory.find( { 'instock.qty': { $lte: 20 } } )
