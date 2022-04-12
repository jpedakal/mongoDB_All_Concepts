A record in MongoDB is a document, which is a data structure composed of field and value pairs. 
MongoDB documents are similar to JSON objects. The values of fields may include other documents, 
arrays, and arrays of documents.


The advantages of using documents are:
-----------------------------------------------------------------------------------------------
--> Documents (i.e. objects) correspond to native data types in many programming languages.
--> Embedded documents and arrays reduce need for expensive joins.
--> Dynamic schema supports fluent polymorphism.


Document Size Limit
------------------------------------------------------------------------------------------------
--> The maximum BSON document size is 16 megabytes.

--> The maximum document size helps ensure that a single document cannot use excessive amount of RAM or, 
    during transmission, excessive amount of bandwidth. To store documents larger than the maximum size, 
    MongoDB provides the GridFS API. See mongofiles and the documentation for your driver for more 
    information about GridFS.
    
