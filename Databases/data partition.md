### Data Partitioning Models

#### Why Do We Partition Data?
Partitioning data is essential as traditional databases struggle with scalability under increasing data and traffic loads, impacting latency and throughput. To maintain the benefits of relational databases (range queries, secondary indices, ACID properties), partitioning distributes data across multiple nodes, balancing load and improving performance.

#### Sharding
Sharding splits a large dataset into smaller chunks stored on different nodes. Balanced partitioning is crucial to avoid hotspots and ensure efficient data retrieval.

**Types of Sharding:**
1. **Vertical Sharding**: 
   - **Description**: Divides tables into smaller tables with different columns or places different tables on separate database instances.
   - **Example**: Splitting an `Employee` table into `Employee` and `EmployeePicture` tables.
   - **Advantages**: Improves data retrieval speed, particularly for tables with large text or blobs.
   - **Disadvantages**: Manual and complex, especially with frequent joins.

2. **Horizontal Sharding**: 
   - **Description**: Splits a table into multiple tables by rows, distributing them across servers (shards).
   - **Strategies**:
     - **Key-Range Based Sharding**:
       - **Description**: Assigns each partition a continuous range of keys.
       - **Advantages**: Easy to implement range queries and know where to look for specific keys.
       - **Disadvantages**: Cannot perform range queries with keys other than the partition key; uneven key distribution can cause imbalance.
     - **Hash-Based Sharding**:
       - **Description**: Uses a hash function on an attribute to determine partitioning.
       - **Advantages**: Uniform key distribution across nodes.
       - **Disadvantages**: Cannot perform range queries.

#### Consistent Hashing
- **Description**: A variant of hash-based sharding that helps in rebalancing partitions when nodes are added or removed.
- **Advantages**: Efficient handling of changes in the number of nodes without major data movement.
- **Disadvantages**: Can still suffer from uneven distribution if not properly managed.

#### Rebalance the Partitions
Strategies to manage and rebalance partitions:
- **Avoid Hash Mod n**: Prevents data distribution issues when the number of nodes changes.
- **Fixed Number of Partitions**: Pre-defines a number of partitions irrespective of node count.
- **Dynamic Partitioning**: Adjusts the number of partitions based on load.
- **Partition Proportionally to Nodes**: Distributes partitions based on the number of nodes.

#### Partitioning and Secondary Indexes
Secondary indexes can also be partitioned:
- **By Document**: Indexes are partitioned along with the documents they index.
- **By Term**: Indexes are partitioned based on the terms they index.

#### Request Routing
**ZooKeeper**: A tool often used to manage distributed applications and ensure synchronized request routing across shards.

### Conclusion
Partitioning (or sharding) is vital for managing large datasets across multiple nodes, ensuring scalability, availability, and performance while maintaining the advantages of traditional databases. Different sharding strategies address specific needs and challenges, requiring careful planning and implementation.
