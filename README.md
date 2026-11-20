# IPv4 Router with Access Control (SDN, Mininet + POX)

A software-defined network that routes IPv4 traffic deterministically across a simulated enterprise and enforces security policy with access-control rules, all programmed from a Python OpenFlow controller.

## The network

- **Topology (Mininet + Open vSwitch):** four switches (two department floors, a core switch and an internet edge), two department subnets of four hosts each, an internal server, and two external hosts: one trusted, one untrusted.
- **Controller (POX, OpenFlow):** handles PacketIn events, decides the output port per switch and destination, and installs flow entries so later packets are forwarded in the switch without going back to the controller. IP traffic is never flooded.

## Security policy

Drop rules are installed as higher-priority flow entries than forwarding rules:

- The untrusted external host cannot reach the server at all, and cannot ping anything internal.
- The trusted external host cannot reach the server, and cannot ping Department B.
- The two departments cannot ping each other, while normal traffic within each subnet still flows.

This is the same segmentation pattern used in campus networks and data centers to limit reconnaissance and protect sensitive servers.

## Tech

Python, POX (OpenFlow 1.0), Mininet, Open vSwitch, Ubuntu 22.04 on Multipass, shell test scripts

## Source code

Built as UC Santa Cruz coursework, so the source is kept private to respect course policy. I'm happy to walk through the controller with recruiters on request: [LinkedIn](https://www.linkedin.com/in/mohamedsbadri/).
