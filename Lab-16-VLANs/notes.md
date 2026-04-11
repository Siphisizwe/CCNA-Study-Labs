LAB 16 - VLANs Part 1

What is a VLAN:
A separate broadcast domain. Mini network where traffic 
stays isolated. Used for security and performance.

VLANs in this lab:
VLAN10 - Engineering - 10.0.0.0/26
VLAN20 - HR          - 10.0.0.64/26
VLAN30 - Sales       - 10.0.0.128/26

Key commands:
switchport mode access
switchport access vlan 10

Gateway addresses:
VLAN10 gateway = 10.0.0.62
VLAN20 gateway = 10.0.0.126
VLAN30 gateway = 10.0.0.190

Router interfaces:
R1 G0/0 = 10.0.0.62
R1 G0/1 =  10.0.0.126
R1 G0/2 = 10.0.0.190
