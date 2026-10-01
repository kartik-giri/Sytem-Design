# What is scaling?
- Scaling means increasing the specs of the machines for exmple incerasing the cpu, storage, ram etc. or Addigng more machines in the server and distributing the computing and data to multiple mahchines so that the more load can be handle efficicintly.

# Veritcal scaling?
- In vertical scaling the specs of the single machine is being increased for exmaple ram, cpu, storage etc. So that the single server can handle the  more load efficitently.
- Vertical sclaing is used to scale sql db or state full application because it is hard and risky to  maintian the state in distbuted system.

# Horizontal scaling?
- Using vertical scaling we can scale server to a certain extent.
- In horizontal scaling we add more machines in the server and distribute the load accordingly. so that load can be handled efficiently.
- In horizontal sclaing we add load balancer. The client send the req to the load balancer and the load balancer route the request to the server which is less busier to handle the load management.

- In horizontal scaling the applications should be stateless. Because if the server A stores the user session data and in 2nd req the load balancer route the request to server B than there will be no user session data.
- Instead of keeping important session state inside Server A's memory, we can put shared state in something like Redis or a database.
- This is one of the reasons horizontal scaling is much easier when your application layer is stateless.