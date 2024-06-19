### Global and Local Load Balancing

Load balancing is necessary not only within a data center but also at a global level to efficiently distribute traffic. Here’s an overview of how global and local load balancing function:

#### Introduction

- **Global Server Load Balancing (GSLB)**: Distributes traffic across multiple geographical regions.
- **Local Load Balancing**: Manages traffic within a data center to improve efficiency and resource utilization.

#### Global Server Load Balancing

GSLB ensures traffic is routed to the appropriate data center based on factors like geographic location, server availability, and health of the data centers. It provides automatic failover in case of regional issues, such as power or network failures. GSLB can be implemented on-premises or via Load Balancing as a Service (LBaaS).

**How GSLB Works**:
- GSLB can route requests to multiple data centers.
- Local load balancers in each data center maintain communication with the GSLB, sharing health and status information.
- GSLB uses this data to make informed routing decisions.

#### Load Balancing in DNS

DNS can perform GSLB by responding with multiple IP addresses for a single query, using a round-robin method to distribute load across different servers.

**DNS Round-Robin Method**:
1. User from ISP requests the IP address of a service.
2. DNS responds with a list of IP addresses, reordered for each query.
3. Users receive different IP addresses, distributing the load.

**Limitations of DNS Round-Robin**:
- Uneven load distribution due to different numbers of users per ISP.
- DNS does not account for server crashes, distributing IPs of failed servers until the TTL expires.

Despite its limitations, round-robin DNS is still widely used, with short TTL values helping to mitigate some issues.

**Application Delivery Controllers (ADCs)**:
- ADCs are part of the application delivery network (ADN).
- They perform tasks like web acceleration, SSL offloading, proxy services, and IP traffic optimization.
- ADCs implement GSLB with real-time server health monitoring and optimized request forwarding.

#### The Need for Local Load Balancers

DNS has limitations in load balancing, such as:
- Packet size constraints preventing inclusion of all server IP addresses.
- Limited control over client behavior.
- Clients may not choose the closest or least busy server.
- Slow recovery from failures due to DNS caching.

Local load balancers address these issues by managing traffic within a data center. They act as reverse proxies, using virtual IP addresses (VIPs) to distribute incoming requests among available servers.

#### What is Local Load Balancing?

Local load balancers are situated within a data center and are responsible for efficiently distributing client requests to the servers. They use techniques like reverse proxy to manage this distribution, ensuring optimal performance and resource utilization.

#### Conclusion

Global and local load balancing work together to ensure efficient traffic management across and within data centers. While DNS can perform basic GSLB, ADCs offer more advanced and reliable global load balancing. Local load balancers further optimize resource use within individual data centers, ensuring high availability and performance. Future lessons will delve deeper into the specifics of local load balancers and their implementation in complex environments.
