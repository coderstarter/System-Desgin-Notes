### Summary of Back-of-the-Envelope Calculations (BOTECs) in System Design

**Introduction to BOTECs:**
- BOTECs are quick, rough calculations done to estimate parameters and feasibility without getting into detailed complexities.
- They provide preliminary evaluations, useful in system design and interviews.
- Example: Estimating neighborhood population by counting houses and averaging people per household.

**Importance in System Design:**
- Modern systems are complex with various interconnected nodes (e.g., web servers, application servers, caches, databases).
- BOTECs help focus on essential aspects, like resource feasibility, by abstracting details.

**Common BOTEC Applications:**
1. Estimating concurrent TCP connections a server can support.
2. Determining requests per second (RPS) a server can handle.
3. Calculating storage requirements for a service.

**Types of Data Center Servers:**
1. **Web Servers:**
   - Handle API calls, need good processing power.
   - Example: Facebook's web server with 32 GB RAM and 500 GB storage.
2. **Application Servers:**
   - Run core applications and business logic, need extensive resources.
   - Example: Facebook's application server with 256 GB RAM and 6.5 TB storage.
3. **Storage Servers:**
   - Store vast amounts of data, structured (SQL) and unstructured (NoSQL).
   - Example: Facebook's storage server with 120 TB capacity.

**Typical Server Specifications:**
- Example server: Intel Xeon, 64 cores, 256 GB RAM, 16 TB storage.

**Important Latencies:**
- L1 cache reference: 0.9 ns
- L2 cache reference: 2.8 ns
- Main memory reference: 100 ns
- SSD read (1 MB): 200,000 ns (200 µs)
- Disk seek: 4,000,000 ns (4 ms)

**Important Rates:**
- MySQL: 1,000 queries per second (QPS)
- Key-value store: 10,000 QPS
- Cache server: 100,000 to 1 million QPS

**Estimating Requests Per Second (RPS):**
1. **Types of Requests:**
   - CPU-bound: Depend on the processor (e.g., compressing 1 KB data).
   - Memory-bound: Depend on memory access (e.g., reading 1 MB from RAM).
   - IO-bound: Depend on IO subsystems (e.g., reading 1 MB from disk).

2. **CPU Time Calculation:**
   - Use the formula: `CPU time per program = Instructions per program × CPI × CPU time per clock cycle`
   - Example assumptions: 3.5 million instructions per request, CPI = 1, CPU clock rate = 3.5 GHz.
   - Calculate total requests per second for a single core, then multiply by the number of cores.

**Example Calculation:**
1. CPU clock cycles per second: \(3.5 \times 10^9\)
2. CPU time per clock cycle: \( \frac{1}{3.5 \times 10^9} \)
3. CPU time per program: \( \frac{3.5 \times 10^6}{3.5 \times 10^9} = 10^{-3} \) seconds
4. Total requests per second (single core): \( \frac{1}{10^{-3}} = 1,000 \) requests
5. Total requests per second (64 cores): \( 64 \times 1,000 = 64,000 \) requests

**Conclusion:**
- BOTECs simplify complex system design by abstracting details, making it easier to estimate resources and feasibility quickly.
- These calculations are foundational for initial designs, later validated through prototypes and monitoring for accurate capacity planning.
