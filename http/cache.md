### Cache

> The web cache is an HTTP device that automatically saves duplicates of documents.

the cache offers benefits such as:
1. Reducing network costs and unnecessary data.
2. Minimizing network delays.
3. Decreasing requests to the origin server.
4. Mitigating distance delays.

In this chapter, we will learn how the cache upgrades itself and reduces costs.


### Send Unnecessary Data

When many clients send requests to one origin server, the server has to respond to each client multiple times.
this unnecessary data communication causes delays. 

In such case, using a cache is helpful. 
the cache stores the origin server's responses and provides duplicates for client's requests, reducing the need for repeated communication with the server.


### Bandwidth Bottleneck

the cache can alleviate network bottleneck. 

many networks allocate more bandwidth for a local network client than to an origin server.
The speed at which clients access the server is equal to the speed of the slowest network component in that path.
Therefore, If the client could obtain a duplicate from LAN cache, performance could be improved.


### Flash Crowds

the caching is also important for Flash Crowds, which causes a serious problem.

### Distance Delay

Although bandwidth is not a problem, distance could be. 
All network routers introduce delay to internet traffic.
Even though there are not many routers between a client and a server, 
light itself could cause delay.
in this case, installing a cache could reduce the distance. 

### Cache hit and Cache miss

However, the cache doesn't store all the documents in the world. 
when a request arrives at the cache, 
it could be processed if there is a document corresponding to the request.
this is called a cache hit. If there is not, it is called the cache miss.
 
