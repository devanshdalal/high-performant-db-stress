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

### Meminfo
```
[admin@he-456-1d ~]$ cat /proc/meminfo
MemTotal:       528359868 kB
MemFree:        359669456 kB
MemAvailable:   476511512 kB
Buffers:            7324 kB
Cached:         105505292 kB
SwapCached:            0 kB
Active:         67679032 kB
Inactive:       85355088 kB
Active(anon):   48174020 kB
Inactive(anon):   151748 kB
Active(file):   19505012 kB
Inactive(file): 85203340 kB
Unevictable:       48604 kB
Mlocked:           48604 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Dirty:              2456 kB
Writeback:             0 kB
AnonPages:      47570148 kB
Mapped:          2163664 kB
Shmem:            800568 kB
Slab:           13894984 kB
SReclaimable:   13533980 kB
SUnreclaim:       361004 kB
KernelStack:      121552 kB
PageTables:       161624 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:    264179932 kB
Committed_AS:   127694444 kB
VmallocTotal:   34359738367 kB
VmallocUsed:           0 kB
VmallocChunk:          0 kB
HardwareCorrupted:     0 kB
AnonHugePages:  41156608 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:     2205880 kB
DirectMap2M:    178114560 kB
DirectMap1G:    358612992 kB
```

### CPU info
```
[admin@he-456-1d ~]$ cat /proc/cpuinfo
processor	: 39
vendor_id	: GenuineIntel
cpu family	: 6
model		: 62
model name	: Intel(R) Xeon(R) CPU E5-2690 v2 @ 3.00GHz
stepping	: 4
microcode	: 0x427
cpu MHz		: 3000.000
cache size	: 25600 KB
physical id	: 1
siblings	: 20
core id		: 12
cpu cores	: 10
apicid		: 57
initial apicid	: 57
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr pdcm pcid dca sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm epb kaiser tpr_shadow vnmi flexpriority ept vpid fsgsbase smep erms xsaveopt dtherm ida arat pln pts
bugs		: cpu_meltdown spectre_v1 spectre_v2 spec_store_bypass l1tf mds
bogomips	: 6007.35
clflush size	: 64
cache_alignment	: 64
address sizes	: 46 bits physical, 48 bits virtual
power management:
```

### Summary
2. Leveldb is not a distributed store, hence corresponding bandwidth are better  than cassandra. 
3. Bulk read seems to perform worse than even sequestial write when batch size is large.
3. Truncate is worse compared to cassandra, there is some hidden gc cost. 

## [Apache Cassandra™ Leads All Others In Latest NoSQL Benchmark](https://www.datastax.com/apache-cassandra-leads-nosql-benchmark).

NoSQL databases are challenging relational technologies by delivering the flexibility required of modern applications. But, which NoSQL database is best architected to handle performance demands of today’s workloads? 

Benchmarks recently run by End Point an independent database firm, stress-tested Apache Cassandra, HBase, MongoDB, and Couchbase on operations typical to real-world applications. Results showed that Cassandra outperformed its NoSQL counterparts. 

In fact, for mixed operational and analytic workloads typical to modern Web, Mobile and IOT applications, Cassandra performed six times faster than HBase and 195 times faster than MongoDB.

![alt text](https://user-images.githubusercontent.com/5080310/63927250-f1961600-ca6a-11e9-9828-49aa7dd504ba.png)

## References
1. https://gist.github.com/devanshdalal/9ae6c474a9235db853ce2dbb4ebfa425
