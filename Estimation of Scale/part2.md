### Introduction

In this lesson, we'll apply resource estimation techniques to a Twitter-like service, focusing on servers, storage, and bandwidth requirements. Using assumptions and principles such as the Pareto principle and back-of-the-envelope calculations (BOTECs), we'll derive estimations that help understand the feasibility and scale of the system. 

### Number of Servers Required

#### Assumptions:

1. **Daily Active Users (DAU)**: 500 million (M).
2. **Requests per User per Day**: 20.
3. **Server Capacity**: Each server (with 64 cores) can handle 64,000 requests per second (RPS).

#### Calculations:

1. **Total Requests per Day**:
   \[
   500 \text{ M users} \times 20 \text{ requests/user/day} = 10 \text{ billion requests/day}
   \]

2. **Average Requests per Second**:
   \[
   \frac{10 \text{ billion requests}}{86,400 \text{ seconds/day}} \approx 115,740 \text{ RPS}
   \]

3. **Number of Servers Required**:
   \[
   \frac{115,740 \text{ RPS}}{64,000 \text{ RPS/server}} \approx 2 \text{ servers}
   \]

### Points to Ponder:

- **Hidden Assumption**: The calculation assumes a perfectly uniform distribution of requests throughout the day, which is unrealistic. In reality, traffic spikes and non-uniform patterns must be accounted for.

### Peak Capacity Estimation

To handle flash crowds and peak loads, we must consider a worst-case scenario where all users might make requests simultaneously.

#### Peak Load Calculation:

1. **Total Requests at Peak**:
   \[
   10 \text{ billion requests}
   \]

2. **Number of Servers for Peak Load**:
   \[
   \frac{10 \text{ billion requests}}{64,000 \text{ RPS/server}} \approx 157,000 \text{ servers}
   \]

Given the astronomical number of servers required, we need to reconsider our assumptions.

### Improving the RPS of a Server

Assume a maximum of 100,000 servers:
1. **Maximum Requests per Server**:
   \[
   \frac{10 \text{ billion requests}}{100,000 \text{ servers}} = 100,000 \text{ RPS/server}
   \]

### Applying the Pareto Principle

By assuming 80% of traffic occurs within 20% of the time (4.8 hours):

1. **Total Requests in Peak Time**:
   \[
   0.8 \times 10 \text{ billion} = 8 \text{ billion requests}
   \]

2. **Peak Time Window**:
   \[
   4.8 \times 60 \times 60 = 17,280 \text{ seconds}
   \]

3. **Average RPS During Peak Time**:
   \[
   \frac{8 \text{ billion requests}}{17,280 \text{ seconds}} \approx 462,962 \text{ RPS}
   \]

4. **Number of Servers Required**:
   \[
   \frac{462,962 \text{ RPS}}{64,000 \text{ RPS/server}} \approx 8 \text{ servers}
   \]

### Graceful Degradation

During unexpected peak loads, such as during a significant news event:

1. **Shift to Static Content**: Reduce personalization and serve static content via CDN nodes.
2. **Optimize Multimedia**: Limit or compress multimedia content to ensure faster load times.

### Cost of Servers

Using AWS's m7i.16xlarge instance:
- **Hourly Cost**: $3.54816

1. **Cost for Minimum Servers (2)**:
   \[
   2 \times 3.54816 = \$7.096 \text{ per hour}
   \]

2. **Cost Under 80/20 Assumptions (8)**:
   \[
   8 \times 3.54816 = \$28.38 \text{ per hour}
   \]

3. **Cost for Peak Load (157,000)**:
   \[
   157,000 \times 3.54816 = \$557,061 \text{ per hour}
   \]

### Storage Requirements

#### Assumptions:

1. **Daily Active Users**: 500 million.
2. **Tweets per User per Day**: 3.
3. **Image Size**: 200 KB.
4. **Video Size**: 3 MB.
5. **Text and Metadata Size**: 250 bytes.
6. **Image Tweets**: 10%.
7. **Video Tweets**: 5%.

#### Calculations:

1. **Total Tweets per Day**:
   \[
   500 \text{ M} \times 3 = 1.5 \text{ billion tweets}
   \]

2. **Storage for Text**:
   \[
   1.5 \text{ billion} \times 250 \text{ bytes} = 375 \text{ GB/day}
   \]

3. **Storage for Images**:
   \[
   1.5 \text{ billion} \times 10\% \times 200 \text{ KB} = 30 \text{ TB/day}
   \]

4. **Storage for Videos**:
   \[
   1.5 \text{ billion} \times 5\% \times 3 \text{ MB} = 225 \text{ TB/day}
   \]

5. **Total Storage per Day**:
   \[
   0.375 \text{ TB} + 30 \text{ TB} + 225 \text{ TB} \approx 255 \text{ TB/day}
   \]

6. **Total Storage per Year**:
   \[
   255 \text{ TB/day} \times 365 \approx 93.08 \text{ PB/year}
   \]

### Bandwidth Requirements

#### Incoming Traffic:
- **Daily Data**: 255 TB
- **Bandwidth**:
  \[
  \frac{255 \times 10^{12} \text{ bytes}}{86,400 \text{ seconds/day}} \times 8 \approx 24 \text{ Gbps}
  \]

#### Outgoing Traffic:
- **Tweets Viewed per User per Day**: 50.
- **Active Users**: 500 million.
- **Traffic Mix**: Same as above (text, images, video).

1. **Daily Outgoing Data**: Calculate using similar assumptions and ratios as incoming.
2. **Bandwidth**:
   \[
   \approx 393.62 \text{ Gbps}
   \]

#### Total Bandwidth:
\[
24 \text{ Gbps (incoming)} + 393.62 \text{ Gbps (outgoing)} = 417.62 \text{ Gbps}
\]

### Conclusion

Estimations provide a framework for understanding the resources needed to support a large-scale service. By leveraging principles such as the Pareto rule and focusing on realistic assumptions and calculations, we can plan and optimize resources effectively. Practical strategies like graceful degradation, optimizing RPS, and adjusting for peak loads ensure resilience and efficiency in real-world scenarios.
