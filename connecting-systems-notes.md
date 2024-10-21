# Connecting-Systems-Notes

## Introduction

This is a short collection of notes I have generated from 
the choice of topics Kevin had given at the lecture. 
In the following we will do a deep dive into load balancers.
 We will cover the various types of load balancers, and what problems they solve.


## Why load balancers?

Instead of explicitly telling you rightaway what a load balancers does, 
let's discuss a problem that a load balancer was created to solve. 

Pretend you are an artist who has built their own small 
website to sell their artwork. This entire website is managed by a 
one server with a single API instance handling requests. 
Now for small volumes of traffic this server can keep up and 
nobody notices any issues. However your work has become famous 
overnight and the amount of traffic is overwhelming the system. 
So how do we solve this problem? If your solution is to 
add another web server and split the traffic between them congratulations 
you have now just thought of the concept of load balancing.

More formally, load balancing is the act of distributing network traffic to 
the different servers in the network in order to distrubte the work across 
multiple servers. This will have the advantage that you can deal with a larger number of requests.

## Static and Dynamic Load Balancing

There are two types of load balancing called static and dynamic load balancing. 
In this section we will go over each type 
and describe when you might prefer one over the other

### Static Load balancers

A static load balancer is an approch to load balancing that follows fixed rules 
and works independent of the current server state in order to to distribute the load. 
Examples of static load balancing includes the folling:

- Round-robin - This appoach is exactly what it sounds like. The 
load balancer distributes request by cyclically going around each server.
- Weighted Round-robin - This approach is similar to the first 
but maybe some servers are given multiple requests in a cycle 
since they are one may be more powerful
- IP hash - This method takes the clients IP address and hashes 
it and then uses that hash to decide which server to send a request.

#### Advantages an disadvantages of static load balancers

Advantages:

- The first advantage is that this a very simple approach to solving 
the problem above.

- Another is that it has lower overhead and does not require lots 
of computational complexity since how the traffic will be distributed is fixed.

Disadvantages:

- One significant drawback is that a static load balancing approach 
is inherently inflexible and if your the traffic conditions change the approach may be suboptimal.

- More limited fault tolerance. since if a server fails to change 
it may be more difficult for the load balcning to take the failure 
of a server into account.




### Dynamic load balancing 

If a staitc load balancers is an appoeach to load balancing which allocates request independent of the server state 
then dynamic load blancers is one which takes the current server state into account when allocating requests. Approaches of dyanmic load balancing include:

- Method of least connection - checks which server has the fewest 
connections open at a given point in time in order to balance the load.

- Quickest response time - uses how quickly a server responds in 
order to decide to allocate resources

- Another approach is to analyse what resources each server 
has available and allocate based on that. i.e. how much CPU and 
memory a server has available.

#### Advantages and Disadvatages of Dynamic load balancers.

Advantages:

- Contrasting itself with static load balancing the dynamic 
approach to load balancing allows greater flexibility to changing conditions in 
particular with dealing with unpredictable workloads.

- It is also an approach that is much more scalable as you can 
efficeintly distrubute work across many servers and is easier to 
accomodate bigger system size or capacity.

Disadvantages:

- Compared to static load balancing, dynamic load balancing is much more complex.

- There is a higher computational overhead as you must always monitor 
the state of the system at all times.

- There can also be issues regarding configurations.


### Static versus Dynamic load Balancing

So when should be use a static verus a dynamic load balancer? 
From information online, and from what we can see in the our list of 
advantages/disadvantages above, a 
static approach seems to be preferred when the number of requests is 
steady and their is a lack of variability in the number or types of requests. 
If you are an e-commerce company such as THG you will probably benefit 
from a dynamic appraoch as traffic to the servers can be varied and with high peaks, 
like on black friday.

## Bibliography 

- https://www.cloudflare.com/en-gb/learning/performance/what-is-load-balancing/

- https://www.geeksforgeeks.org/static-vs-dynamic-load-balancing/

- https://aws.amazon.com/what-is/load-balancing/

- Kevin's slides






