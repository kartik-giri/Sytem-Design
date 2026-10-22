# What is Monolith?
- In monolith architecture the whole application is developed as the single application unit. It contains only single deployable application unit for whole backend of the appicaiton.
- For example. In ecommerce app the devs maintain the single backend for different servies like authentication, user management, order management etc.

# What is Micro service?
- Microservice is the service which should own a specific business capability and ideally own its data.
- In micro service architecure devs maintain the individual, manageble services which are independtly deployable and does communicate with other micro services for example authentication service communicating with user management service or websocket service communicate with order service.

# WHy should we use microservice architecture.
1. Independent scaling: If there is some component in backend which have a lot traffic, in that case we can create that component microservice and scale it indvidually.
2. Fault isolation : To not have single point of failure. Using microservice we can distrbute and manage the indvidual services to isolate the fault and reduce blast radius.
3. Techonology flexibility: Also using microservice architecture we can create different services in different tech stack.

# How do clients request in a microservice architecture?
- Every microservice is independtly deployable services. Their instances maybe run difference machines or containers and therfore may have different network address. is usually deployed on different machine with different IP address or domain.
- It would be very condusing or hard to send req to different micro services from client.
- That' why we use API gateways. using API gateways clients sends request to the single endpoint of API gateway and the API gateway checks the request, does authentication etc and route the req to the correct microservice and return the response from microservce back to client.
![APIGATEWAY](/img/APIGateway.png)
![APIGATEWAYARCH](/img/APIGatewayARCH.png)
- Also if we want to scale the microservice we can use loadbalancer in between api gateway and number of machines where micro serice is hosted.
![APIGATEWAYWITHLOADBALANCER](/img/APIGAtewayWithLOadbalancer.png)

