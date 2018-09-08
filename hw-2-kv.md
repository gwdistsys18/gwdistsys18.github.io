---
layout: page
title: "HW 2 - KV Store"
permalink: /hw-2/
---

> More details about the assignment submission requirements will be posted later.
>
> [Groups must be formed](https://goo.gl/forms/DZfJWKGZW5Z5x3kw1) by Friday 9/14, end of class (but you are strongly encouraged to do this earlier)
>
> **Due:** Friday 9/21 at 10AM

In this homework you will build a simple key value (KV) store similar to the one we discussed in class. This is a group assignment.  *Each group can have between 1-4 students.*

To complete the assignment you must:
 - Write a client and a server in C, Python, or Java that supports the Basic GW-KV protocol described below (60 points)
 - Add extra features from the list below (25 points)
 - Evaluate the performance of your KV store's throughput and latency (15 points)

## Basic GW-KV Protocol  
Your KV Store must use an ASCII based protocol. You can make the following assumptions about the keys and values in the system:
 - Keys are strings composed of only letters and numbers. Keys are at most 64 characters long.
 - Values are strings composed of any ASCII symbols *except for new line characters*. Values are at most 1KB in size.

Your KV Store should support the following operations:
 - **SET** adds a key and value to the server
 - **GET** returns a value to the client for the requested key
 - **STATS** returns a count of objects currently stored in the KV store

You should precisely describe all of the messages in your protocol in your `README.md` file.  

## The Client and Server
You can write your client and server in C, Python, or Java. You must use the socket interface for communication.  If you use Java, you may use the server provided in [HW 1](/hw-1/) as a base.

The **Server** should store keys and values in a data structure such as a hash table. You do not need to write your own code for the hash table. For the basic server implementation you do not need to do anything complicated for memory management (i.e., you do not need to implement your own eviction policy and can assume that your KV store will not run out of space). The server does not need to support parallelism (multi-threading)

The **Client** should be
Each socket connection should issue a single request.

## Extra Features
Depending on your group size you will need to implement additional features to increase the complexity of your KV store. However, you cannot implement the same set of extra features as any other group.
 - Groups with 1-2 members must implement 1 additional feature.
 - Groups with 3-4 members must implement 3 additional features.

Possible extra features include:
 - Support for binary values
 - Support for a binary-based protocol
 - Support parallelism in the server using threads (note that the HW 1 java server already does this, so you cannot use that code to qualify for this extra feature)
 - Support parallelism using non-blocking IO
 - Support a fixed sized data store with an eviction policy
 - Support a **MULTISET** operation that allows several key/value pairs to be added in a single connection
 - Support a **MULTIGET** operation that allows several key/value pairs to be retrieved in a single connection
 - Support for large value sizes
 - Support for both TCP and UDP
 - Something else (you must post your idea to Piazza to get approval)


## Performance Evaluation
You must measure the throughput (number of requests per second) and latency (milliseconds from when socket opens until it is closed) that your server can support. You may want to create a different client program to do this test. Your performance testing client should measure the performance of at least 10,000 operations made to the server.

In addition to testing the throughput and latency of SET and GET requests, you should also evaluate the extra feature(s) that you added.  For example, if your server supports large value sizes, then you should evaluate how the size of the value affects latency and throughput.

## Group Formation
You can use Piazza to communicate with other classmates who are looking for a team. Once you have determined all the members of your team, use this [GitHub Assignment](https://classroom.github.com/g/0qCvkCHk) to create your team's repository. The first member of the group will have to create the team by assigning it a name. **Be sure to only join the team with the name of your group.** Then you must [complete this form](https://goo.gl/forms/DZfJWKGZW5Z5x3kw1) to provide the instructor with a list of all team members and the language you plan to use.
