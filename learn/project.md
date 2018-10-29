---
layout: page
title: Final Project
permalink: /learn/project/
---

If you do a **Final project** you should:
  - Pick a a project that involves a substantial programming component and include a measurement/cost study.  For example, you might build a simple web / database application spread across several AWS services, and then evaluate its performance with different EC2 instance types.
  - Final projects can be completed in groups with 1-4 members. *It is recommended that research projects be performed in groups, unless you are a PhD student already active on a related research project.*
  - You must post a description of your project plan to Piazza for professor approval by **Friday November 2nd before class.** If you plan to do a final project you are encouraged to meet with the professor in advance.
  - If you do your project in a team, then you must include a writeup in your readme of which student was responsible for each part of the project.
  - You will need to demonstrate your project working to the professor before the end of the semester.


### "Startup" Projects
This type of project is your chance to build a new web application or tool with relatively few limitations. If you have a start up in mind or the idea for an application which you think would be useful, then you can spend a month building it as your project. Your project must meet this criteria:
  - It must have at least 4 components running on different servers or services. For example, you could build a web application that includes 1) a client web browser, 2) a Node.js web application, 3) a Memcached key value store, and 4) a database.  These components can either be applications that you run on an EC2 server, or they can be provided by a cloud service (e.g., using AWS DynamoDB as your database).
  - You must perform some kind of performance evaluation on your application. For example, if it is a web application you could use the Apache Bench tool to measure the throughput and latency of issuing different types of requests.  Or you could do a performance comparison of issuing requests to Memcached vs the database.  If it is a data analysis project using machine learning algorithms, then you should evaluate the accuracy of the models you are building.

Sample Projects:
  - Anything you can think of... a web application that solves a problem in your life, analysis of a large data set using big data and ML tools, etc.

### "Research" Projects
This type of project is more focused on answering a research question. Since you have limited time, you will want a narrow research problem, and most likely your focus will be on gathering preliminary data.  Some of these projects are ones which could turn into a semester long 3 credit Research course in the Spring if you do very well at them!

Sample Cloud Projects:
  - **Coordinated container management:** Microservices are a popular way to break an application down into smaller components that are easier to scale up and down.  Microservices are often combined with a container management system such as Kubernetes. However, a problem with existing container management services is that they observe each container in isolation when trying to detect that they are overloaded. This can lead to problems such as scaling up one component, only for that to cause a different microservice component to become overloaded.  In this project you will explore ways to do *coordinated container management*.  To do this, you should:
    - Setup the environment: build a simple microservice application that allows you to setup a "chain" of services that send requests to each other. You may be able to find sample microservices to use as a template, or you might have to build your own. The service doesn't need to do anything useful - you just need a way to be able to deploy a configurable microservice with an adjustable number of services.
    - Setup a workload: deploy Kubernetes to manage your microservice.    You will need to find or design a workload creation tool that lets you create "bursts" of requests from new users. Measure the throughput and latency of the system when using the Kubernetes auto-scaling system.
    - Measure the problem: You should be able to show that if the request rate rises quickly, the later microservices in the chain do not scale up quickly enough, leading to some slow or dropped requests. Study how Kubernetes does auto-scaling and measure how long it takes it to setup a new container when it detects overload.
    - Propose a solution: From your workload measurements you should be able to explain where the problems are (detecting overload? scaling up after it is detected? etc).  Propose a solution to the problem.

Sample SDN/NFV Projects:
  - **SDN - NFV Interactions:** OpenNetVM currently has limited support for interacting with an SDN controller. This project is a good one if you want to learn more about SDN and the OpenFlow protocol used to communicate information between network devices and the SDN controller. Ideally the OpenNetVM platform should be able to:
    - Send reports to the SDN controller so that the controller knows what NFs are running and statistics such as their current load.
    - Receive rules from the SDN controller to configure service chain rules. Each new flow into the system should be sent to the controller which will return a service chain rule to be applied to all remining packets in that flow.
    - We have some preliminary code for both of these, which you can use as a base. You will need to finish the code and do an evaluation to show the costs and benefits of communicating with an SDN controller.
  - **NFV Key Value Store:** In this project you will explore the benefits of building a key value store (like you did at the start of the semester) on a high performance NFV platform.  You should:
    - Build a key value store that supports the memcached UDP protocol to set and get data using the OpenNetVM platform.
    - Evaluate the performance of your NF compared to the Key Value store you built earlier and standard Memcached.
  - **KV Store Load Balancing:** In this project you will explore how NFV can be used as an application-aware load balancer for key value stores.  A common problem in KV stores is that some objects are much more popular than others. To handle that, you will build a load balancer that observes incoming traffic and automatically load balances it across multiple replicas.  You should:
    - Build an NF that can interpret memcached UDP `get` and `set` requests. It should measure the popularity of all keys being requested and decide how many times to replicate each key.  You can use streaming analytic techniques like a Lossy Counter to efficiently track the "top-k" most popular keys.
    - Design a load balancing algorithm that distributes requests to popular keys across multiple servers.
    - We have a paper, [NetKV](http://faculty.cs.gwu.edu/timwood/papers/16-ICAC-netkv.pdf), which proposes a design for this type of system, unfortunately the code is no longer usable. You can reimplement the system we proposed, or design a new one.
  - **TCP Hand-off:** The load balancer described above only works for UDP... why is that? The reason is that load balancing for TCP is much more challenging since you can't see any application-level data (such as the memcached key being requested, or the HTTP GET request) until after the 3-way handshake has been completed. This means that the load balancer itself must respond to the 3-way handshake to build a connection to the client, observe the request made by the client, and then repeat the 3-way handshake process with the selected back-end server.
    - Detect incoming SYN requests and reply with a SYNACK. This should allow the client to form a TCP connection with the LB.
    - The client will then issue its request (e.g., an HTTP request).  The LB should look inside the request and extract information such as the HTTP GET url to decide what server to forward to.
    - The LB then must send a SYN to the selected server and establish a TCP connection with it.
    - Now the LB has one TCP connection with the client and one TCP connection with the server. The LB must splice the two together by copying data from one to the other. The LB will need to modify the TCP sequence numbers in each packet so that the line up correctly for each connection.  This is called TCP splicing or hand-off.
