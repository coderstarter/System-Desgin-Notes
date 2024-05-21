# Network Abstractions: Remote Procedure Calls

## Overview

Remote Procedure Calls (RPCs) provide a way to simplify the process of executing code on a remote server, making it appear as though it's running locally. This abstraction helps developers focus on their application logic without worrying about the complexities of network communication.

## What is an RPC?

RPC is an interprocess communication protocol widely used in distributed systems. It spans the transport and application layers of the OSI model, enabling a computer program to execute a procedure in a different address space.

### Key Points
- **Abstraction**: RPC hides the complexities of remote interactions.
- **Interprocess Communication**: Used for executing procedures in separate address spaces.

## How Does RPC Work?

When an RPC is made, the calling environment pauses, sends the procedure parameters over the network, executes the procedure remotely, and returns the results to the caller. 

### Components of an RPC System

1. **Client**
2. **Client Stub**
3. **RPC Runtime (Client-side)**
4. **Server**
5. **Server Stub**
6. **RPC Runtime (Server-side)**

### RPC Process

1. **Initiation**: The client initiates a call with parameters.
2. **Parameter Packing**: The client stub packs the parameters into a message.
3. **Message Delivery**: The client's RPC runtime sends the message to the server.
4. **Message Receipt**: The server's RPC runtime receives the message.
5. **Unpacking and Execution**: The server stub unpacks the message and executes the procedure.
6. **Result Return**: The server stub packs the result and sends it back.
7. **Result Unpacking**: The client's RPC runtime receives the result and sends it to the client stub.
8. **Completion**: The client stub unpacks the result and returns it to the caller.

### RPC Runtime Responsibilities
- Message transmission
- Retransmission and acknowledgment
- Encryption

### Illustration of RPC Workflow

![RPC Workflow](rpc-workflow.png)

## Real-World Usage

### Google
- Uses RPC in its distributed infrastructure.
- Developed gRPC, an open-source RPC framework used in services like Google Search and YouTube.

### Uber
- Uses RPC for real-time location tracking, ride matching, and communication between drivers and riders.
- Facilitates fast and responsive services.

### Facebook
- Uses Thrift for RPC in most services.
- Enables interoperability between different languages and efficient communication.

## Summary

RPC abstracts the complexities of network communication, allowing developers to build distributed applications as if they were calling local procedures. This method enhances developer productivity by letting them focus on application design rather than low-level communication details.

---

This summary provides a concise yet comprehensive overview of RPCs, their working mechanism, and real-world applications, making it suitable for revision purposes.
