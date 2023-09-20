# Inter-Vlan Routing
There are two main ways to implement inter-VLAN routing:

- `Router on a stick (ROAS):` This method uses a single physical interface on a router to connect multiple VLANs on a switch. It is a simple and cost-effective solution for small networks, but it has some drawbacks, such as limited bandwidth, security risks, and configuration complexity.
- `Layer 3 switch inter-VLAN routing:` This method uses a Layer 3 switch to route traffic between VLANs. Layer 3 switches have dedicated hardware for routing, which makes them faster and more scalable than ROAS. However, they are also more expensive.

In addition to these two methods, there is also a third option called legacy inter-VLAN routing. However, this method is no longer recommended because it is outdated and has several security risks.

Which method you choose will depend on the specific needs of your network. If you have a small network and are on a tight budget, then ROAS may be a good option for you. However, if you have a larger network or need high performance and scalability, then a Layer 3 switch is a better choice.