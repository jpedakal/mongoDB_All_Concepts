Update a Single Document
-----------------------------------------------------------------------------------------------------
The following example uses the db.collection.updateOne() method on the inventory collection to update 
the first document where item equals "paper":

      db.inventory.updateOne(
         { item: "paper" },
         {
           $set: { "size.uom": "cm", status: "P" },
           $currentDate: { lastModified: true }
         }
      )

uses the $currentDate operator to update the value of the lastModified field to the current date. 
If lastModified field does not exist, $currentDate will create the field. See $currentDate for details


Update Multiple Documents
-------------------------------------------------------------------------------------------------------

The following example uses the db.collection.updateMany() method on the inventory collection to update 
all documents where qty is less than 50:

      db.inventory.updateMany(
         { "qty": { $lt: 50 } },
         {
           $set: { "size.uom": "in", status: "P" },
           $currentDate: { lastModified: true }
         }
      )
