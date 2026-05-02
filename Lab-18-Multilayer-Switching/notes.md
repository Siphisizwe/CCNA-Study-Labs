LAB 18 - Multilayer Switching
Date: 24 April 2026

WHAT IS A MULTILAYER SWITCH:
A Layer 3 switch capable of both switching and routing.
More efficient than router on a stick because routing
happens inside the switch. No external router needed
for inter-VLAN routing.

KEY CONCEPTS:

SVI (Switch Virtual Interface):
- Virtual interface assigned to a VLAN
- Acts as the default gateway for that VLAN
- Assigned the last usable IP of the subnet
- Command: interface vlan 10

Routed Port:
- Converts a switch port from Layer 2 to Layer 3
- Command: no switchport
- Then assign IP address like a router interface

IP Routing:
- Must be enabled on multilayer switch to route traffic
- Command: ip routing

Default Route:
- Catch-all route for unknown destinations
- Sends unknown traffic to the router
- Command: ip route 0.0.0.0 0.0.0.0 10.0.0.194

TOPOLOGY:
R1 G0/0        = 10.0.0.194/30  (P2P to SW2)
SW2 G1/0/2     = 10.0.0.193/30  (P2P to R1)
SW2 Vlan10 SVI = 10.0.0.62/26   (VLAN10 gateway)
SW2 Vlan20 SVI = 10.0.0.126/26  (VLAN20 gateway)
SW2 Vlan30 SVI = 10.0.0.190/26  (VLAN30 gateway)

COMMANDS USED:
ip routing
interface vlan 10
ip address 10.0.0.62 255.255.255.192
no shutdown
interface g1/0/2
no switchport
ip address 10.0.0.193 255.255.255.252
ip route 0.0.0.0 0.0.0.0 10.0.0.194
show ip interface brief
show ip route

WHAT I LEARNED:
- Multilayer switch routes internally, no external router needed
- SVI replaces router subinterfaces for inter-VLAN routing
- no switchport converts Layer 2 port to Layer 3 routed port
- Default route sends all unknown traffic to R1
- ip routing must be enabled or switch will not route
