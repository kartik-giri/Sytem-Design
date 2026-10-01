# What is Auto scaling?
- Let's say we have created a website and hosted on single machine. The single machine can handle 1000 users per day. But on certain day traffic can become over 1 lakh.
in this case we can add 100 more machines to handle the more incoming traffic. But in this case it will make us waste the money because on average day we don't need 100 machines.
- That's why we need Auto scaling which let us add the cetain mechanism that if the CPU of EC2 instage goes above a certain threshold launch the new machine and route the traffic accordingly all automatically.
- This changing number in servers based on the incoming traffic is called auto scaling.