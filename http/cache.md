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



