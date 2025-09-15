# Distributed System

## Key characteristics

1. Scalability: Systems ability to handle growing demands
	1. Horizontal: adding more servers
	2. Vertical: upgrade existing hardware
2. Reliability: System continues to function correctly even when components fail
3. Availability: Percentage of time a system remains operational
	1. 99.99% -> 52.6 mins / year
	2. 99.90% -> 8.76 hours / year
4. Efficiency
	1. Latency: Delay in getting the first response
	2. Throughput: Number of operations handled in a given time

## CAP Theorem (Scalability vs Consistency)

A distributed system can only guarantee two properties:
1. Consistency: All nodes display identical data; reads always reflect most recent write
2. Availability: Every request receives a response
3. Partition Tolerance: System keeps running despite network failures (if communication breaks between nodes -> system still provides service at the expense of consistency or availability)

| System Type                             | Guarantees                                                                                                                                                 | Explanation                                                                               | Example                                                                                   |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| CA (Consistency + Availability)         | Ensures that every read receives the most recent write (Consistency) and every request receives a response (Availability)                                  | Cannot tolerate network partitions. Rare in real distributed systems; mostly theoretical. | Traditional relational databases in a single node setup (e.g., SQLite, single-node MySQL) |
| CP (Consistency + Partition Tolerance)  | Ensures Consistency and continues to operate despite network partitions, but may sacrifice Availability                                                    | During network partitions, the system may reject requests to maintain consistency.        | HBase, MongoDB (in majority-write mode), Zookeeper                                        |
| AP (Availability + Partition Tolerance) | Ensures the system continues to operate during network partitions and every request receives a response, but may serve stale data (sacrifices Consistency) | Prioritizes availability over immediate consistency; eventual consistency is common.      | Cassandra, CouchDB, DynamoDB                                                              |

## Load Balancer
Distributes incoming requests across multiple servers.

**Global Load Balancer:** DNS based routing to the closest regional data center (AWS Route 53)
**Local Load Balancer**: NGINX, AWS ELB

Can be single point of failure!!

1. Algorithms
	1. Least Connection: To server with fewest active connections
	2. Round Robin: Cycle through list of servers
	3. IP Hash: Client IP Address determines which server receives the request
2. Placement
	1. Between Users & webservers
	2. Between webservers & Application servers
	3. Between Application servers & Database Servers

## Cache

1. Level
	1. Application Cache
	2. CDN (static media)
		1. Cache content closer to the user to reduce latency
2. Challenges
	1. Consistency: Cache Invalidation Strategies
			1. Write Through: Written to cache & storage at the same time (increases write latency)
			2. Write-Around: Writing directly to storage (increase read latency) 
			3. Write Back: First written to cache -> later to storage (risking data loss)
	2. Cache Eviction Policies: Prevent Cache overflow
		1. Least Recently Used (removes LRU items)
		2. First In First Out: Removes the oldest items first
		3. Least Frequently Used: Removes least often accessed items
## Storage

|             | SQL                                               | NoSQL                                                                                                                             |
| ----------- | ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Structure   | Rigid Schema                                      | Flexible Schema                                                                                                                   |
| Queriying   | Structured Query Language                         | Different (client library specific)                                                                                               |
| Scalability | Vertical Scaling<br>Horizontal Scaling (Sharding) | Horizontal Scaling                                                                                                                |
| Reliability | ACID compliant                                    | BASE: Not ACID compliant (sacrifices for performance & scalability)                                                               |
| Examples    | Postgres, MySQL                                   | 1. Key-Value Stores (Redis)<br>2. Document Databases (Mongo DB)<br>3. Wide-Column Stores (Casandra)<br>4. Graph Databases (neo4j) |
### ACID Principles
1. Atomicity: Transaction is fully completed or not at all 
2. Consistency: Transaction brings DB from one valid state to another (rules, triggers, data types, foreign keys, etc.)
3. Isolation: Transactions do not interfere with each other
4. Durability: Once transaction is committed its changes are permanent

### BASE principles
1. Basically Available: Every request gets a response (may not be up-to-date)
2. Soft State: System state may change over time, even without new input (replica sync)
3. Eventual Consistency: If no new updates are made, all replicas will eventually converge to the same state

### Index: Database Query Performance

Index: Separate data structure which points to the location of the actual data
Improves Read Performance but can slow down write performance (on INSERT & UPDATE index must be updated as well)

1. B-tree (default): Equality, range queries, ORDER BY, unique constrains
2. Hash Index: Equality
3. GIN (Generalized Inverted Index): Searching within values (arrays, JSONB, full-text search)
4. GiST (Generalized Search Tree): Geometric data, full-text search
5. BRIN: Naturally ordered by timestamps, sequential IDs (stores summaries for blocks of rows instead of individual entries)

### Database Partitioning Methods
Parent table is divided into smaller child tables. 
Queries against parent table is routed automatically to the right partitions.
Improves Performance / Scalability: Smaller Indexes & Parallelism; skip irelevant partitions, vacuum partitions independently ([[Datebase Vaccuuming]]), preparation for future scaling
Can cost performance: Longer planning time

1. Range Partitioning: Range of values (e.g. date)
2. List Partitioning: Based on Specific value (e.g. country code)
3. Hash Partitioning: Distributed across partitions based on hash function of column value (even distribution if list or range is not possible)
4. Composite Partitioning: Combination of methods (e.g. range + hash)

### Database Sharding Methods
1. ...Same as partitioning methods
2. Geographical sharding: Users are routed to the nearest shard
3. Functional sharding: Orders Shard A, users Shard B, logs Shard C