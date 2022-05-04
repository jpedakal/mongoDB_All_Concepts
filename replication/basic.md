A replica set in MongoDB is a group of mongod processes that maintain the same data set. 
Replica sets provide redundancy and high availability, and are the basis for all production deployments.
 
This section introduces replication in MongoDB as well as the components and architecture of replica sets. 
The section also provides tutorials for common tasks related to replica sets.

* Replication provides redundancy and increases data availability.

<img width="712" alt="Screenshot 2022-04-26 at 3 37 39 PM" src="https://user-images.githubusercontent.com/40006634/165276822-e4cf209d-e47a-41cc-aa76-c3741fda142f.png">

<b>Automatic Failover</b>

* When a primary does not communicate with the other members of the set for more than the configured electionTimeoutMillis period (10 seconds by default), an eligible secondary calls for an election to nominate itself as the new primary. 
* The cluster attempts to complete the election of a new primary and resume normal operations.
<img width="712" alt="Screenshot 2022-04-26 at 3 42 52 PM" src="https://user-images.githubusercontent.com/40006634/165277708-398a0b8a-ae4f-4012-8401-1738444745e2.png">

* The replica set cannot process write operations until the election completes successfully. 
* The replica set can continue to serve read queries if such queries are configured to run on secondaries while the primary is offline.
* The median time before a cluster elects a new primary should not typically exceed 12 seconds, assuming default `replica configuration settings`. 
* This includes time required to mark the primary as unavailable and call and complete an election. 
* You can tune this time period by modifying the `settings.electionTimeoutMillis` replication configuration option. 
* Factors such as network latency may extend the time required for replica set elections to complete, which in turn affects the amount of time your cluster may operate without a primary. These factors are dependent on your particular cluster architecture.
* Lowering the `electionTimeoutMillis1 replication configuration option from the default 10000 (10 seconds) can result in faster detection of primary failure. 
* However, the cluster may call elections more frequently due to factors such as temporary network latency even if the primary is otherwise healthy. This can result in increased rollbacks for w : 1 write operations.

