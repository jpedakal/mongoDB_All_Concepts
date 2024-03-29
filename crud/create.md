To insert a single document into collection. If the document does not specify an _id field, MongoDB adds the _id field with an ObjectId value to the new document.


        db.inventory.insertOne({ item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5}});


To insert multiple documents into collection.

        db.inventory.insertMany([
         { item: "journal", qty: 25, tags: ["blank", "red"], size: { h: 14, w: 21, uom: "cm" }},
         { item: "mat", qty: 85, tags: ["gray"], size: { h: 27.9, w: 35.5, uom: "cm" } },
         { item: "mousepad", qty: 25, tags: ["gel", "blue"], size: { h: 19, w: 22.85, uom: "cm" }}
       ]);

To inserts a single document or multiple documents into a collection.

    db.inventory.insertOne({ item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5}});

    db.inventory.insert([
     { item: "journal", qty: 25, tags: ["blank", "red"], size: { h: 14, w: 21, uom: "cm" }},
     { item: "mat", qty: 85, tags: ["gray"], size: { h: 27.9, w: 35.5, uom: "cm" } },
     { item: "mousepad", qty: 25, tags: ["gel", "blue"], size: { h: 19, w: 22.85, uom: "cm" }}]);
   
   
<b>Note:</b> If the collection does not currently exist, insert operations will create the collection.


_id Field
------------------------------------------------------------------------------------------------------
* In MongoDB, each document stored in a collection requires a unique _id field that acts as a 
    primary key.
* If an inserted document omits the _id field, the MongoDB driver automatically generates an ObjectId 
    for the _id field.
* This also applies to documents inserted through update operations with upsert: true.
