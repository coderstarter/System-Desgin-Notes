### Trade-offs in Databases: Horizontal vs. Vertical Sharding

#### Which is the Best Database Sharding Approach?
Choosing between horizontal and vertical sharding depends on the specific needs of your organization. Both methods involve adding resources to your infrastructure to handle growth, prevent downtime, and reduce latency. Deciding the best approach involves evaluating the pros and cons of centralized and distributed databases.

#### Centralized Database
**Advantages:**
- Easy data maintenance (updating and backups).
- Strong consistency and ACID transactions.
- Simpler programming model.
- Efficient for small amounts of data on a single node.

**Disadvantages:**
- Slows down with high query rates.
- Single point of failure, higher risk of downtime.

#### Distributed Database
**Advantages:**
- Fast data access from the nearest or most-used shard.
- Different levels of data transparency can be stored separately.
- Intensive queries can be split into parallel subqueries for faster processing.

**Disadvantages:**
- Accessing data from multiple sites can be slow.
- Joins across partitions can be complex and costly.
- Maintaining data consistency across sites is challenging.
- Synchronizing updates and backups takes time.

#### Query Optimization and Processing Speed
Query performance in a distributed database depends on factors like query type, number of shards, communication speed, hardware, and database type. Here's an example scenario:

**Database Schema:**
- **Store Table**: 10,000 rows, site A.
- **Product Table**: 100,000 rows, site B.
- **Sales Table**: 1,000,000 rows, site A.

**Query Example:**
```
Select Store_key from (Store JOIN Sales JOIN Product)
where Region = 'East' AND Brand = 'Wolf';
```

**Communication Assumptions:**
- Data rate = 50M bits/second
- Access delay = 0.1 seconds

**Possible Approaches:**
1. **Move Product Table to Site A**: 
   - Total time = 0.1 + (100,000 * 200) / 50,000,000 = 0.5 seconds

2. **Move Store and Sales to Site B**:
   - Total time = 0.2 + (10,000 + 1,000,000) * 200 / 50,000,000 = 4.24 seconds

3. **Filter Brand at Site B and Move Results to Site A**:
   - Total time = 0.1 + (10 * 200) / 50,000,000 ≈ 0.1 seconds

The third approach, filtering at site B, is the fastest with 0.1 seconds of latency. This example shows the importance of query optimization in distributed databases.

#### Conclusion
Data distribution through vertical or horizontal sharding improves:
- **Reliability** (fault tolerance)
- **Performance**
- **Storage capacity** and cost balance

Choose centralized or distributed databases based on your application's needs.
