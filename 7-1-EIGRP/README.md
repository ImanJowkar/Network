# EIGRP

Enhanced Interior Gateway Routing Protocol (EIGRP) is a Cisco-proprietary, distance vector routing protocol used to dynamically route IP packets within a network. It was developed to overcome some of the limitations of older routing protocols like RIP (Routing Information Protocol) and IGRP (Interior Gateway Routing Protocol). EIGRP falls under the category of hybrid routing protocols because it incorporates features from both distance vector and link-state routing protocols.

Here are some key aspects of EIGRP:

1. **Advanced Metric Calculation**: Unlike traditional distance vector protocols, EIGRP uses a sophisticated metric calculation algorithm that takes into account various factors such as bandwidth, delay, reliability, load, and MTU (Maximum Transmission Unit) to determine the best path to a destination network.

2. **Diffusing Update Algorithm (DUAL)**: EIGRP uses the DUAL algorithm to ensure loop-free routing and fast convergence. DUAL allows routers to maintain multiple feasible successor routes to a destination, providing redundancy and faster convergence in case of link failures.


3. **Partial Updates**: EIGRP sends only partial updates when there are changes in the network topology, reducing the amount of bandwidth consumed compared to protocols like RIP, which send complete routing updates at regular intervals.


4. **Route Summarization**: EIGRP allows for the summarization of routes at network boundaries, reducing the size of routing tables and minimizing the propagation of routing information.

5. **Authentication**: EIGRP supports authentication mechanisms to secure routing updates exchanged between routers, ensuring that only authorized routers participate in routing processes.

6. **Scalability**: EIGRP is designed to scale well in large networks, providing efficient routing in complex environments with multiple interconnected routers and subnets.

Overall, EIGRP is a robust and scalable routing protocol commonly used in enterprise networks, particularly those using Cisco networking equipment.