# Db stress


## Cassandra-store-stress


Variation of Bandwidth in MB/s with key-value batch size in Bytes.

| #                          	| 614     	| 1024    	| 3072    	| 15360    	| 32768   	| 65536   	|
|----------------------------	|---------	|---------	|---------	|----------	|---------	|---------	|
| SEQUENTIAL WRITE           	| 1.39953 	| 2.08492 	| 6.74197 	| 25.6199  	| 36.6982 	| 50.0723 	|
| SEQUENTIAL READ KEY/VALUES 	| 36.85   	| 65.2504 	| 26.4902 	| 18.2165  	| 15.2918 	| 44.0081 	|
| TRUNCATE TABLE             	| 616     	| 133     	| 898     	| 760      	| 764     	| 727     	|

### Summary
1. These tests were done on a local dev workstation with one/three node cassandra cluster.
2. Bandwidth of writes increases when batch size increases. 
3. Bulk read seems to perform worse than even sequestial write when batch size is large.
3. Truncate is independent of size of table. So indeed truncate is metadata change only.

