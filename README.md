# Db stress


## Cassandra-store-stress


Variation of Bandwidth in MB/s with key-value batch size in Bytes. Client concurency is 1.

| #                          	| 614     	| 1024    	| 3072    	| 15360    	| 32768   	| 65536   	|
|----------------------------	|---------	|---------	|---------	|----------	|---------	|---------	|
| SEQUENTIAL WRITE           	| 1.39953 	| 2.08492 	| 6.74197 	| 25.6199  	| 36.6982 	| 50.0723 	|
| SEQUENTIAL READ KEY/VALUES 	| 36.85   	| 65.2504 	| 26.4902 	| 18.2165  	| 15.2918 	| 44.0081 	|
| TRUNCATE TABLE             	| 616     	| 133     	| 898     	| 760      	| 764     	| 727     	|

### Summary
1. Bandwidth of writes increases when batch size increases. 
2. Bulk read seems to perform worse than even sequestial write when batch size is large.
3. Writes outperforms reads on average strenthening the fact that cassandra is write performant.
4. Truncate is independent of size of table. So indeed truncate is metadata change only.


## Leveldb streess tests

| #                          	| Bandwidth(batch size: 65536 B)    	|
|----------------------------	|------------------------------------	|
| SEQUENTIAL WRITE           	| 85.1396  	                          |
| SEQUENTIAL READ KEY/VALUES 	| 79.40825 	                          |
| TRUNCATE TABLE             	| 78.92575 	                          |

### Summary
2. Leveldb is not a distributed store, hence corresponding bandwidth are better  than cassandra. 
3. Bulk read seems to perform worse than even sequestial write when batch size is large.
3. Truncate is worse compared to cassandra, there is some hidden gc cost. 

## [Apache Cassandra™ Leads All Others In Latest NoSQL Benchmark]. (https://www.datastax.com/apache-cassandra-leads-nosql-benchmark).

NoSQL databases are challenging relational technologies by delivering the flexibility required of modern applications. But, which NoSQL database is best architected to handle performance demands of today’s workloads? 

Benchmarks recently run by End Point an independent database firm, stress-tested Apache Cassandra, HBase, MongoDB, and Couchbase on operations typical to real-world applications. Results showed that Cassandra outperformed its NoSQL counterparts. 

In fact, for mixed operational and analytic workloads typical to modern Web, Mobile and IOT applications, Cassandra performed six times faster than HBase and 195 times faster than MongoDB.

![alt text](https://user-images.githubusercontent.com/5080310/63927250-f1961600-ca6a-11e9-9828-49aa7dd504ba.png)

## References
1. https://gist.github.com/devanshdalal/9ae6c474a9235db853ce2dbb4ebfa425
