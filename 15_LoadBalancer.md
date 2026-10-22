# What is LoadBalancer?
- As the app traffic grows, We scale our server horizontally.
- In horizontal scaling backend/microserivce is being hosted on multiple servers.
- Now clients have multiple servcers to send requests. But clients are dumb and can't route the request to the appropraite server.
- That's why we need loadbalancer. It sits between the client and the mulitple servers and route the requests across available instances according to the routing algo. to the least busy servcer to manage the load efficiently.
- LoadBalancer algo
1. Round robin algo - in this the clients request are send sequentiolly to the servers in the circullar order.
- if there are 3 machines 1 req will go to first first serer and 3 goes to 3rd servcer and 4th goes to 1st server again.
2. Weighted round robin algo -> In this the weights are attached to the servers according to there specs and more reqs are routed to the servers which have more specs than othere serer to manage the load.
3. Least connection algo -> In this the load balancer route the request to the server which have least connections with the load balancer.
4. Hash based algo -> this algo takes anything from user like client ip, user id etc as input and hash that to find the server. This ensures the same client is consistently is routed to the same server.