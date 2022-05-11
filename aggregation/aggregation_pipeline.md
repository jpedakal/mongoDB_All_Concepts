* The aggregation pipeline is a framework for data aggregation modeled on the concept of data processing pipelines. 
* Documents enter a multi-stage pipeline that transforms the documents into aggregated results. 


      db.orders.aggregate([
         { $match: { status: "A" } },
         { $group: { _id: "$cust_id", total: { $sum: "$amount" } } }
      ]);


<b>First Stage</b> 
* The $match stage filters the documents by the status field and passes to the next stage those documents that have status equal to "A".

<b>Second Stage</b>
* The $group stage groups the documents by the cust_id field to calculate the sum of the amount for each unique cust_id.

Calculate Total Order Quantity
------------------------------
The following aggregation pipeline example contains two stages and returns the total order quantity of medium size pizzas grouped by pizza name:

           db.orders.aggregate( [

         // Stage 1: Filter pizza order documents by date range
         {
            $match:
            {
               "date": { $gte: new ISODate( "2020-01-30" ), $lt: new ISODate( "2022-01-30" ) }
            }
         },

         // Stage 2: Group remaining documents by date and calculate results
         {
            $group:
            {
               _id: { $dateToString: { format: "%Y-%m-%d", date: "$date" } },
               totalOrderValue: { $sum: { $multiply: [ "$price", "$quantity" ] } },
               averageOrderQuantity: { $avg: "$quantity" }
            }
         },

         // Stage 3: Sort documents by totalOrderValue in descending order
         {
            $sort: { totalOrderValue: -1 }
         }

       ] )
